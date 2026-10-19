# Resume Playbook

A set of rules, templates, and two Claude Code skills for writing a one-page tech resume that gets
past a recruiter's 10-second scan and holds up in an interview.

The rules come from many review rounds, including peer resumes, external AI reviews, and feedback
from people who hire. Every rule is here because breaking it cost something.

## What's in here

| Path | What it is |
|---|---|
| [`RULES.md`](RULES.md) | The rulebook: bullet writing, bolding, layout, verification. Read this first. |
| [`templates/resume.tex`](templates/resume.tex) | One-page LaTeX template that already follows the rules. |
| [`templates/inventory.md`](templates/inventory.md) | Your fact sheet. Every number on your resume lives here first, with a tag. |
| [`templates/WORK_LOG.md`](templates/WORK_LOG.md) | Running log of what you build, filled in by `/resume-log`. |
| [`.claude/skills/make-resume/`](.claude/skills/make-resume/SKILL.md) | `/make-resume`: builds a tailored resume for a role type or a job posting. |
| [`.claude/skills/resume-log/`](.claude/skills/resume-log/SKILL.md) | `/resume-log`: after you finish work, records it with measured numbers so your resume never runs dry. |
| [`EXAMPLES.md`](EXAMPLES.md) | Before/after bullets showing each rule. |

## The 8 rules that matter most

1. **Specific but high level.** Each bullet says *what you built*, *the named tool*, and *the result*.
   A recruiter with no CS background should be able to repeat it back.
2. **Name things, skip internals.** "on the Google Vision API" is good. "using a partial unique index"
   loses the recruiter. Save the internals for the interview.
3. **Too vague is also wrong.** "Improved the booking system" says nothing. "Blocked overlapping
   bookings" says what it does.
4. **Bold the numbers only.** `\textbf{250+ students}`, `\textbf{40\%}`. Tool names stay plain,
   because they're already on the header's stack line. Never bold a whole clause, and never ship a
   resume with no bold at all.
5. **Tech stack goes on the header**, `Company | Python, FastAPI, PostgreSQL`, so the bullets can
   stay in plain words.
6. **Every number must survive "how did you measure that?"** Tag it `verified`, `estimate`, or
   `banned` in your inventory. Only `verified` numbers go in as-is. An `estimate` needs a hedge
   ("roughly", "~"), and `banned` never appears.
7. **Grounded beats dramatic.** "used weekly by 250+ students" beats "supporting 10,000
   concurrent users". Real usage beats capacity claims. Don't stack buzzwords.
8. **One page, filled.** A half-empty page reads as unfinished. One line per bullet by default.
   Two lines only when the second line carries a real number or ownership fact.

## Setup

1. Copy this repo into a folder for your resume (or fork it).
2. Fill in `templates/inventory.md` with your experience. Be honest: tag every number.
3. Open the folder in [Claude Code](https://claude.com/claude-code). The skills in `.claude/skills/`
   load automatically. To use them in every project instead, copy them into `~/.claude/skills/`.
4. Run `/make-resume swe`, or paste a job posting after `/make-resume`.
5. Compile with `pdflatex templates/resume.tex` (or Overleaf), then check it against
   the **Verification** list in `RULES.md`.

Keep `/resume-log` running from the projects you work on. When you finish something real, run it
and the work gets written down with measured numbers while you still remember the details. When
you apply next, the bullets are already there.

## Working without Claude Code

Everything works by hand too. `RULES.md` is the rulebook and `EXAMPLES.md` shows each rule in use,
so write bullets against them and check every one with the self-test at the bottom of `RULES.md`.
