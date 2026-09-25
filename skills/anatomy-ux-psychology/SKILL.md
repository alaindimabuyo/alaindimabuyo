---
name: anatomy-ux-psychology
description: Use when designing, writing, auditing, or rebuilding a SaaS flow where the user must decide or act (forms, booking or search screens, signup, onboarding checklists, free-tool results gated behind signup, upgrade prompts, paywalls, add-on or upsell offers, checkout), when a flow converts or retains poorly, or when someone asks to "make it more persuasive" or apply defaults, endowed progress, reciprocity, IKEA/endowment effect, loss aversion, or anchoring. Applies even if the user only says "people drop off at step two".
---

# Anatomy: UX Psychology

Six principles decide whether a user acts or leaves. Each one works because it matches how people actually decide, and each one becomes a dark pattern when the fact behind it is false. This skill applies them honestly and cites the research correctly.

## Using this in any project
- **With a codebase:** read the real flow first: the form fields and their current defaults, the onboarding steps the product actually records, what the free plan really does at its limit (blocks, hides, or deletes), and the real prices. Search by content ("onboarding", "checklist", "paywall", "upgrade", "limit") instead of assuming a folder layout.
- **Without a codebase:** the owner's description is the only source of product facts. A feature they did not name does not exist.
- **Output format:** screen copy and a behavior spec per screen, in the project's framework if one is named.

## Shared rules (same in all anatomy-* skills)
- Never invent facts, pages, customers, features, or claims. Use `[NEEDS: ...]` placeholders and list them at the end.
- Keep facts identical across the site.
- When the owner's request conflicts with this skill, build the skill's version and output a "Changed from the request" table: asked for, built, why. Do not drop a request silently.

This skill adds two rules.

**1. The psychology is applied to true facts only.** A default must be the real most common choice (or the documented safest one). A progress head start must be a step the user really finished. A loss must be a loss the product really causes, with the real deadline. A comparison price must be a real price on the same screen. If the true fact is not known, write `[NEEDS: ...]`, do not assume it.

**2. Cite only the evidence table below.** Use its figures and attributions exactly. Do not add statistics from memory, blog posts, or videos ("70 to 90% never change defaults", "samples raise sales 2,000%", "reciprocity is the most powerful driver"); these are unsourced. For the team, cite the effect, not a promised lift for this product: no study predicts this product's conversion.

## The six principles

| # | Principle | Use it on | Honest version | Becomes a dark pattern when |
|---|---|---|---|---|
| 1 | **Smart defaults** | Forms, search, booking, settings | Pre-select the most common or safest value; label the result ("12 results for these dates") | The default favors the business against the user: pre-ticked paid extras (banned for EU consumers, Consumer Rights Directive Art. 22), pre-ticked marketing opt-ins (not valid GDPR consent) |
| 2 | **Endowed progress / goal gradient** | Onboarding, profile setup, checklists | Count steps the user really did (account created, email verified) as step 1; show "2 of 6 done", never 0% | The bar starts at a number no real step earned ("start at 40%") |
| 3 | **Reciprocity (give first)** | Free tools, reports, trials, calculators | Show a genuinely useful partial result, then offer to save or extend it | The "free" part is useless without signup, or the result is blurred and held hostage |
| 4 | **IKEA / endowment effect** | Signup, first run, templates | Let the user make real choices (name, template, settings, first item) before the account wall; keep what they made after signup | Their work is deleted, or held back, to force payment |
| 5 | **Loss aversion (loss framing)** | Upgrade prompts, limits, expiring trials | Name what the user will really lose, by name and with the real date ("3 projects become read-only on 12 Oct") | The loss, countdown, or deadline is invented, or the decline button shames ("I'll risk it", "No, I like losing work") |
| 6 | **Contrast / anchoring** | Add-ons, upsells, plan tables | Show the offer next to the real, related price the user just saw ("adds 2.6% to your $1,900 order") | The anchor is a fake "was" price or a decoy plan that no one can buy |

**Decline controls stay neutral:** "Not now", "No thanks", "Keep Free plan". Honest loss framing belongs in the body copy, never in the dismiss button. False countdowns and confirmshaming are named deceptive patterns (FTC, "Bringing Dark Patterns to Light", 2022; EU DSA Art. 25; EU Unfair Commercial Practices Directive for false urgency).

## Evidence table (cite exactly this)

| Effect | Study | What it found | Caveat to state |
|---|---|---|---|
| Choice overload | Iyengar & Lepper, 2000 (jam tasting booth) | Of shoppers who stopped, ~30% bought with 6 jams vs ~3% with 24 | Replications are mixed; a 2010 meta-analysis (Scheibehenne et al.) found an average effect near zero. Use it as "fewer decisions help", not as a fixed number |
| Defaults | Johnson & Goldstein, 2003 (organ donation) | Opt-out countries had far higher consent than opt-in countries | Strong for low-effort choices; no single "% keep defaults" figure for products |
| Endowed progress | Nunes & Drèze, 2006 (car wash cards) | 8-stamp blank card: 19% completed; 10-stamp card with 2 pre-filled: 34% | The 2 stamps were given, but disclosed; users were not misled about how many washes remained |
| Goal gradient | Kivetz, Urminsky & Zheng, 2006 (coffee cards) | Customers bought coffee more often as they got closer to the free reward | |
| Reciprocity | Cialdini, *Influence* (1984) | Receiving something first creates a felt obligation to return it | Do not rank it "the most powerful driver"; the book does not say that |
| IKEA effect | Norton, Mochon & Ariely, 2012 | People valued items they assembled more than identical pre-built items | Only when the task was completed; failed builds lost the effect |
| Endowment effect | Kahneman, Knetsch & Thaler, 1990 (mugs) | Owners asked roughly twice what buyers would pay | |
| Loss aversion | Kahneman & Tversky, 1979 (prospect theory) | Losses weigh about twice as much as equal gains | This is loss aversion, not "status quo bias" (a related, separate effect) |
| Contrast / anchoring | Tversky & Kahneman, 1974 | Judgments shift toward a number seen just before | |

## Step 1: Map the decision points
For each screen in the flow, list: what the user must decide, how many fields or choices, what they get before they give anything, and the exit option. Output a table (screen, decisions, value given first, exit copy, principle to apply).

## Step 2: Apply the principles
Per screen, choose only the principles that fit (usually 1 or 2). Check each against rule 1: state the true fact it rests on, or `[NEEDS: ...]`.

## Step 3: Output
- Decision-point table (Step 1)
- Before/after per screen: current copy and layout, new copy and layout, principle, true fact it rests on, study from the evidence table
- "Changed from the request" table for every dark-pattern request replaced by the honest version
- Metric to watch per change (completion rate, drop-off step, upgrade rate, refund or complaint rate) and a suggestion to A/B test; no promised lift
- `[NEEDS: ...]` list

## Auditing an existing flow
Report pass/fail with the fix for each:
1. Forms pre-fill the common or safest value; no pre-ticked paid extras or opt-ins
2. Onboarding progress never starts at 0% and never starts above the real steps done
3. Free results or tools give real value before any account wall
4. Users make something of their own before signup, and it survives signup
5. Upgrade prompts name the real loss and real date; no invented countdown
6. Decline buttons are neutral; no confirmshaming
7. Add-on and upsell prices appear next to a real related price, never alone; no fake "was" prices
8. Each screen asks for no more decisions than it needs
9. Every stat in copy or internal docs is in the evidence table with its caveat
