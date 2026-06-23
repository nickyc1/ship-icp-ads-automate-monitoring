# Slack setup — get a webhook URL (from scratch)

The `Post to Slack` node posts to a **Slack incoming webhook**. You create one by making a
tiny Slack app. For a single webhook, doing it **from scratch** is the fastest path. Takes
about a minute, all clicks, nothing to install.

> ⚠️ A webhook URL is a secret. Anyone with it can post to your channel, and Slack
> auto-revokes URLs it finds leaked. For a live demo, use a throwaway workspace or a
> dedicated `#demo` channel, and don't leave the URL on screen.

---

## Fastest path: from scratch (do this live)

You're on the **Your Apps** screen (api.slack.com/apps). Then:

1. Click **Create New App** (green button, top-right).
2. Choose **From scratch**.
3. **App Name:** `Ads Reporting Bot`. **Pick a workspace.** Click **Create App**.
4. In the left sidebar, click **Incoming Webhooks**.
5. Toggle **Activate Incoming Webhooks** to **On**. The page refreshes with new options.
6. Scroll down, click **Add New Webhook to Workspace**.
7. On the permission screen, pick the **channel** (e.g. `#ads-reports`) and click **Allow**.
8. Back on the Incoming Webhooks page, under **Webhook URLs for Your Workspace**, click
   **Copy** next to the URL. It looks like:
   ```
   https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXX
   ```
9. In n8n, open the **Post to Slack** node and paste that into the **URL** field. Done.

Test it without n8n if you want:
```bash
curl -X POST -H "Content-type: application/json" \
  --data '{"text":"Hello from the Ads Reporting Bot."}' \
  https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXX
```

---

## Alternative: from a manifest (for attendees to clone the exact app)

Same result, one paste instead of toggling. Use this if you want everyone to build the
identical app.

1. **Create New App → From an app manifest.**
2. Pick the workspace, choose **JSON**, and paste [`slack-app-manifest.json`](slack-app-manifest.json).
3. Review, click **Create**.
4. You still finish with steps **6–9** above (Add New Webhook to Workspace → Allow → copy
   the URL). The manifest just pre-enables webhooks and names the bot for you.

## Why not the Slack CLI?

The Slack CLI (`slack create`) is great for building real apps, but it needs an install and
a login flow. For one incoming webhook in a live demo, the from-scratch clicks above are
faster and have nothing to break on stage.
