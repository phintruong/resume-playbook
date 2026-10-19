---
name: make-resume
description: Generate a tailored one-page LaTeX resume from the inventory, either by role type (SWE, AI/ML, backend, fullstack, data) or by fitting a specific job description. Use when the user says /make-resume, "make my resume", "tailor my resume to this posting", or pastes a job description.
---

# Make Resume

This skill is the **workflow only**. Every rule lives in **`RULES.md`** and every fact lives in
**`templates/inventory.md`**. Read both in full before Step 1. If this file and `RULES.md` ever
seem to disagree, `RULES.md` wins.

## Core principles

1. **Specific but high level, in plain words.** A recruiter with limited technical background
   reads it first. Each bullet says what was built, the named tool, and the result. Name things,
   skip internals. Too vague is also wrong.
2. **Bold the numbers only.** Never tool names, never whole clauses, never zero bold.
3. **Tech stack on the org line** (`Company | stack`), so bullets stay plain.
4. **Every number must be defensible.** `verified` goes on the page as-is, `estimate` needs a
   hedge, `banned` never appears. Never invent a number, even if the user asks for one. Say no
   metric exists and offer a grounded outcome instead.
5. **Before→after beats bare %. Consequences beat inputs. Grounded beats dramatic.**
6. **One page, filled.** One line per bullet by default.

## Step 1: Determine the target

If the message names a role type or contains a job description, skip the question. Otherwise ask:

> Targeting a **role type** (`swe`, `ai`, `backend`, `fullstack`, `data`, or name one) or a
> **specific job posting** (paste it)?

## Step 2: Posting analysis (posting mode only)

Show this briefly before writing anything:
- **Requirements:** must-have / important / nice-to-have
- **Keywords:** every tool and method, the exact phrasing, and the repeated terms (ATS weight)
- **Closest role type**

## Step 3: Select and reframe bullets

Source everything from `templates/inventory.md`.

- **Role-type mode:** pick the most relevant entries and bullets.
- **Posting mode:** map each must-have to an inventory bullet, mirror the posting's words where
  true, make sure every must-have keyword appears once, and put the most relevant Skills row first.
- **Always:** apply `RULES.md` §2–3. Reword to emphasize different sides of the same work, but
  never add facts.
- **New facts from the user:** write them into the inventory first (with a tag), then use them.

## Step 4: Gap analysis

Show strengths / indirect matches / gaps and ask whether to adjust. A gap stays a gap. Only add a
skill the user confirms they can answer questions on.

## Step 5: Write the .tex

Copy `templates/resume.tex` to `resume_<type>.tex` or `resume_<company>.tex`. Follow `RULES.md` §4
exactly. Fill the page.

## Step 6: Compile

`pdflatex -interaction=nonstopmode <file>.tex`. Fix errors and retry until it compiles.

## Step 7: Verify (compiled ≠ correct)

Run `RULES.md` §7 in full: no `Overfull \hbox`, exactly one page, render the page and look at it
(bullets ≤ 2 lines, page filled, header on one line, numbers bold and tool names not), and grep for
banned words. Fix and recompile until everything passes. Then run the §8 self-test on every bullet.

## Step 8: Hand back

Give the PDF path and, for posting mode:
- **2–3 cover-letter hooks** using only `verified` numbers.
- **3–5 interview talking points.** For each bullet likely to be picked, the internals the user
  left off the page (from the inventory's interview notes), so they can answer "how?".
