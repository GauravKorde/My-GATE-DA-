# Session Rulebook — The Documentary Style

> A permanent reference for constructing every future session.
> Read this before writing any new session. Follow it strictly.

---

## 1. The Core Philosophy

Every session must be a **documentary**, not a textbook chapter.

A textbook: *"The Binomial distribution has PMF $\binom{n}{k}p^k(1-p)^{n-k}$ with mean $np$ and variance $np(1-p)$."*

A documentary: *"You flip a biased coin n times. Each flip is Bernoulli. The total heads is the sum. Let's build the probability from the ground up — first one sequence, then all sequences, then the mean, then the variance. Here's why each formula looks the way it does."*

**Rule:** Never state a formula without deriving it from something simpler. Never derive without explaining *why* each step works.

---

## 2. Chapter Template

Every chapter must follow this structure:

```
## Chapter N: [Evocative Title] — [Subtitle]

### Narrative Hook
- Opens with a problem or question that this chapter will solve
- "What if we could..." / "The problem with..." / "Imagine..."
- Connects to previous chapters: "In Chapter N-1 we learned X. But what about Y?"

### The Setup
- Define the scenario
- Introduce notation
- Build the intuition before the math

### Step-by-Step Derivation
- Break into labeled steps: "Step 1: ...", "Step 2: ..."
- Every algebraic manipulation SHOWN (not "simplifying gives")
- Use numerical examples alongside algebraic steps
- ✅ verification markers after each check

### The Formula
- Box the final result: $$\boxed{formula}$$
- But wait! Before moving on...

### "Let's Understand This Formula"
- A dedicated section after EVERY derived formula
- Ask: What does this tell us? When is it zero? Maximum? Minimum?
- Test extreme values: p=0, p=1, n→∞, etc.
- Connect to intuition: "If p=0.5, variance is maximal because..."

### Numerical Verification
- Test on a concrete example
- Show the numbers work out
- ✅

### Real-World Connection
- Where does this appear in practice?
- Why should the reader care?

### Bridge to Next Section
- Last sentence points forward: "This is the foundation for..."
- OR: "Now that we understand X, what about the related question Y?"
```

---

## 3. Stylistic Checklist

Every session must check ALL of these:

- [ ] **Narrative hook** at chapter start (problem first, solution second)
- [ ] **Self-dialogue moments** ("Wait, let me check...", "This sounds weird but...", "Let me be careful here")
- [ ] **Full algebra** — every common denominator, every factorization, every cancellation shown line by line
- [ ] **Multiple methods** for key derivations (e.g., mean via definition AND via linearity)
- [ ] **Numerical verification** after every formula (test on concrete values)
- [ ] **"Let's understand this formula"** section after every derived result
- [ ] **✅ markers** to verify correctness
- [ ] **Bridge sentences** connecting chapters and previous sessions
- [ ] **Real-world analogies** woven into derivations (not just listed at end)
- [ ] **Extreme case testing** (what happens at boundaries?)
- [ ] **Table summaries** when comparing multiple distributions
- [ ] **Practice problems** with full theoretical explanations in callouts (even if few)

### Tone Markers

- Use phrases like: "Here's the key insight:", "The magic happens when:", "Let me show you why:"
- Address the reader directly: "You might wonder why..."
- Use conversational but precise language
- No monotone "Definition → Property → Theorem → Proof" flow

---

## 4. Mathematical Derivation Standards

### Algebra Must Show

**DO:**
```
Var(X) = (n+1)(2n+1)/6 - ((n+1)/2)²
= (n+1)(2n+1)/6 - (n+1)²/4
= (n+1)[(2n+1)/6 - (n+1)/4]
= (n+1)[2(2n+1)/12 - 3(n+1)/12]
= (n+1)[(4n+2 - 3n - 3)/12]
= (n+1)[(n-1)/12]
```

**DON'T:**
```
Var(X) = (n+1)(2n+1)/6 - ((n+1)/2)²
= (n²-1)/12
```

### Limit Steps Must Show

**DO:**
```
Factor B = (1 - λ/n)^n
We know: e^x = lim_{n→∞} (1 + x/n)^n
So with x = -λ: (1 - λ/n)^n → e^{-λ}

Numerical check for λ=2:
n=10:  (0.8)^10 ≈ 0.107
n=100: (0.98)^100 ≈ 0.133
n=1000: (0.998)^1000 ≈ 0.135
e^{-2} ≈ 0.1353 ← converging
```

