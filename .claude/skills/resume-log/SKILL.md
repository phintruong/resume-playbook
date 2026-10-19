---
name: resume-log
description: Record work just finished into WORK_LOG.md with measured, tagged numbers so it can become resume bullets later. Invoke after finishing a task, a feature, a merge, or a session ("/resume-log", "log this for my resume", "update my resume info").
---

# resume-log

Appends the work just finished to `WORK_LOG.md` (copied from `templates/WORK_LOG.md` in the
resume repo), refreshes its metrics, and keeps every number defensible in an interview.

**The log is the product.** It is not a diary or a changelog. It is the place work facts enter the
resume pipeline, and `inventory.md` and `/make-resume` draw from it. Six months from now it should
let you rebuild any story for an interview without opening the repo.

## Non-negotiables

1. **Append, never rewrite.** Fix an earlier entry with a new entry that says what changed.
2. **Every number gets a tag:** `verified` / `estimate` / `banned`, plus one line on how it was
   measured. An untagged number is a bug.
3. **Measure, don't estimate.** Run a command, read a dashboard, check the database. Don't carry a
   number over from memory, an old entry, or what an AI agent reported. If you can't measure it,
   tag it `estimate` and write the hedge.
4. **Attribute honestly.** Only count your own commits (`--author=<your git name>`). Label team
   totals as team totals. AI-built work you specified, reviewed, and merged is yours, but describe
   it as directing and reviewing, not hand-writing.
5. **No confidential data.** No customer names, addresses, real records, secrets, or anything under
   NDA. Describe the client generically ("a landscaping company") unless you have permission.
6. **The ban list is enforced.** Lines of code, commit counts, "sole developer", and config counts
   as impact ("46 categories") never become bullets. If the work only produced those, say so and
   write no bullet.

## Steps

### 1. Find the delta

Read the **Sync markers** table in `WORK_LOG.md`, then for each repo listed:

```bash
git -C <repo> log --all --author="<your git name>" --date=short \
  --pretty='%ad|%h|%s' <last-logged-sha>..HEAD | grep -v '|Merge '
```

If the SHA is gone (rebased or re-cloned), use `--since=<last synced date>` and note the fallback.
Work done in this conversation but not committed yet still counts; mark it `uncommitted` so the
next run doesn't count it twice.

### 2. Decide the tier

Most work is tier 1, and that's fine.

- **Tier 1, log only.** Bug fixes, copy changes, lint, test repairs, CI fixes. One line, no
  bullet.
- **Tier 2, log and re-measure.** A shipped feature, a new API, a migration, a new integration.
  Append and refresh the Metrics table.
- **Tier 3, log, re-measure, and propose a bullet.** A new capability, a hard problem solved, a
  production incident with a real story, or **any real-world consequence number** (users, time
  saved, money, adoption). A consequence number is always tier 3, and it's worth more than
  anything else this skill records.

### 3. Re-measure (tier 2 and 3)

Re-run whatever produces each Metrics row (analytics query, test count, timing, git command) and
update it. Never edit a number without re-running its method. If a number moved, check whether a
bullet candidate quotes the old one. A stale number in a bullet is worse than no bullet.

### 4. Write the entry

Add it to the top of **Entries**:

```markdown
### YYYY-MM-DD: <what shipped, not what you did all day>

<2–5 sentences: what it was, why it was hard or mattered, what it now does.>

**Tier:** 1 / 2 / 3
**Numbers:** <each with a tag, or "none">
**Bullet candidate:** <tier 3 only, or "none">
```

A tier-3 bullet candidate follows `RULES.md`: specific but high level, named tool, plain words,
numbers bold, tool names not bold, one line. Put the internals you left out under the entry as
interview notes. Add the bullet to **Bullet candidates**.

Update **Last synced** and every **Sync marker** to the current HEAD on every run, tier 1
included, or the next run re-reads work already logged:

```bash
git -C <repo> rev-parse --abbrev-ref HEAD; git -C <repo> rev-parse --short HEAD
```

### 5. Sync to the inventory (tier 3, only when asked)

Ask before touching `inventory.md`. If yes, add or update the entry, copy only `verified` numbers
(keeping their tags), and carry `banned` numbers across as `<!-- banned -->` so they can't come
back.

### 6. Report

Three lines: the tier, what was logged, and whether any metric moved. If the work still has no
real-world consequence number (users, time, money), say so once and suggest how to get one.

## When nothing is worth logging

Say so and write nothing. Padding the log with "fixed a typo" makes the real work harder to find.
