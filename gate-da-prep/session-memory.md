# Session Memory — GATE DA 2027

> **Purpose:** Any AI (opencode, Antigravity 2.0, or future agents) reads this file to continue the conversation seamlessly. Updated after every significant action.
>
> **File is maintained by the AI.** Outdated info gets compressed or removed to save context.
>
> **Last updated by:** opencode — Jun 13, 2026
> **Agent identity:** Every update must note which agent made the change (opencode, Antigravity 2.0, etc.)

---

## 1. STATIC CONTEXT (Permanent)

### User Profile
| Field | Value |
|---|---|
| Name | Gaurav |
| Background | Final year Engineering, strong Mathematics |
| Study hours | 6+ hrs/day dedicated |
| Target | **IISc Bangalore 835+** (primary), IIT Hyderabad 640+ (secondary) |
| Exam | GATE DA 2027 (~Feb 2027) |
| Vault path | `C:\Users\HP\Desktop\gate - Copy\gate-da-prep\` |

### Teaching Style (Mandatory — Never Deviate)
- **Documentary narrative** — each chapter builds like a story
- **First-principles derivations** — every formula derived, never stated
- **Conversational tone** — "you", "we", short sentences, physical analogies, no academic/ passive voice
- **Full algebra shown** — no skipped steps, every manipulation explained
- **Verification checks** — `✅` after every derivation
- **Boxed formulas** — `\boxed{}` for key results
- **"Understanding the formula"** sections after each derivation
- **One distribution per session file**
- **Collapsible content** via Obsidian `> [!success]-` / `> [!info]-` callouts, never HTML `<details>`
- **No emojis** unless user explicitly requests
- **Charts**: matplotlib-generated PNGs in `assets/`, embedded via `![[path.png]]`

### Repo Structure
```
gate-da-prep/
├── 01-probability-and-stats/   ← Current phase
├── 02-linear-algebra/
├── 03-calculus-optimization/
├── 04-programming-dsa/
├── 05-dbms-warehousing/
├── 06-machine-learning/
├── 07-artificial-intelligence/
├── 08-general-aptitude/
├── assets/                     ← matplotlib charts (PNG)
├── progress-tracker.md         ← Full timeline + buffer + confidence + problem tracking
├── session-rulebook.md         ← Style guide reference
├── tracker-rules.md            ← AI maintenance rules (9 rules)
├── session-memory.md           ← THIS FILE
└── README.md
```

### File Naming
- Session files: `session-XXX.md` (e.g., `session-006.md`)
- Session header template:
  ```
  > **📅 Expected:** Mon DD – Mon DD | **Buffer:** +X days 🟢 | **Status:** 📄 Doc ready
  ```

### Key Decisions Made (Historical — Do Not Change)
1. **Documentary style** adopted as permanent teaching method (rejected academic/bookish language)
2. **One distribution per file** — Poisson in session-004, Exponential in session-005, Normal in session-006
3. **Python + matplotlib** for charts (not ASCII art or Mermaid for statistical graphics)
4. **doubts-solved.md** created for deep-dive concept explanations outside session flow
5. **Two-bucket system** (LAZY/ACTIVE) for energy-based topic selection
6. **Progress tracker rewritten** 3 times — final version has confidence (1-5), problem counts, weak topics register, weekly review, GA daily checkboxes, interleaved revision

---

## 2. DYNAMIC STATE (Updates After Every Action)

### Current Standing
| Metric | Value |
|---|---|
| **Date** | Jun 13, 2026 |
| **Phase** | 1 — Probability & Statistics (Day 1 of 30) |
| **Content buffer** | +13 days 🟢 (docs written through Jun 28) |
| **Study buffer** | 0 days (on pace with schedule) |
| **Done** | Sessions 001-005 written (docs exist) |
| **Study confirmed ✅** | Topic 1 (Counting) — user confirmed done |
| **In study window [~]** | Topic 2 (Axioms) — Jun 15-17 |
| **Doc ready [📄]** | Topics 3-5 (Bayes thru Continuous) — written, awaiting scheduled dates |
| **Not started [ ]** | Topics 6-8 (Descriptive Stats thru Hypothesis Testing) |

### Sessions Status
| Session | Topic | Expected | Buffer | Status |
|---|---|---|---|---|
| 001 | Counting, Axioms, Events | Jun 13-17 | +13 | ✅ Completed |
| 002 | Bayes, Conditional Expectation | Jun 18-20 | +13 | 📄 Doc ready |
| 002b | Variance Mastery (35 problems) | Jun 18-20 | +13 | 📄 Doc ready |
| 003 | RVs, Bernoulli, Binomial, Uniform | Jun 21-24 | +13 | 📄 Doc ready |
| 004 | Poisson Distribution | Jun 21-24 | +13 | 📄 Doc ready |
| 005 | Exponential Distribution | Jun 25-28 | +13 | 📄 Doc ready |
| 006 | Normal Distribution | Jun 26-27 | 🔜 | Not written |
| 007 | Standard Normal | Jun 27-28 | 🔜 | Not written |
| 008 | t-dist, Chi-squared | Jun 28 | 🔜 | Not written |

### Next Actions
1. **Next doc to write:** Session 006 — Normal distribution (due Jun 26)
2. **Next user action:** User will read sessions and say "done session-X" to mark complete
3. **Next weekly review:** Sunday Jun 14-19 (prompt user)

### GA Tracker
| Week | M | T | W | T | F | S | S | % |
|---|---|---|---|---|---|---|---|---|
| Jun 13-19 | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | 0/7 |

---

## 3. USER PREFERENCES (Emerged During Chats)

| Preference | Detail |
|---|---|
| **Perfectionist** | Wants every formula step shown, no skipped algebra |
| **Hates** | Academic/bookish language, passive voice, "consequently," "thus," "parameter" |
| **Likes** | "you," "we," "so," "here's the deal," short sentences, physical analogies |
| **Conversation style** | Direct, no fluff, doesn't want summaries of what was done unless asked |
| **Corrections** | Expects AI to acknowledge mistakes and fix logically (e.g., the ✅ vs 📄 inconsistency, the buffer definition) |
| **Tone preference** | Concise answers (≤4 lines of text unless detail requested), no preamble/postamble |
| **Visuals** | Wants matplotlib charts for abstract concepts; embedded via Obsidian `![[path.png]]` |
| **Practice problems** | Deferred for separate review passes; current focus is theory delivery |
| **Target psychology** | Wants IISc-level depth, not surface GATE prep |

---

## 4. RECENT HISTORY (Last ~10 Actions)

| # | Date | Action | Detail |
|---|---|---|---|
| 1 | Jun 13 | Initial | Created repo structure with 8 topic folders, README, progress-tracker |
| 2 | Jun 13 | Session 001-005 | Created all 5 Probability sessions (Counting through Exponential) |
| 3 | Jun 13 | Session-003 analysis | User noted session-003's structure was best; rewritten sessions 004, 005 to match |
| 4 | Jun 13 | Progress tracker v1 | Full timeline added with dates, 9 phases, 200-day plan |
| 5 | Jun 13 | Progress tracker v2 | Adjusted to match user's HTML planner — 28/22/18/30/20/38/22/37 day splits |
| 6 | Jun 13 | ✅ vs 📄 fix | User caught inconsistency: future-dated topics can't be ✅; added [📄] status + buffer system |
| 7 | Jun 13 | Buffer split | User clarified: content buffer (pre-written docs) vs study buffer (studied ahead) — track separately |
| 8 | Jun 13 | Major tracker upgrade | Added confidence (1-5), problem counts, weak topics register, weekly review, GA checkboxes, interleaved revision |
| 9 | Jun 13 | tracker-rules.md | Created 9 AI maintenance rules — status logic, buffer calc, update triggers, weekly prompts |
| 10 | Jun 13 | GitHub push | `git push -u origin main` — 24 files, 9,231 lines to https://github.com/GauravKorde/My-GATE-DA- |

---

## 5. ARCHIVE (Compressed — Older History)

> Entries older than ~1 month or superseded by newer decisions move here.

**Pre-Jun 13:** Sessions 001-005 created with initial documentary style. Session-003 identified as best-structured. Sessions 004 and 005 rewritten to match session-003's structure. doubts-solved.md (474-line covariance deep-dive) created. session-rulebook.md created with documentary style conventions. assets/ folder with matplotlib charts created.

---

## AI Maintenance Notes

- Update this file **immediately after** each session creation, user "done" confirmation, or significant decision
- Every update must include the **agent identity** that made the change — add a line like `> Updated by: opencode` or `> Updated by: Antigravity 2.0` at the top of the file under the purpose block
- When RECENT HISTORY exceeds ~15 entries, **compress oldest 5 into ARCHIVE**
- When a phase completes, **move all its session entries into ARCHIVE** with a single summary line
- When a user preference is confirmed over 3+ interactions, **promote it to section 3** and remove from recent history
- Keep ARCHIVE clean — if it grows beyond ~20 lines, remove truly obsolete entries (e.g., resolved style debates)
- The **Dynamic State** section is the most important — keep it accurate at all times
- The **Static Context** should almost never change; only update if user explicitly revises a decision
