# Email setup — also send the report by Gmail

The workflow ships with an **Email the report (optional)** node already wired in, sitting
next to **Post to Slack**. It's **switched off** so the Slack demo always runs clean. Turn
it on to email the same digest to a list of people.

There are two ways to connect Gmail. For a live demo, use the **App Password (SMTP)** path:
it's the fastest and has no Google Cloud setup. The Gmail OAuth node is the cleaner
long-term option but needs a Google Cloud OAuth client, which is slow to do on stage.

---

## Fastest path: Gmail App Password + SMTP (do this live)

**A. Create a Gmail App Password** (one time, ~30 seconds)

1. The Google account needs **2-Step Verification ON** (myaccount.google.com → Security).
2. Go to **myaccount.google.com/apppasswords**.
3. Name it `n8n` and click **Create**.
4. Copy the **16-character password** Google shows you. (You won't see it again.)

**B. Turn on the node in n8n**

5. In the workflow, click the **Email the report (optional)** node and **enable** it
   (the toggle on the node, or right-click → **Activate**).
6. In the node's **Credential to connect with**, click **Create new credential** (type:
   **SMTP**) and fill in:
   - **User:** your full Gmail address
   - **Password:** the 16-character App Password from step 4
   - **Host:** `smtp.gmail.com`
   - **Port:** `465`
   - **SSL/TLS:** on
   Save it.
7. Back in the node, set:
   - **From Email:** your Gmail address
   - **To Email:** the recipients (comma-separated for several people)
   - **Subject:** `Daily Paid Media Digest`
   - **Text** is already set to `{{ $json.digest }}` — the same digest that goes to Slack.
8. Click **Test workflow**. The digest now posts to Slack **and** lands in the inboxes.

That's it. The node already connects from **Analyze**, so it gets the exact same digest.

---

## Cleaner long-term path: the Gmail node (OAuth2)

Better for ongoing use (no app password to rotate, sends as your real Gmail with threading),
but slower to set up live because it needs a Google Cloud OAuth client.

1. In Google Cloud Console: create an **OAuth client ID** (type: Web application) and add
   n8n's OAuth redirect URL (n8n shows it when you create the credential).
2. In n8n, add a **Gmail** node, create a **Gmail OAuth2** credential, paste the client ID
   and secret, and click **Sign in with Google**.
3. Configure the node: **To**, **Subject**, and **Message** = `{{ $json.digest }}`.
4. Connect **Analyze → Gmail**, the same way the optional SMTP node is wired.

Use SMTP for the workshop. Mention OAuth as the upgrade once they're running it for real.

> Tip: the digest is plain text. If you want a nicer email, switch the node's **Email
> Format** to **HTML** and wrap the digest in basic HTML, or have Claude generate an HTML
> version in the Analyze node.
