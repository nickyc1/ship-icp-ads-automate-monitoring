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
├── dummy-data/          # a fake customer list so the demo runs
└── example-output/      # what a finished run looks like
```

*"The memory stopped being about chat history. It became about disk state."* When the work is on disk, a new Claude Code session picks up exactly where the last one left off. The mesh is the value — not any single file.

---

## Run it (the demo)

1. In Claude Code, open this folder.
2. Drop your customer export into `dummy-data/` (or use the included `customers.csv`).
3. Paste [`BUILD-PROMPT.md`](BUILD-PROMPT.md). Claude will:
   - **Synthesize the ICP** from the list using the [`icp-synthesis`](skills/icp-synthesis/SKILL.md) skill — find the rich avatar, the segments, the exact language.
   - **Build an ICP page** — a single HTML dossier you can open: who they are, what they want, the words they use.
   - **Build an example Google Ads campaign** — RSA/PMax copy and audiences on a separate page, every asset scored against the ICP using the [`ad-copy`](skills/ad-copy/SKILL.md) skill.

No real customer data required to follow along. The included list is fake but shaped like a real export, with a clear high-value segment to find.

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
