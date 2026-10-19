# Resume Rules

One convention. If an old note, a template you found online, or a reviewer contradicts this file,
this file wins unless you decide to change it. When you change it, change the rule here, in the
section where it lives, and don't just append a note at the bottom. Rules that only live in an
appended log end up contradicting the sections above them.

---

## 1. Who reads it, and in what order

1. **ATS parser.** Needs plain text it can extract, standard section names, and no icon fonts,
   tables-as-layout, or images.
2. **Recruiter, about 10 seconds.** Often not an engineer. Reads the bold left column (companies),
   the dates, the first bullet of each entry, and anything bold.
3. **Engineer in the interview.** Picks one bullet and asks "how?". Every bullet must have a real
   answer behind it.

Write for #2 and make sure #3 has something to dig into.

## 2. Writing bullets

### Specific but high level

Each bullet answers three things:

- **What you built.** The product or feature, in words anyone understands.
- **With what.** The named tool, API, platform, or module (Stripe, Google Vision API, Socket.IO,
  Salesforce, university single sign-on).
- **What happened.** The result, preferably a number.

> Built a receipt scanner on the Google Vision API, cutting expense entry from **~10 minutes to
> under 1** for **3 student clubs**.

**Name things, skip internals.** Internals are interview material, not resume text. Keep these
off the page: partial unique index, idempotent, half-open interval, RLS, JWT, sharding key,
CUDA-to-HIP, memoization. Say what they *achieve*: "blocking double-booked slots", "requiring login
on every API", "every order goes to exactly one driver".

**Too vague is also wrong.** If a reader would ask "what module? how? with what?", the bullet is
too vague. "Improved the booking flow" fails. "Replaced a shared spreadsheet with an online booking
page for 40 tutors, blocking double-booked slots" passes.

### Word order

Default: `[Past-tense verb] [what] [with what], [result].` Lead with the outcome when the number is
the headline: `Cut month-end billing from 3 days to 4 hours by ...`. Either way, the reader
should hit the number before the line ends.

Start with a past-tense verb: Built, Shipped, Launched, Cut, Replaced, Automated, Led, Designed,
Integrated, Migrated, Owned.

### Numbers

- At least one number per bullet wherever a defensible one exists: users, time saved,
  before→after, %, money, scale.
- **Before→after beats a bare percentage.** "~30 to ~5 minutes" beats "83% faster".
- **Consequences beat inputs.** Users, time, money, and what broke without it are consequences.
  "8 modules", "12 endpoints", and "300 tests" are inputs. They're fine as context, but they can't
  carry a bullet alone.
- "by X%" for a change, "to X%" for a level.
- One bullet per entry may have no number if it shows a distinct capability (security, an
  integration, accessibility).

### Credibility

- **Grounded beats dramatic.** "used weekly by 250+ students across 4 courses" beats
  "supporting 10,000 concurrent users". Real usage beats a capacity guess.
- "92% accuracy on a held-out test split" beats "with 92% accuracy". Saying how you
  measured shows you understand measurement.
- No impossible or unexplained numbers ("reduced complexity by 80%"). Add how you measured it, or
  replace it with a grounded outcome.
- **Never on the page:** lines of code, commit counts, "sole developer", config counts dressed up
  as impact ("built a 46-category taxonomy"), "etc.", "we", slang, unexplained internal acronyms.
- If the work was AI-assisted, you still own what you specified, reviewed, and shipped. Don't
  claim you hand-wrote it, and don't undersell it either.

### Length

- **One physical line by default.**
- Two lines only when the second line carries a verified number, an adoption/ownership fact, or
  the thing that makes the result believable. Never two lines just for a tech list or adjectives.
- At most ~5 two-line bullets per resume, all on your top two entries. Never three lines.
- No em-dashes in bullet text. En-dash `--` is fine in date ranges.

### Order within an entry

The strongest, most *legible* bullet goes first. It's the only one guaranteed to be read.

## 3. Bolding

- **Bold the numbers.** `\textbf{250+ students}`, `\textbf{3 days to 4 hours}`,
  `\textbf{under a minute}`. Bold just the number phrase, not "by" or "to".
