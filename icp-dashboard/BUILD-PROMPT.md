# Build prompt — ICP to scored ad copy

Paste this into Claude Code with this folder open. It runs the two skills in order and
produces two pages you can open in a browser: the ICP dossier and an example campaign.

---

## The prompt

```
Read voice/voice-rules.md, skills/icp-synthesis/SKILL.md, and skills/ad-copy/SKILL.md in
full before doing anything. Then work in two passes against dummy-data/customers.csv.

PASS 1 — SYNTHESIZE THE ICP (use the icp-synthesis skill)
- Rank customers by trailing revenue. Isolate the top ~10%: that cohort is the rich avatar.
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
- Pick the rich avatar as the target and one landing page outcome.
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
