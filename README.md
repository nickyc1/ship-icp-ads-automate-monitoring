# Ship ICP-driven ad campaigns and automate monitoring

The starter repo for the CXL live workshop with **Nick Christensen** and **Tarek Reslan**.

> One marketer now does the work of a copywriter, an analyst, and a media buyer. This repo is the working proof. Clone it, run the prompts, and you walk out with two systems you keep.

The whole idea: stop logging into dashboards, and stop guessing at copy. You design the system once, then it runs the day-to-day. *"The software you don't log into wins."*

---

## What's in here

This repo has one folder per thing we demo live. Each folder is self-contained: a README that explains the outcome, a `BUILD-PROMPT.md` you paste into Claude Code to build it, and dummy data so it runs without touching a real ad account.

| Folder | What you build | Deliverable |
|--------|----------------|-------------|
| [`n8n-ads-reporting/`](n8n-ads-reporting/) | A daily Google + Meta performance digest that lands in Slack, already analyzed | A working n8n workflow JSON |
| [`icp-dashboard/`](icp-dashboard/) | ICP research turned into scored ad copy: an ICP page + an example Google Ads campaign | A starter repo + an ICP-to-copy prompt |

Run them in that order. The first ends the daily dashboard grind. The second goes upstream to where the winning copy comes from. Together they close a loop: research feeds copy, copy ships, the digest grades it, the decisions sharpen the next round of research.

---

## Prerequisites

- **Claude Pro** (or Claude Code access)
- **GitHub** account (free)
- **n8n** account (free trial is fine) — only for the first module
- A **Slack** workspace where you can add an incoming webhook (for the demo digest)

You do **not** need a real Google Ads or Meta account to follow along. Every module ships with dummy data so the workflow runs end to end. The last step of each README shows you how to point it at your own sources.

---

## How to use this in the workshop

1. Clone the repo: `git clone https://github.com/nickyc1/ship-icp-ads-automate-monitoring.git`
2. Open it in your terminal and start Claude Code.
3. Open the folder we're working on, read its `README.md`, then paste its `BUILD-PROMPT.md` into Claude Code.
4. Fire it with the dummy data and watch the result.

Read-only first, then write, then automate, then scale. That sequence is the whole game.

---

## The source material

Everything here is built on the systems Nick runs in production. The full write-ups:

- [Find your rich avatar](https://www.nickbuilds.ai/blog/find-your-rich-avatar-matt-appsumo)
- [My GitHub is my marketing operating system](https://www.nickbuilds.ai/blog/my-github-is-my-marketing-operating-system)
- [Claude memory vs GitHub](https://www.nickbuilds.ai/blog/claude-memory-vs-github-the-system-behind-seamless-sessions)
- [I stopped logging into Google Ads](https://www.nickbuilds.ai/blog/i-stopped-logging-into-google-ads)
- [The complete Google Ads AI agent automation playbook](https://www.nickbuilds.ai/blog/google-ads-ai-agent-automation-playbook)
- [The complete guide to managing Google and Meta with AI](https://www.nickbuilds.ai/blog/complete-guide-managing-google-and-meta-with-ai)
- [Meta just released an Ads CLI and MCP](https://www.nickbuilds.ai/blog/meta-just-released-an-ads-cli-and-mcp)
- [People buy from people](https://www.nickbuilds.ai/blog/people-buy-from-people)

More agent stack skills: [github.com/nickyc1](https://github.com/nickyc1)
