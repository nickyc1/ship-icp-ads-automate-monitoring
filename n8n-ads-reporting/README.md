# n8n Ads Reporting — the daily digest that comes to you

**Outcome:** a daily performance digest across Google Ads and Meta that lands in Slack, already analyzed, so you stop logging into dashboards.

This is the system behind ["I stopped logging into Google Ads"](https://www.nickbuilds.ai/blog/i-stopped-logging-into-google-ads). Monday reviews across three accounts went from 3+ hours to about 60 seconds. The dashboard becomes a message you skim with your coffee.

---

## What it does

```
Schedule trigger (daily, ~9am)
   → pull Google Ads metrics      ┐
   → pull Meta metrics            ┘→ merge into one table
   → analyze: grade every campaign, flag anomalies, rank by profit
   → write the digest in plain language
   → post to Slack
```

In production you also pull first-party profit (Looker / Snowflake) and product data (Merchant Center), because **ROAS in Google Ads is not profit, and your business runs on profit.** The starter keeps it to the two ad platforms so it runs anywhere.

## What it measures

- **Profit-to-spend ratio** per campaign, graded green (above target) or red (below). See [`benchmarks.md`](benchmarks.md) for the example thresholds — tune them to your business.
- **CAC vs LTV** — a campaign isn't "bad" because CAC is high if the buyers it brings are worth more. Breakeven horizon matters (Nick uses ~3 months).
- **Anomalies** — spend spikes, spend running below the mid-afternoon baseline, CPA more than 2x its historical norm.
- **The decision, in plain language** — scale / pause / test. High conversion + low spend = underfunded, scale it. Low conversion + high spend = cut it. Below target = investigate or pause.

You make the decisions. The workflow is the analyst, not the boss.

---

## Run it with dummy data (the demo)

There is no import button on the n8n **Overview** screen. In n8n you import from *inside*
a workflow, so you create a blank one first. From the Overview screen:

1. Click **Create workflow** (top-right of the screen).
2. On the empty canvas, open the **⋯** menu (top-right, next to the **Save** button).
3. Choose **Import from URL...** and paste this, then **Import**:
   ```
   https://raw.githubusercontent.com/nickyc1/ship-icp-ads-automate-monitoring/main/n8n-ads-reporting/starter-workflow.json
   ```
   *(Or choose **Import from File...** and pick `n8n-ads-reporting/starter-workflow.json` from your clone — same result.)*
4. The workflow drops onto the canvas: six active nodes, plus an **Email the report**
   node that ships switched off (ignore it for now). Click the **Post to Slack** node and
   paste your Slack incoming webhook into the **URL** field. Need one? Follow
   [`slack-setup.md`](slack-setup.md) — it's about a minute, from scratch.
5. Click **Test workflow** (button at the bottom-center). The two Code nodes emit the dummy
   data, **Analyze** grades it, and the digest posts to your Slack channel.

No Google or Meta account required. It runs entirely on the dummy data so you see the whole
pipeline fire end to end.

> Demo tip: **Import from URL** is the cleanest move on a screen share — no file dialog, no
> hunting through folders. Have the Slack webhook ready in your clipboard beforehand.

### Also email the report

Want the digest in inboxes too? The workflow already has an **Email the report (optional)**
node wired up next to Slack, switched off so it never breaks the demo. Turn it on and add a
Gmail credential by following [`email-setup.md`](email-setup.md) — the fast path is a Gmail
App Password over SMTP (no Google Cloud setup).

## Where the data comes from

The numbers you just saw in Slack are **hardcoded inside the two `Mock Google Ads` and
`Mock Meta Ads` Code nodes** — open either node and the array is right there in the
JavaScript. They're realistic but invented (one campaign is deliberately a red flag so the
grading has something to catch). Nothing is fetched from anywhere; that's why the demo can't
break.

The `dummy-data/*.json` files in this folder are **not** read by the workflow. They're the
**data contract**: the exact shape (`campaign, spend, conversions, conversion_value, cpa,
historical_cpa, ctr...`) your real ad data has to arrive in. Match that shape and everything
downstream just works.

## What you keep vs. what you swap

This is the whole point of the demo. The workflow has two halves:

- **Swap (the data source):** the two `Mock` nodes. In real life these become live API calls.
- **Keep (the brain):** the `Analyze` node and the Slack / email delivery. The grading, the
  anomaly flags, the plain-language decisions, the digest format — none of it cares where the
  numbers came from. That's the reusable part you take with you.

To go live, replace only the two mock nodes so they output the same shape as the contract:

- **Google Ads:** an HTTP Request node (or the Google Ads node) calling the [Google Ads API](https://developers.google.com/google-ads/api) `searchStream` for your customer ID. Cleanest path: a local `google-ads-mcp` server — see [google-ads-mcp-setup](https://github.com/nickyc1/google-ads-mcp-setup).
- **Meta:** the [Meta Ads CLI/MCP](https://www.nickbuilds.ai/blog/meta-just-released-an-ads-cli-and-mcp) — one OAuth, no third-party app in the middle. See [meta-ads-mcp-setup](https://github.com/nickyc1/meta-ads-mcp-setup).

Leave `Analyze`, Slack, and email exactly as they are.

> Before you let anything **write** to an account, run it read-only for ~2 weeks. When you do add write actions, gate them: Claude proposes → a second AI reviews → a human approves. Two AIs and a human before any dollar moves.

---

## Build it from scratch instead

Want to see it built live rather than imported? Paste [`BUILD-PROMPT.md`](BUILD-PROMPT.md) into Claude Code (with the [n8n-recipes](https://github.com/nickyc1/n8n-recipes) skill loaded) and it will generate this workflow for you.
