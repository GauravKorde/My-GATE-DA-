# AI Tracker Maintenance Rules

> These rules define how I (the AI) update the progress tracker and session files.
> Hard-coded behavior — I follow these every interaction without being reminded.

---

## Rule 1: When I Update

| Trigger | Action |
|---|---|
| **I create a new session file** | Immediately update progress tracker — set topic from `[ ]` → `[📄]`, add buffer |
| **You say "done session-X"** | Mark topic `✅`, fill Actual Finish date, ask for problems count + confidence score |
| **You report weak / wrong answer** | Immediately add entry to Weak Topics Register |
| **Every Sunday (week end)** | Prompt for weekly review — ask problems solved, avg confidence, carry-forward |
| **You ask "where am I?"** | Show current standing summary from tracker |

---

## Rule 2: Status Logic

| Status | Meaning | When I Set It |
|---|---|---|
| `[ ]` | Nothing written, nothing studied | Default — topic is in future |
| `[📄]` | Documentary exists, scheduled start not reached | Right after I create a session whose expected start > today |
| `[~]` | Within study window, not yet confirmed done | When today falls between expected start and finish, but you haven't said "done" |
| `✅` | Studied + practiced + confirmed | Only after you explicitly say "done session-X" or "mark this complete" |
| `[-]` | Skipped | Only if you explicitly say "skip this" |

**Critically:** I never mark `✅` just because the file exists. Only your explicit confirmation counts.

---

## Rule 3: Buffer Calculation

Two separate buffers tracked:

**Content Buffer** = Days of pre-written docs beyond today's schedule
- When I write a session whose expected start is D days from now, content buffer increases
- Formula: `(furthest scheduled date with [📄] doc) - (today)`
- Max possible: I can write sessions far ahead, but study schedule is fixed

**Study Buffer** = Days where you finished a topic before its expected finish date
- When you mark a session `✅` before its expected finish, study buffer increases
- When you finish after expected finish, study buffer decreases
- Formula: `sum of (expected finish - actual finish) across completed topics`

Display format: `Content: +X days 🟢` / `Study: +Y days 🟡`

**Initial state (Jun 13):** Content = +13, Study = 0

---

## Rule 4: When I Create a New Session

Every session file I write must include this header (inserted right after the title):

```
> **📅 Expected:** Jun 26 – Jun 27 | **Buffer:** +13 days 🟢 | **Status:** 📄 Doc ready
```

Then update the progress tracker:
- Change the topic's Status from `[ ]` to `[📄]`
- Add expected start/finish dates if not already present
- Recalculate content buffer

---

## Rule 5: When You Say "Done Session-X"

I will:
1. Change topic status from `[📄]` / `[~]` to `✅`
2. Fill **Actual Finish** with today's date
3. **Ask you two questions:**
   - "Problems solved for this topic?"
   - "Confidence level (1-5)?"
4. Fill **Problems** and **Conf** columns
5. If Confidence ≤ 2: auto-add to Weak Topics Register
6. Recalculate study buffer

---

## Rule 6: Weekly Review Prompt

Every Sunday (or first interaction after Sunday), I'll say:

> **Weekly review time.** Number of problems solved this week? Average confidence? Any concepts that need carry-forward to next week?

Then I fill the Weekly Review Log row.

---

## Rule 7: Weak Topics Register

Entries added when:
- You explicitly tell me a concept is weak
- Confidence ≤ 2 on a completed session
- You get a PYQ/mock question wrong and flag it

Format I use:
```
| # | Date | Topic | Specific Concept | Resolved? |
|---|------|-------|-----------------|-----------|
| 1 | Jun 20 | Bayes' Theorem | Law of total prob. derivation | ☐ |
```

I keep unresolved items at the top. When you say "resolved," I mark ☑.

---

## Rule 8: General Aptitude Tracking

Every day when we interact, I check the GA tracker. If today's checkbox is empty, I remind:
> "GA checkbox for today is still open — 45 min."

This is the most-skipped subject. Nagging is intentional.

---

## Rule 9: Schedule Recalculation

If you fall ≥ 5 days behind on study buffer (study buffer ≤ -5), I will:
1. Propose a revised schedule with compressed timelines
2. Move buffer time from low-priority topics (Aptitude, DBMS) to high-priority (ML, Prob, LA)
3. Never suggest skipping derivations — depth stays same, scope adjusts

---

## Quick Reference: Session Header Template

```markdown
# Session 00X — Topic Name

> **📅 Expected:** Mon DD – Mon DD | **Buffer:** +X days 🟢 | **Status:** 📄 Doc ready
```

When you complete it:
```markdown
> **📅 Expected:** Mon DD – Mon DD | **Buffer:** +X days 🟢 | **Status:** ✅ Completed
```