### Integration Steps Must Show

- Set up u and dv clearly for integration by parts
- Show boundary term evaluation
- Show remaining integral computation
- Verify final result

### Series Manipulations Must Show

- Show index shifts (k → k-1 → j)
- Show factorial cancellations
- Show why the remaining sum equals a known series

---

## 5. Blueprint Process for New Sessions

Before writing ANY session, follow this process:

### Step A: Read the last session

- Understand the current narrative state
- Identify what topics come next naturally
- Note what bridges need to connect

### Step B: Write a Blueprint (plan mode)

1. List every chapter with its narrative hook
2. Within each chapter, list every Part with its derivation
3. Note which derivations need "two methods" treatment
4. Plan real-world examples for each chapter
5. Plan numerical verification points
6. Plan bridge sentences between chapters
7. **Identify which concepts need matplotlib charts** (flag for generation)

### Step C: Present blueprint for review

- User reviews and approves (or says "go ahead" for standard topics)

### Step D: Expand to full session (build mode)

- Expand each bullet into full documentary narrative
- Follow the Chapter Template from Section 2
- Run the Stylistic Checklist from Section 3
- Every algebraic step must be written out
- **Generate matplotlib charts** for every flagged concept BEFORE writing the chapter
- Embed charts via `![[chart-name.png]]` in Obsidian

---

## 6. Mandatory Quality Checkpoints

**Before declaring a session complete, run through ALL:**

| Checkpoint | Action |
|---|---|
| **Algebra audit** | Every line of algebra verified; no "simplifies to" jumps |
| **Formula audit** | Every boxed formula has a "Let's Understand This Formula" section |
| **Numerical verification** | Every formula tested with concrete numbers; ✅ markers present |
| **Chart audit** | Every abstract concept has a matplotlib PNG (not just ASCII) |
| **Link audit** | Every chapter has a bridge sentence to next chapter |
| **Practice problems** | 3-5 problems: E1, E2, M1, M2, M3 with full solutions |
| **Header correct** | Session header has expected dates, buffer, status |
| **Cross-refs** | References to previous sessions use `⚡ Session XXX` format |
| **Assets committed** | All PNGs saved to `assets/` and embedded correctly |

---

## 7. Visual Generation Standards

**Mandatory matplotlib charts for:**

- Distribution shape evolution (e.g., Binomial → Normal)
- PDF/CDF comparisons across parameters
- Area-under-curve visualizations (68-95-99.7, tail probabilities)
- Symmetry/transform demonstrations
- Convergence sequences (n=10, 100, 1000, ∞)

**Chart style:**

- Clean, minimal, publication-ready
- Colorblind-safe palette (viridis/cividis or explicit hex)
- Axes labeled with units
- Key points annotated (mean, σ, inflection points)
- Saved as PNG to `assets/` at 150 DPI
- Filename pattern: `concept-name.png` (kebab-case)

**Chart style — No ASCII art for statistical graphics** — use matplotlib. ASCII only for quick inline structure.

---

## 8. Problem Difficulty Bands

**Easy (E1, E2):** Direct application of one formula; one-step Z-score or 68-95-99.7 rule

**Medium (M1, M2):** Multi-step; continuity correction, linear transform, sum of Normals, Binomial/Poisson approximation

**Tough (M3):** Multi-concept; conditional probability within approximation, comparing exact vs approx, edge cases (non-linear transforms)

**Each problem must include:**

- Full step-by-step solution
- "Check intuition" or "Verify" step
- ✅ marker at end

---

## 9. Session Header Standard

**Every session file MUST start with:**

```
# Session NNN — [Topic]: The Documentary

> **📅 Expected:** Mon DD – Mon DD | **Buffer:** +X days 🟢 | **Status:** 📄 Doc ready
>
> A first-principles journey through [covered topics].
> Read like a story — each chapter builds on the last.

---
```

Buffer = days docs written ahead of schedule. Status: 📄 Doc ready / ✅ Completed / [~] In progress.

---

## 10. Content Buffer Rules

