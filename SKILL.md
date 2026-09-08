---
name: write-spec-template
description: Hand over a blank, ready-to-fill PRD template plus the questions and quality bar behind it — for when the user wants to write the PRD themselves rather than have AI draft it. Use when the user asks for "just the template", "a PRD template I can fill in", "the framework, not the draft", wants to write the first draft themselves and get direction rather than content, or explicitly invokes /write-spec-template. Do not draft the user's actual problem statement, metrics, or content — this skill provides structure and prompts only.
argument-hint: "[optional: feature or problem name, for the header only]"
---

# Write Spec — Template

Give the user the scaffolding to write their own PRD. This is the opposite job to `write-spec`: that skill drafts the content for the user; this one deliberately does not. If the user starts dictating actual problem content and asking you to write it into the sections, that is a **write-spec** request — say so and offer to switch, rather than quietly drafting here.

## When to use this vs. write-spec

- User says "just give me a template," "I want to write this myself," "what's the framework," "I don't want AI writing my PRD, just structure" → **this skill**.
- User gives you a feature idea and wants a written draft → **write-spec**.
- User pastes a finished or partial PRD and wants feedback → **write-spec-evaluator**.

If ambiguous, ask: "Do you want me to draft this with you, or hand you the blank template to fill in yourself?"

## Output

Produce two things, in this order:

### 1. The blank template

The 14-section structure below, as literal fill-in-the-blank markdown — headers, the one-line guidance under each header, and an empty line (or a bracketed prompt like `[ ]`) for the user to write into. Do not pre-fill any section with example content about their actual feature. If they gave a feature name in `$ARGUMENTS`, use it only in the document title — not inside any section.

```markdown
# PRD: [Feature name]

## 1. One-line summary
_What we are doing and for whom, in a sentence a salesperson could repeat._


## 2. Why now
_The business context. What changed to make this the right quarter._


## 3. The problem
_Specific, measured, sourced. No feature names._


## 4. Who has it
_The persona, and the evidence. Mark assumptions as assumptions._


## 5. Success metrics
_Name, baseline, target, timeframe. Plus how the target was derived._


## 6. Guardrail metrics
_What must not get worse while we chase the above._


## 7. Solution and user flow
_High level. The perimeter, not the pixels._


## 8. Must-haves
_Login, permissions, security, compliance. Do not assume people know._


## 9. Non-goals
_What we are explicitly not doing this time, and why._


## 10. Failure modes and edge cases
_What happens when it breaks, when data is missing, when the model is wrong._


## 11. Risks, from the pre-mortem
_Five reasons this failed, and the mitigation for each._


## 12. Timeline and dependencies
_Written with engineering. Never quoted before that conversation._


## 13. Open questions
_The honest list. This section proves the document is alive._


## 14. Decision log
_What we changed, when, and what we learned that caused it._
```

Deliver this as a markdown artifact/file the user can copy into their own doc tool, not just inline chat text — they're going to be writing into it over days, not reading it once.

### 2. The prompts to work from

Right after the template, give the user the thinking tools to fill it in themselves — not the content, the questions:

**Before you write anything**, work through the six-step process this template comes from. Writing (Section 1–14) is the fast, small step — most of the real work happens before it:

| Step | Time | Do this before writing |
|---|---|---|
| Immerse | weeks | Talk to users, read support tickets, watch the data |
| Frame | days | Turn what you learned into a sharp problem statement |
| Explore | days | Look at more than one solution before committing |
| Align | days | Get engineering, design, and stakeholders on the same page |
| Narrate | hours | *This is when you fill in the template* |
| Evolve | forever | Update Section 14 as reality corrects the plan |

**The five questions to answer before you start filling in sections** (each maps to specific sections above):

1. Why does this problem matter, to users and to the business? → Sections 2, 3
2. Who has this problem, and how do we know? → Section 4. If the honest answer is "we assume," write the word *assumption*.
3. What does success look like, in numbers? → Sections 5, 6
4. How will we solve this: scope, non-goals, user flow? → Sections 7, 8, 9
5. When will we deliver, and what are the risks? → Sections 10, 11, 12

**Check your problem statement (Section 3) against this before moving on** — a weak Section 3 undermines everything after it:

| The statement | Verdict |
|---|---|
| "We need to add a search feature to the dashboard." | No — a solution wearing a problem's clothes |
| "Forty percent of users abandon onboarding. They cannot find value in the first three minutes." | Yes — specific, measured, names what's happening to a person |
| "We need to improve the checkout flow." | Half — improve what, and why? A location, not a problem |
| "Enterprise customers lose six hours a week reconciling data across three tools." | Yes — specific, quantified, sourced |
| "Our NPS is 23 and declining. We should redesign the UI." | Half — real number, then jumps straight to a solution |

**Before you call it done, check for these seven habits** — they are what separate a real PRD from a filled-in template:

1. Solution as problem (Section 3 names a feature instead of a problem)
2. Template filling (words in every section, but no real thought)
3. Over-specification (Section 7 defines pixels instead of perimeter)
4. Solo authoring (nobody but you has seen this before it's "done")
5. Vague metrics (Section 5/6 missing a baseline, target, or timeframe)
6. Happy path only (Section 10 is thin or missing)
7. Missing non-goals (Section 9 is empty)

When the user has a full or partial draft and wants it scored against this list rather than just reminded of it, point them to **write-spec-evaluator**.

## Tips

- Stay hands-off on content. If the user asks "what should I put for the problem statement," turn it back into a question ("what's the specific, measured effect you're seeing, and on whom?") rather than proposing wording for their actual feature — that crosses into write-spec territory.
- It's fine to explain *why* a section exists or give a generic, non-feature-specific example (as in the tables above) — the line is between illustrating the pattern and writing their content.
- If they ask you to fill in more than the title, confirm they want to switch to write-spec before doing it.
