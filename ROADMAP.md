# Roadmap — planned, not built

Agreed but deliberately unbuilt. Nothing here gets built without checking with
Abhinandan first. `CLAUDE.md` records what *is* built.

---

## 1. The log — a dated stream of shipped work and learning

**Decided:** a short growth log on the site. **No blog** — see "Why no blog".

### The idea

The page is already about data arriving on time, in order, appended as it
comes. The log is that idea turned on himself: an append-only stream of what he
shipped and what he learned, newest first. It is not a "Blog" tab; it is the
site's own metaphor applied to a career.

The existing two-accent system covers it with no additions:
**teal = shipped** (it worked, same meaning as `.outcome`),
**tangerine = learning** (in motion, same meaning as attention).

### What it is for

Proof of momentum. Abhinandan wants to read as energetic and growing — but an
adjective on a page is a claim, and a timestamped trail is evidence. Eighteen
dated entries across eight months say it; the word "workaholic" does not, and
in a hiring context that word reads as burnout risk rather than dedication.
**Show the trail, drop the adjective.**

### Shape

- Rail label `LOG`. Section heading in the established voice, not "Blog".
- Each entry: a month-level date in mono muted type, a kind tag
  (`SHIPPED` / `LEARNED` / `SHIPPING`), and one to three lines of prose.
- Month granularity, not exact dates — honest, and ages more gracefully.
- Newest first. Show the most recent 6–8 only. No pagination, no archive.
- Plain markup inline in `index.html`, roughly 15 lines an entry. **No build
  step, no JS, no data file** — the single-file rule holds.

### Placement — deliberately not at the top

Goes **after Work, before Credentials.** Two reasons. The case studies are the
substance and should not be pushed down by a list of small entries. And a log
placed low does less damage on the day it goes stale.

### The staleness rules — the important part

A neglected log is the one thing here that can actively hurt him, so the
defences are part of the design, not an afterthought:

- **No auto "last updated" stamp.** It converts silence into a visible
  accusation. Month-level entry dates only.
- **Seed with 5–6 entries before it ever ships.** A log with one entry looks
  worse than no log. Backfill honestly from the last six months — the
  Databricks certification, the Snowflake/dbt KPI work starting, the Coursera
  generative-AI track, this site going live.
- **Realistic cadence is one entry every two or three weeks**, not weekly.
  A bar he clears is worth more than one he defaults on.
- **Exit condition: if four months pass with no new entry, remove the section.**
  Reverting to no log is neutral; leaving a visibly abandoned one is not. This
  is the rule most people never write down, which is why so many portfolios
  carry a dead blog. Any future session that notices the gap should raise it.

### Why no blog

Considered and rejected for now, on his own call. He has not written any posts
yet, and a blog with three posts and an eight-month gap is worse than no blog —
it reads as started-and-quit, the exact opposite of the intended impression.
Building the section will not create the habit; the habit has to come first.

**Revisit only if** two or three posts exist in draft and have survived a busy
month. At that point the cheap route is publishing where readers already are —
LinkedIn — and keeping a short "Writing" list on the site that links out. A
post on a personal domain gets almost no readers. That keeps the no-build-step
rule intact either way.

### Not on the page

"Easy to adapt in culture" and similar cannot be asserted — a page claiming it
achieves the opposite. It is already demonstrated: the case studies were
rewritten to drop internal shorthand so HR could read them, and that instinct
for translating to an audience is the culture signal, working silently.