- **Content buffer** = furthest scheduled session date with 📄 doc - today
- Target: maintain **≥ 7 days** buffer at all times
- If buffer < 7 days → priority is writing next session(s)
- **Study buffer** tracked separately in progress-tracker (user's actual pace)

---

## 11. Error & Correction Protocol

When you catch a mistake (or user points one out):

1. **Acknowledge immediately** — "You're right, that was wrong."
2. **Explain the error** — what was wrong and why
3. **Show the corrected version** — with full derivation
4. **Mark the fix** — add a note: `// FIXED: ...` in the session file
5. **Update session-memory.md** with the correction
6. **Don't be defensive** — treat it as a debugging session

---

## 12. Cross-Session Linking

- Reference previous sessions: `⚡ Session 003` or `🔜 Session 007`
- Use consistent terminology across sessions
- When a concept is first defined, note: `(defined in ⚡ Session XXX)`
- When a concept is extended, note: `(extends ⚡ Session XXX)`

---

## 13. Scope & Length Guidelines

| Session type | Target chapters | Target lines | Problems |
|---|---|---|---|
| Distribution deep-dive (Normal, Exponential) | 8-10 | 800-1200 | 5 |
| Transformation/approximation | 6-8 | 600-900 | 5 |
| Tool session (CLT, Hypothesis) | 6-8 | 600-900 | 4 |
| Review/PYQ | 4-5 | 400-600 | 3 |

**Rule:** One distribution per session file. Don't cram multiple distributions.

---

## 14. Stylistic Rules

### Tone

**Talk like you're explaining the plot of a movie to a friend.** Not like you're writing a research paper.

**❌ Academic / Bookish (DON'T):**

> "If events arrive at a Poisson rate λ, then the waiting time between events follows an Exponential distribution with parameter λ."
> "This ensures the total area under the curve equals 1. The σ in the denominator accounts for the spread."

**✅ Conversational / Narrative (DO):**

> "So here's the situation. Buses arrive at some rate. You're standing at the stop. How long will you wait? That's what Exponential tells you. And here's the neat part: if λ is the rate, your waiting time is Exponential(λ). Simple as that."
> "Think about it this way. If the bell is wider, it needs to be shorter, so the total area still equals 1. That's all the σ in the denominator does — it adjusts the height to match the width."

### Simple Language Toolkit

| Instead of this | Say this |
|---|---|
| "We define X as..." | "Here's what X means..." |
| "It can be shown that..." | "Here's why this works..." |
| "This is called the..." | "We call this the... — here's why the name fits" |
| "Consequently..." | "So..." / "Which means..." |
| "Utilizing the property..." | "Using this trick..." |
| "The following holds true..." | "Check this out..." |
| "Parameter λ" | "λ (the rate)" |
| "X follows a distribution..." | "X is a [Normal/Poisson/Exponential] — here's what that means: ..." |
| Passive voice everywhere | Active voice. "You transform X." Not "X is transformed." |

### The Test

Before writing any section, ask yourself: **"Would I explain it this way to a friend over chai?"**

If the answer is no, rewrite it.

A friend explaining doesn't say "the Poisson distribution converges to Normality as λ increases." They say:

> "Look at what happens when λ gets bigger. When λ is small, the bars are all bunched up on the left. When λ is big, the bars spread out and look like a bell. It just naturally smooths out."

### Specific Patterns

1. **Set up a scene.** Don't state a fact. Paint a picture.
   - ❌ "The Exponential distribution models waiting time."
   - ✅ "You're standing at a bus stop. How long until the bus comes? That's the Exponential."

2. **One idea per sentence.** Short sentences. Periods, not commas.

3. **Use "you" and "we".** Make the reader part of the story.
   - "You want to find P(X > 130). Here's how."
   - "We start from the Binomial PMF."

4. **Show the thinking process.** Don't just state results.
   - ❌ "The integral equals 1/λ."
   - ✅ "Now we need to evaluate this integral. Let's use integration by parts. Set u = t, dv = λe^{-λt}dt..."

5. **Bridge with "so" and "here's the thing".** Make the logic flow natural.
   - "So we've got P(T > t) = e^{-λt}. That's the survival probability. But what we usually want is P(T ≤ t) — the probability that the event has already happened. Here's how we get that..."

6. **End sections with a punchy takeaway.** Don't trail off.
   - ✅ "And that's it. Mean = λ. Variance = λ. For Poisson, they're the same number. That's unique."

---

## 15. Visuals & "Show Me, Don't Tell Me"

### Rule 1: Use Visuals Whenever Possible

Abstract concepts must be accompanied by a visual. Preferred visual types (in order):

**matplotlib charts** (mandatory for statistical graphics):
- Distribution shape evolution (Binomial → Normal)
- PDF/CDF comparisons across parameters
- Area-under-curve visualizations (68-95-99.7, tail probabilities)
- Symmetry/transform demonstrations
- Convergence sequences (n=10, 100, 1000, ∞)

**Mermaid diagrams** for relationships, flow, connections:

```mermaid
graph LR
    A[Binomial<br/>n→∞, p→0] --> B[Poisson<br/>λ = np]
    B --> C[Exponential<br/>Waiting time]
```

**Tables with visual comparison columns:**

| λ | Mean | Spread (σ) | Spread/Mean | Shape |
|---|------|------------|-------------|-------|
| 1 | 1 | 1 | 100% | Very lopsided ← |
| 4 | 4 | 2 | 50% | Somewhat lopsided |
| 16 | 16 | 4 | 25% | Starting to look symmetric |
| 100 | 100 | 10 | 10% | Almost bell-shaped |

**No ASCII art for statistical graphics** — use matplotlib. ASCII only for quick inline structure.

### Rule 2: Use Simple Language — No Bookish/Academic Tone

Talk like you're explaining the plot of a movie to a friend. Not like you're writing a research paper.

### Rule 3: "Show Me, Don't Tell Me" for Abstract Concepts

When explaining a relationship between two quantities:
1. First, say it in plain words
2. Then show a table with numbers
3. Then add a visual (matplotlib chart or Mermaid diagram)

### Rule 4: Tables Over Text for Comparisons

Instead of paragraphs comparing values, use a table. The eye processes tables faster than sentences.

---

## 16. Common Pitfalls to Avoid

| ❌ Mistake | ✅ Fix |
|---|---|
| Stating formula without derivation | Derive from first principles, show every step |
| "It can be shown that..." | Show it yourself |
| Skipping algebra ("simplifying gives") | Write every intermediate line |
| No numerical verification | Test with concrete numbers after every formula |
| No "why" explanation | Add a "Let's understand this formula" section |
| Dry tone | Add self-dialogue, analogies, narrative |
| Bookish/academic language | Use short sentences, "you", physical analogies |
| Abstract without visual | Add table, matplotlib chart, or Mermaid diagram |
| Compressing multiple ideas into one paragraph | Break into subsections with clear headings |
| Forgetting connections to previous topics | Add bridge sentences explicitly |
| Only one method for derivation | Show at least two approaches when possible |
| Formulas without context | Explain what each parameter means in words |
| Walls of text for comparisons | Use a table instead |

---

## 17. Session Structure Template

```
# Session NNN — [Topic]: The Documentary

> **📅 Expected:** Mon DD – Mon DD | **Buffer:** +X days 🟢 | **Status:** 📄 Doc ready
>
> A first-principles journey through [covered topics].
> Read like a story — each chapter builds on the last.

---

## Chapter 1: [Title] — [Subtitle]

### [Narrative hook]

### [The Setup]

### [Step-by-step derivation]

### [The Formula]

### [Let's Understand This Formula]

### [Numerical Verification]

### [Real-World Connection]

---

## Chapter 2: [Title] — [Subtitle]

... (same structure)

---

... (more chapters)

---

## Summary of Formulas

| Distribution | PMF/PDF | Mean | Variance |
|---|---|---|---|

---

## Practice Problems

... At least 3-4 problems with full theoretical explanations

---

> Say **"done session-NNN"** when you've worked through these.
```

---

## 18. The Incremental Learning Rule (Foundational Practice First)

To prevent cognitive overload, we follow a strict small-step learning progression:
*   **Theory First**: We study the theoretical concepts and mathematical derivations of the session first.
*   **Immediate Foundational Practice**: Immediately after the theory of any study session is finished, we **must** run a dedicated foundational practice session covering all the basic formulas of that unit before moving to advanced applications.
*   **No Skipping**: Never jump into complex, multi-concept problems (like competing risks or mixture models) until basic formula fluency is verified.

---

## 19. Summary — The Enhanced Golden Rule

**If a step feels like "too much detail," include it.**
**If a formula feels "obvious," derive it anyway.**
**If an algebraic step is "trivial," show it anyway.**
**If a concept lacks a chart, generate it.**
**If a formula lacks "Let's Understand," write it.**
**If a derivation lacks verification, add it.**

The documentary style leaves nothing to the imagination. Every number, every operation, every transformation, every visual is explained. The reader never has to "fill in the gap."

This is what made Session 003 a gold mine. This is what every session must be.