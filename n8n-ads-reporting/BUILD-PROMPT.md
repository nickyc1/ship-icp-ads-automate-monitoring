# Build prompt — n8n ads reporting digest

Paste this into Claude Code to generate the workflow live. It works best with the
[n8n-recipes](https://github.com/nickyc1/n8n-recipes) skill loaded so Claude knows the node
schema and expression syntax. The goal is a valid `workflow.json` you import straight into n8n.

---

## The prompt

```
You are building an n8n workflow that produces a daily paid-media performance digest
and posts it to Slack. Output a single valid n8n workflow JSON file I can import
(Workflows → Import from File). Use current node types and typeVersions.

GOAL
A scheduled workflow that pulls Google Ads and Meta metrics, merges them, grades each
campaign on profit-to-spend, flags anomalies, writes a plain-language digest, and posts
it to a Slack channel. For now it must run end to end on DUMMY data with no external
credentials except a Slack webhook, so it can be demoed live.

NODES (in order)
1. Schedule Trigger — daily at 09:00.
2. "Mock Google Ads" — a Code node that returns an array of campaigns with:
   campaign, platform:"google", spend, conversions, conversion_value, cpa, ctr, clicks, impressions.
   Include 4-5 realistic campaigns, at least one underperformer and one clear winner.
3. "Mock Meta Ads" — a Code node, same shape, platform:"meta", with frequency added.
4. Merge — combine both into one list.
5. "Analyze" — a Code node that, for each campaign, computes:
   - profit_to_spend = conversion_value / spend
   - a grade: "green" if profit_to_spend >= the platform target (Google 1.5, Meta 0.5), else "red"
   - a decision string: high conv + low spend => "scale", low conv + high spend => "cut",
     below target => "investigate / pause", else "hold"
   - an anomaly flag if cpa > 2x a passed-in historical_cpa or spend spikes
   Then build a single markdown digest string: a headline summary line, a table or bullet
   list of campaigns with grade + decision, and a "needs attention" section listing red /
   anomalous campaigns first. Keep the language plain and skimmable.
6. "Post to Slack" — an HTTP Request node POSTing { "text": <the digest> } to a Slack
   incoming webhook. Leave the URL as a clearly-marked placeholder.

RULES
- Runs on dummy data with zero credentials except the Slack webhook.
- The digest leads with the decision, not raw metrics. Profit, not ROAS, is the hero number.
- Comment each Code node so a non-engineer can read it.
- Make the Google/Meta mock nodes trivially swappable for real HTTP Request / MCP calls later.

After you output the JSON, give me a 4-line summary of how to import it and where to paste
my Slack webhook.
```

---

## Why it's built this way

- **Dummy data first** so the whole room can run it without wiring up an ad account live (the hard part is connecting your own sources, and that's homework, not stage time).
- **Profit-to-spend, not ROAS**, because platform-reported numbers overstate the story. The same period showed Google reporting $541K on $64K spend while first-party data showed $420K. Reconcile against real profit.
- **The digest leads with the decision.** Scale, cut, or hold — in plain language. Metrics are the evidence, not the headline.
- **Swappable inputs.** Only the two mock nodes change when you go live. Everything downstream stays put.
