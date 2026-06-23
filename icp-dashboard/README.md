# ICP Dashboard — turn customer research into scored ad copy

**Outcome:** your customer list becomes an ICP you can see, and that ICP becomes ad copy graded against your buyer before a single line ships.

This is the system behind ["Find your rich avatar"](https://www.nickbuilds.ai/blog/find-your-rich-avatar-matt-appsumo) and ["My GitHub is my marketing operating system"](https://www.nickbuilds.ai/blog/my-github-is-my-marketing-operating-system).

> There's no market. There's a person. At AppSumo, 10% of buyers drove about half the revenue. We named him "Marketing Agency Matt," built around him, and went from $7M to $90M. He was a real customer, not a made-up persona.

---

## The mesh

The work lives in folders, not in a chat window. This is the marketing operating system in miniature:

```
icp-dashboard/
├── skills/
│   ├── icp-synthesis/   # turn a raw customer list into a grounded ICP
│   └── ad-copy/         # turn the ICP into scored Google + Meta copy
├── voice/               # the non-negotiable voice rules every output passes through
├── dummy-data/          # fake but realistic customer data so the demo runs
│   ├── customers.csv        # the list: revenue, orders, title, company
│   ├── reviews.md           # verbatim review language
│   ├── support-tickets.md   # pains, in their words
│   └── sales-call-notes.md  # why they actually buy
└── example-output/      # a finished run, committed so you can see the deliverable
    ├── icp-dossier.html     # the ICP page
    └── campaign.html        # the scored PMax asset bundle
```

*"The memory stopped being about chat history. It became about disk state."* When the work is on disk, a new Claude Code session picks up exactly where the last one left off. The mesh is the value — not any single file.

---

## Run it (the demo)

The dummy data is already in `dummy-data/` — nothing to download. From this folder:

1. Open this folder in Claude Code (`claude` in your terminal, or the Claude Code extension).
2. Paste the prompt in [`BUILD-PROMPT.md`](BUILD-PROMPT.md) and hit enter.
3. Claude reads the data and the skills, then writes two pages into `example-output/`:
   - **`icp-dossier.html`** — the ICP page. The rich avatar up top, the segments below, a
     "their words" section of verbatim language, and the pains and desires. (Use the
     [`icp-synthesis`](skills/icp-synthesis/SKILL.md) skill.)
   - **`campaign.html`** — an example Google Ads campaign for that avatar: RSA/PMax copy and
     audiences, every asset scored 1–5 against the ICP, anything under 4 cut. (Use the
     [`ad-copy`](skills/ad-copy/SKILL.md) skill.)
4. Open the two HTML files in a browser. That's the deliverable.

Finished [`icp-dossier.html`](example-output/icp-dossier.html) and
[`campaign.html`](example-output/campaign.html) are both committed in `example-output/` so you
can see exactly what comes out before you run it. The campaign page is a full Google PMax
asset bundle (25 text assets + 12 image specs), every line scored against the ICP — modeled
on the real CXL bundles.

No real customer data needed. The included data is fake but shaped like a real export, with a
clear high-value segment (the agency owners) to find.

### What to look for when it runs
- The avatar comes from the **top ~10% by revenue** — the agency owners (Jordan, Marisol,
  Tomas), not the one-time buyers.
- The copy echoes the **verbatim language** ("lifetime deals are a cheat code for an agency"),
  not generic SaaS-speak.
- Rows with blank fields **stay blank** in the dossier. Empty beats hallucinated.

## The 7-step synthesis (what the skill does)

1. Pull the top ~10% by trailing revenue — your rich avatar lives here.
2. Enrich with public signals: title, company, industry.
3. Layer qualitative: support tickets, reviews, sales-call notes.
4. Synthesize the patterns with Claude.
5. Force exact language — keep grammar, slang, and phrasing intact. Do not paraphrase.
6. Cross-validate against real sales calls.
7. Compile into a `skills.md` that guides every future piece of copy.

Phone calls stay irreplaceable. AI tells you who to call, not what they'll say.

## Point it at your own data

Replace `dummy-data/customers.csv` with a real export (email + revenue is the minimum; name, company, and LinkedIn lift coverage a lot). The grounding rule is the whole game:

> The customer list is the only source of truth. If there's no real signal for a field, leave it blank. Empty cells beat hallucinated cells every time.
