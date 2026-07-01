# Build prompt — ICP to scored ad copy

Paste this into Claude Code with this folder open. It runs the two skills in order and
produces two pages you can open in a browser: the ICP dossier and an example campaign.

### Bring your own data

Do not rename the `dummy-data/` folder or its files — the prompt below refers to them by
name. Just swap the contents:

- **`dummy-data/customers.csv`** (required) — replace with your customer export. Keep the
  filename. Minimum columns: an email and a revenue/spend column (the rest lift quality).
- **`reviews.md`, `support-tickets.md`, `sales-call-notes.md`** (optional) — replace with your
  own verbatim language, or empty them. This is where the best copy comes from.
- Then fill in your landing page + brand in Pass 2 below and run the prompt unchanged.

---

## The prompt

```
Read voice/voice-rules.md, skills/icp-synthesis/SKILL.md, and skills/ad-copy/SKILL.md in
full before doing anything. Your source data is the whole dummy-data/ folder:
- customers.csv         (the list: revenue, orders, title, company, industry)
- reviews.md            (verbatim review language)
- support-tickets.md    (pains, in their words)
- sales-call-notes.md   (why they actually buy)

PASS 1 — SYNTHESIZE THE ICP (use the icp-synthesis skill)
- Rank customers by trailing revenue. Isolate the top ~10%: that cohort is the rich avatar.
- Cross-reference each high-value name against reviews.md, support-tickets.md, and
  sales-call-notes.md and pull their exact words.
- Describe that avatar as a real person, grounded only in what's in the data. Give them a
  name in the spirit of "Marketing Agency Matt." Note their job, their business model, why
  they buy repeatedly, and the outcome they're really buying.
- Identify the other distinct segments below the avatar.
- Pull EXACT customer language wherever the data has it (notes, reviews). Keep grammar and
  slang intact. Never paraphrase real phrasing into corporate-speak. If a field has no real
  signal, leave it blank — empty beats hallucinated.
- Output icp-dossier.html: a clean single-page dossier — the avatar up top, then segments,
  then a "their words" section of verbatim language, then the likely pains and desires.

PASS 2 — BUILD AN EXAMPLE CAMPAIGN (use the ad-copy skill)
- Target the rich avatar. Landing page: [YOUR LANDING PAGE URL] · Business name: [YOUR BRAND].
  (Leave these blank and Claude will use a placeholder brand for the demo.)
- Generate Google Ads assets: 15 RSA headlines (<=30 chars), 5 long headlines (<=90),
  5 descriptions, plus a PMax-style set. Generate Meta assets: primary texts, headlines,
  descriptions.
- Generate the audiences: who to target, which signals, which lookalike/keyword seeds,
  drawn from the avatar.
- SCORE every asset against the ICP (1-5) on: does it use their words, does it lead with
  the outcome, does it pass the voice rules. Show the score next to each line. Cut anything
  under 4 and say why.
- Output campaign.html: a separate page with the scored copy grouped by platform and the
  audience plan.

Lead with the buyer, not the product. Outcomes over features. Profit over vanity. When
you're done, give me a 5-line summary and the two file paths.
```

---

## What "good" looks like

- The avatar is a **person you could call**, pulled from the data — not a demographic.
- The copy sounds like **the customer talking**, because the language came from them.
- Every asset has a **score and a reason**, so nothing ships on vibes.
- It's two clean pages you can hand to a client or drop into the ad platform.

This is the front half of the flywheel: research → scored copy → ships → the daily digest
(the other module) grades it → the results sharpen the next ICP.
