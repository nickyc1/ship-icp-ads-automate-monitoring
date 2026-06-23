# Example output

When you run [`../BUILD-PROMPT.md`](../BUILD-PROMPT.md) against the dummy customer list,
Claude Code writes two files here:

- **`icp-dossier.html`** — the ICP page. The rich avatar at the top (the agency owners
  buying 20-30+ times: think "Marketing Agency Jordan"), the segments below, a "their words"
  section of verbatim language, and the likely pains and desires. Everything traceable to a
  row in `customers.csv`.
- **`campaign.html`** — an example Google Ads campaign built for that avatar: scored RSA and
  PMax copy, Meta variants, and the audience plan. Every asset carries a 1-5 score against
  the ICP, and anything under 4 is cut with a reason.

These are generated live in the workshop, so they're intentionally not committed here. Run
the prompt and they'll appear in this folder.

What to look for when it runs:
- The avatar should come out of the **top ~10% by revenue** (the agency segment), not the
  one-time buyers.
- The copy should echo the **verbatim notes** ("lifetime deals are a cheat code for an
  agency"), not generic SaaS-speak.
- Rows with blank fields should **stay blank** in the dossier, not get filled with guesses.
