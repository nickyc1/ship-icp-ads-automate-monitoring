---
name: icp-synthesis
description: Turn a raw customer list (email + revenue at minimum) into a grounded ICP — the rich avatar, the segments, and the exact language they use. Use before writing any ad copy.
type: skill
---

# ICP Synthesis

You turn a customer list into an ICP that is real enough to write copy from. Not a
demographic, not a stock persona. A specific person you could call, pulled out of the data.

## The core rule

The customer list is the **only** source of truth. Company name, job title, buyer
description, the words they use — every field must be grounded in a real signal from the
data or enrichment. If there is no signal, leave it blank. **Empty cells beat hallucinated
cells every time.** A confident guess that's wrong poisons every piece of copy downstream.

## Step 1 — Find the rich avatar

Rank by trailing revenue. The top ~10% is where your avatar lives. At AppSumo, 10% of
buyers drove about half the revenue; the other 90% bought once and left. Building around
that 10% took the business from $7M to $90M.

Look at what the top cohort has in common: the same job, the same business model, the same
reason for buying again and again. Name them. "Marketing Agency Matt" was a one-person
agency serving 5 to 20 clients, buying 2 to 3 deals a month for years, because *"lifetime
deals are a cheat code for an agency. Overhead kills agencies."* He was punching way above
his weight, and that was the whole point.

Codie Sanchez: *"Every single business has a rich avatar."* Your job is to find yours, not
invent one.

## Step 2 — Map the segments below the avatar

The avatar isn't the only buyer, just the most valuable. Identify the other distinct
groups: who they are, what they buy, where they fall short of the avatar. This keeps you
honest about who you're choosing to ignore.

## Step 3 — Enrich with public signals

For each high-value record, add what's verifiable: title, company, company size, industry.
Public, checkable, grounded. Tier your confidence — full CRM data beats a LinkedIn guess
beats a pattern-match. Mark which tier each field came from.

## Step 4 — Layer the qualitative

Numbers tell you who. Words tell you why. Pull from support tickets, reviews, NPS
verbatims, and especially recorded sales calls. This is where the buying motivation and
the real objections live.

## Step 5 — Keep their exact language

When you capture how a customer talks, **keep grammar, slang, and phrasing intact.** Do not
clean it up. Do not paraphrase. The moment you smooth "saving money AND making money on the
same tools" into "cost-effective multi-tool value," you've thrown away the only thing that
makes the copy convert. People buy words that sound like their own thoughts.

## Step 6 — Cross-validate

Check the synthesized avatar against real sales calls. Does the person on the call match
the person on the page? If not, the data lied to you somewhere. Phone calls stay
irreplaceable — AI tells you who to call, not what they'll say.

## Step 7 — Compile into a reusable profile

Write the result to disk as a skills file the ad-copy skill (and every future session)
loads on every run. The synthesis is only valuable if it persists and compounds. The mesh
is the value, not any single output.

## Output

A single ICP dossier (one page): the avatar at the top, the segments below, a "their words"
section of verbatim language, and the likely pains and desires — each grounded, each
traceable to a signal in the data.