- **Tool names are never bold.** They're already on the header's stack line, and bolding them
  pulls the eye away from the results.
- One optional non-number bold: an ownership phrase on your lead bullet (e.g. `\textbf{sole engineer}`
  if it is literally true and you can defend it).
- Usually 1–3 bold spans per bullet, each ≤ 4 words. **Never bold a whole clause.**
- **Never ship a resume with zero inline bold.** A flat page gives the recruiter nothing to scan.

## 4. Layout

Use `templates/resume.tex`. Don't tweak spacing to squeeze content in. Cut content instead.

- **One page, filled.** A half-empty page reads as unfinished. Fill it with a fourth bullet on
  your lead role or another project, not padding.
- **Section order:** Education, Experience, Projects, Skills. Students put Education first, and
  many ATS checks expect it there.
- **Header:** name, then one line with phone | email | website | GitHub | LinkedIn. It must fit
  on one line. No address or city needed.
- **Experience entry:**
  ```latex
  \resumeSubheading
    {\href{https://company.com}{Company} $|$ \textnormal{\small Python, FastAPI, PostgreSQL}}{Jun 2026 -- Aug 2026}
    {Software Engineer Intern}{}
  ```
  Company first (recruiters scan company names, not repeated "Intern" titles). The tech stack sits
  on the org line, so bullets can stay plain. A non-technical role (club lead, founder) can skip
  the stack.
- **Project entry:** `Name (1st Place) [repo link] | stack` on line one, then event or context on
  line two. Always claim placements.
- **3–4 bullets per position**, at most 4. Projects get 1–3.
- Reverse chronological. Dates as `Mon Year -- Mon Year`, `Present` if ongoing.
- **Skills:** 3–4 rows (Languages / Frameworks / Data & Systems / Tools). Only list what you can
  answer questions on. For a specific posting, put the most relevant row first.
- **Never:** photos, date of birth, skill bars, self-rated levels, "references available".
  Leave the GPA off unless the application asks for it or it's strong.

## 5. Tailoring to a posting

1. Split the posting's requirements into must-have, important, and nice-to-have.
2. Map each must-have to a bullet from your inventory. Use the posting's exact words where they're
   true for you.
3. Every must-have keyword appears at least once (bullets or Skills).
4. Gaps are gaps. Don't add a skill you can't defend because the posting lists it.
5. Reword to highlight different sides of the same work. **Never invent facts or numbers.**

## 6. The inventory (source of truth)

All facts live in `templates/inventory.md`, never only in a `.tex`. Every number gets a tag:

- `<!-- verified -->`: measured, and you can say how. Goes on the page as-is.
- `<!-- estimate -->`: a reasonable estimate. Only with a hedge ("~", "roughly").
- `<!-- banned -->`: killed in a review, or not defensible. Kept in the file so it never comes back.

When you learn a new fact (new job, new number, new title), update the inventory first, then the
resume.

## 7. Verification (before you send any PDF)

1. Compiles with no errors, and the `.log` has no `Overfull \hbox`.
2. It's exactly one page.
3. Look at the rendered page: every bullet is 1–2 lines, the page is filled, the header is one line,
   every bullet has a bold number (or is the one allowed number-free bullet).
4. Grep for banned words: `sole developer`, `LOC`, `lines of code`, `commits`, `etc.`, ` we `,
   `—`, plus anything tagged `banned` in your inventory.
5. Read it as a recruiter: cover the Skills section and ask whether you'd still know what each job
   was.
6. Read it as an interviewer: for each number, can you answer "how did you measure that?" in one
   sentence?
7. Save the exact PDF you sent for each application. Don't regenerate it later and pretend it's the
   same file.

## 8. Self-test for one bullet

- [ ] Starts with a past-tense verb
- [ ] Says what was built in plain words
- [ ] Names the tool or approach, not its internals
- [ ] Has a number, and that number is bold
- [ ] No tool name is bold
- [ ] A non-engineer could repeat it back
- [ ] You could talk about it for five minutes in an interview
- [ ] Fits on one line (or earns the second line)
