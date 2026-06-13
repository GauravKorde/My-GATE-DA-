# Session 002 — Conditional Probability, Bayes' Theorem & Expectation

> **📅 Expected:** Jun 18 – Jun 20 | **Buffer:** +13 days 🟢 | **Status:** 📄 Doc ready (written ahead of schedule)

## Topics Covered in This Session
- Joint Probability & Marginal Probability
- Conditional Probability
- Law of Total Probability
- Bayes' Theorem (with full proof)
- Conditional Expectation & Variance
- Covariance & Correlation

---

## Part 1: Joint & Marginal Probability

### The Core Idea

So far in Session 001, we only looked at **one event at a time** — P(A), P(B), etc.

But in real life, events often overlap. We need a way to talk about **"what's the probability that A AND B both happen?"**

That's **joint probability**.

### Step 1 — Start with frequencies (easier to visualize)

Take a class of **100 students**:

| | Boys (B) | Girls (G) | Total |
|---|---|---|---|
| Pass (P) | 40 | 35 | 75 |
| Fail (F) | 20 | 5 | 25 |
| **Total** | **60** | **40** | **100** |

This is a **contingency table** of observed counts.

Now ask: **What's the probability a randomly chosen student is a boy AND passed?**

That means: pick one student at random from 100. How many are both boy and passed?
```
Count = 40 (the cell where row = Pass and column = Boys)
P(Boy ∩ Pass) = 40/100 = 0.4
```

That's a **joint probability** — the cell count divided by total.

The **4 interior cells** (40, 35, 20, 5) each divided by 100 give us the **joint probability distribution**:

| | Boys (B) | Girls (G) | Total |
|---|---|---|---|
| Pass (P) | **0.40** | **0.35** | 0.75 |
| Fail (F) | **0.20** | **0.05** | 0.25 |
| **Total** | **0.60** | **0.40** | **1.00** |

### Step 2 — What is marginal probability?

Look at the table above. The **rightmost column** (Total row-wise) says:
```
P(Pass) = 0.75
P(Fail) = 0.25
```

These are the **marginal probabilities** — they're in the **margins** of the table.

How did we get P(Pass) = 0.75?
```
P(Pass) = P(Pass ∩ Boy) + P(Pass ∩ Girl)
        = 0.40 + 0.35
        = 0.75
```

**Key insight:** To get the probability of Pass alone, we **sum over all possibilities of the other variable** (boys and girls). We're "aggregating" or "marginalizing" over gender.

Similarly:
```
P(Boy) = P(Boy ∩ Pass) + P(Boy ∩ Fail)
       = 0.40 + 0.20
       = 0.60
```

### Step 3 — General definition

For any two events A and B:

```
Joint Probability:    P(A ∩ B) = probability both A AND B occur
Marginal Probability: P(A) = P(A ∩ B) + P(A ∩ B')
```

The table in general form:

| | B | B' | Total (Marginal) |
|---|---|---|---|
| A | **P(A∩B)** | **P(A∩B')** | **P(A)** |
| A' | **P(A'∩B)** | **P(A'∩B')** | **P(A')** |
| **Total** | **P(B)** | **P(B'))** | **1** |

- **Cells** = joint probabilities
- **Row/column sums** = marginal probabilities
- **All cells sum to 1** (because they partition the entire sample space)

### Step 4 — Why do the row sums equal the marginal?

Let's prove it using Axiom 3:

B and B' are **mutually exclusive** (a student can't be both boy and girl) and **exhaustive** (every student is either boy or girl).

Now, event A (Pass) can be split into two parts:
- The part of A that overlaps with B: `A ∩ B`
- The part of A that overlaps with B': `A ∩ B'`

Since B and B' don't overlap, these two parts also don't overlap:
```
(A ∩ B) ∩ (A ∩ B') = ∅
```

And together they cover all of A:
```
(A ∩ B) ∪ (A ∩ B') = A
```

By Axiom 3 (additivity for mutually exclusive events):
```
P(A) = P(A ∩ B) + P(A ∩ B')
```

### Step 5 — Generalizing to many partitions

If B₁, B₂, ..., Bₖ form a **partition** (mutually exclusive and cover everything), then:

```
P(A) = P(A ∩ B₁) + P(A ∩ B₂) + ... + P(A ∩ Bₖ)
```

This is the foundation of the **Law of Total Probability** (which we'll use for Bayes' Theorem).

### Step 6 — Independent vs Dependent joint probability

**Case 1 — Independent events (Session 001 example):**

Roll a die AND toss a coin. These don't affect each other.

Sample space: {(1,H), (1,T), (2,H), (2,T), ..., (6,H), (6,T)} → 12 outcomes

P(die=4 AND coin=H) = ?

Count outcomes where both happen: only (4,H) → 1 outcome
```
P(4 ∩ H) = 1/12
```

Notice: `1/12 = 1/6 × 1/2 = P(4) × P(H)` ✅

For **independent** events: `P(A ∩ B) = P(A) × P(B)`

**Case 2 — Dependent events (class example):**

Pick a random student. A = Pass, B = Boy.

```
P(Pass ∩ Boy) = 40/100 = 0.4
P(Pass) × P(Boy) = 0.75 × 0.60 = 0.45
```

`0.4 ≠ 0.45` → They are **dependent**. Gender affects pass rate.

For **dependent** events: `P(A ∩ B) = P(A|B) × P(B)` (we'll derive this below)

### Quick analogy

Think of the sample space S as a pizza. Events are slices or regions:

```
         S (whole pizza)
┌──────────────────────┐
│        B     B'      │
│   ┌──────────────┐   │
│   │  A∩B   │A∩B' │   │
│ A │        │     │   │
│   │        │     │   │
│   └──────────────┘   │
│                      │
└──────────────────────┘
```

- The whole pizza = S (probability = 1)
- Each slice = a joint probability (A∩B, A∩B', A'∩B, A'∩B')
- All 4 slices together = the whole pizza
- **Marginal P(A)** = the entire A region (left half) = its two slices added
- **Marginal P(B)** = the entire B region (top row) = its two slices added

---

## Part 2: Conditional Probability

### Intuition

Sometimes we have **partial information**. "What's the probability of rain given that it's cloudy?"

Knowing that one event occurred changes our uncertainty about another.

### Definition

The conditional probability of A **given** that B occurred is:

```
P(A | B) = P(A ∩ B) / P(B)    provided P(B) > 0
```

### Derivation of the Formula

**Step 1 — Intuitive approach:**
Suppose we know B happened. The sample space **shrinks** from S to B. Among the outcomes in B, we want those that also belong to A — that is, A ∩ B.

Since we're now restricted to B as the sample space:
```
P(A | B) = |A ∩ B| / |B|    (for equally likely outcomes)
```

**Step 2 — Convert to probabilities:**
Divide numerator and denominator by |S|:
```
P(A | B) = [|A ∩ B| / |S|] / [|B| / |S|] = P(A ∩ B) / P(B)
```

**Step 3 — Final formula:**
```
P(A | B) = P(A ∩ B) / P(B)
```

### Example

Roll a die. Let B = {outcome is even} = {2, 4, 6}, A = {outcome > 3} = {4, 5, 6}.

```
P(A | B) = P(A ∩ B) / P(B) = P({4, 6}) / P({2, 4, 6}) = (2/6) / (3/6) = 2/3
```

Check manually: Given die shows even, possible outcomes are {2, 4, 6}. Among these, {4, 6} are > 3. So 2 out of 3. ✅

### Properties of Conditional Probability

1. **Non-negativity:** `P(A|B) ≥ 0`
2. **Normalization:** `P(B|B) = 1`
3. **Additivity:** If A₁ and A₂ are mutually exclusive:
   `P(A₁ ∪ A₂ | B) = P(A₁|B) + P(A₂|B)`
4. **Complement:** `P(A'|B) = 1 - P(A|B)`

**Proof of complement:**
```
P(A' | B) = P(A' ∩ B) / P(B)
         = [P(B) - P(A ∩ B)] / P(B)    [since A'∩B and A∩B partition B]
         = 1 - P(A ∩ B) / P(B)
         = 1 - P(A | B)
```

### The Multiplication Rule — Intuition

Now we come to the most important rule in this session:

```
P(A ∩ B) = P(A | B) × P(B)
```

This is called the **multiplication rule of probability**. Let me build the intuition 4 different ways.

---

#### Intuition 1: Frequency (easiest to feel)

Take a class of **100 students**:
- 60 are boys → P(Boy) = 0.6
- 80% of boys pass → P(Pass | Boy) = 0.8

Now ask: **How many boys pass?**
```
Boys who pass = (total boys) × (fraction of boys who pass)
              = 60 × 0.8
              = 48 students
```

What's the probability a random student is a boy AND passes?
```
P(Boy ∩ Pass) = 48/100 = 0.48
```

But notice:
```
0.48 = 0.6 × 0.8 = P(Boy) × P(Pass | Boy)
```

That's it. **P(A∩B) = P(B) × P(A|B)** is just: count the total of B, then take only the fraction that also has A.

---

#### Intuition 2: Tree diagram (visual)

Think of events happening **sequentially**:

```
                    ┌── A (P(A|B))
                    │
         ┌── B ─────┤
         │   P(B)   │
         │          └── A' (P(A'|B))
 start ──┤
         │
         │          ┌── A (P(A|B'))
         └── B' ───┤
             P(B')  │
                    └── A' (P(A'|B'))
```

To reach the branch where **both B and A happen**, you need to:
1. Take the B branch first (probability = P(B))
2. Then from there, take the A branch (probability = P(A|B))

So the probability of reaching that leaf = **P(B) × P(A|B)**.

This is exactly like saying: the chance of two sequential events both happening = product of each step's probability.

---

#### Intuition 3: Venn diagram (geometric)

Draw a Venn diagram. The outer box (sample space S) has area = 1.

```
┌─────────────────────────┐
│                         │
│    ┌──────┐             │
│    │      │             │
│    │  B   │             │
│    │ ┌────┼────┐        │
│    │ │A∩B │    │        │
│    │ └────┼────┘        │
│    └──────┘             │
│                         │
└─────────────────────────┘
```

- P(B) = area of circle B
- P(A|B) = fraction of circle B that's also inside circle A
        = area of overlap / area of B
        = P(A∩B) / P(B)

Multiply both sides:
```
P(A∩B) = P(B) × P(A|B)
```

**In words:** The overlap area = (area of B) × (fraction of B that A covers).

---

#### Intuition 4: A concrete everyday example

You have a deck of 52 cards. You draw **one card**.

Let A = "card is a King", B = "card is a face card (J, Q, K)".

```
P(B) = 12/52  (12 face cards)
P(A|B) = 4/12  (4 Kings among the 12 face cards)

P(A ∩ B) = P(B) × P(A|B) = 12/52 × 4/12 = 4/52 = 1/13
```

Check directly: P(King) = 4/52 = 1/13. Since every King is a face card, P(King ∩ Face) = P(King) = 1/13. ✅

---

#### Summary of all 4 intuitions

| Approach | What it says |
|---|---|
| Frequency | Count B's total, then take the fraction that's also A |
| Tree diagram | Trace the sequential path: B happens, then A happens |
| Venn diagram | Area of B × fraction of it overlapped by A |
| Concrete example | Face cards × fraction that are Kings |

**Symmetric version:** Since `A ∩ B = B ∩ A`, we also have:
```
P(A ∩ B) = P(B | A) × P(A)
```

Both are always true. Which one you use depends on which conditional probability is easier to compute.

---

## Part 3: Law of Total Probability

### Statement

If events `B₁, B₂, ..., Bₖ` form a **partition** of the sample space (mutually exclusive and exhaustive), then for any event A:

```
P(A) = P(A|B₁)·P(B₁) + P(A|B₂)·P(B₂) + ... + P(A|Bₖ)·P(Bₖ)
```

### Derivation

**Step 1 — Partition A using B's:**
Since B₁,...,Bₖ partition S, we can write A as:
```
A = (A ∩ B₁) ∪ (A ∩ B₂) ∪ ... ∪ (A ∩ Bₖ)
```

The sets A ∩ Bᵢ are mutually exclusive (because Bᵢ's are disjoint).

**Step 2 — Apply Axiom 3:**
```
P(A) = P(A ∩ B₁) + P(A ∩ B₂) + ... + P(A ∩ Bₖ)
```

**Step 3 — Apply multiplication rule:**
Each term P(A ∩ Bᵢ) = P(A | Bᵢ) · P(Bᵢ)

Therefore:
```
P(A) = P(A|B₁)·P(B₁) + P(A|B₂)·P(B₂) + ... + P(A|Bₖ)·P(Bₖ)
```

### Visual Intuition

```
     S
┌─────────────────────┐
│  B₁    B₂    B₃     │
│  ┌──┐ ┌──┐ ┌──┐    │
│  │A │ │AA│ │ A│    │
│  │∩ │ │∩ │ │∩ │    │
│  │B₁│ │B₂│ │B₃│    │
│  └──┘ └──┘ └──┘    │
└─────────────────────┘
```

P(A) = sum of all the A-pieces across all B-partitions.

### Example

Two machines produce chips:
- Machine X: 60% of output, 2% defective
- Machine Y: 40% of output, 5% defective

What's P(defective)?

Let B₁ = "made by X", B₂ = "made by Y", A = "defective"

```
P(A) = P(A|B₁)·P(B₁) + P(A|B₂)·P(B₂)
     = 0.02 × 0.60 + 0.05 × 0.40
     = 0.012 + 0.020
     = 0.032  (3.2%)
```

---

## Part 4: Bayes' Theorem

### The Problem

We know `P(A|B)`. Can we find `P(B|A)`?

This is the **inverse probability** problem — and it's what Bayes' Theorem solves.

### Statement

For two events A and B:
```
P(B|A) = P(A|B) × P(B) / P(A)
```

More generally, if B₁, B₂, ..., Bₖ partition S:
```
P(Bᵢ|A) = P(A|Bᵢ) × P(Bᵢ) / Σⱼ[P(A|Bⱼ)·P(Bⱼ)]
```

### Derivation (step by step)

**Step 1 — Start with the definition of conditional probability:**

From Part 2:
```
P(B|A) = P(B ∩ A) / P(A)      ...(1)
```

**Step 2 — Joint probability is symmetric:**
```
P(B ∩ A) = P(A ∩ B)           ...(2)
```

**Step 3 — Rewrite using multiplication rule:**
```
P(A ∩ B) = P(A | B) × P(B)    ...(3)
```

**Step 4 — Substitute (2) and (3) into (1):**
```
P(B|A) = P(A|B) × P(B) / P(A)
```

This is the **simple form** of Bayes' Theorem.

**Step 5 — Expand P(A) using Law of Total Probability:**

If B₁,...,Bₖ partition S:
```
P(A) = Σⱼ P(A|Bⱼ)·P(Bⱼ)
```

Substitute:
```
P(Bᵢ|A) = P(A|Bᵢ)·P(Bᵢ) / Σⱼ[P(A|Bⱼ)·P(Bⱼ)]
```

This is the **general form**.

### The Terminology

| Term | Name | Meaning |
|---|---|---|
| `P(Bᵢ)` | **Prior** | Belief before seeing evidence |
| `P(A | Bᵢ)` | **Likelihood** | How likely evidence is given each hypothesis |
| `P(Bᵢ | A)` | **Posterior** | Updated belief after seeing evidence |
| `P(A)` | **Evidence** | Total probability of the evidence |

So Bayes' Theorem says:
```
Posterior = (Likelihood × Prior) / Evidence
```

### Example (continued from Part 3)

Machine X: 60% output, 2% defective
Machine Y: 40% output, 5% defective

A chip is found defective. What's the probability it came from Machine X?

We want `P(B₁ | A)`:

```
P(B₁ | A) = P(A | B₁) × P(B₁) / P(A)
          = 0.02 × 0.60 / 0.032
          = 0.012 / 0.032
          = 0.375  (37.5%)
```

And from Machine Y:
```
P(B₂ | A) = P(A | B₂) × P(B₂) / P(A)
          = 0.05 × 0.40 / 0.032
          = 0.020 / 0.032
          = 0.625  (62.5%)
```

Notice: `P(B₁|A) + P(B₂|A) = 1` — the posterior probabilities still sum to 1.

Also notice: Before seeing evidence (prior), Machine X had higher probability (60%). After seeing a defect (evidence), Machine Y becomes more likely (62.5%) because it has higher defect rate. This is Bayesian updating in action.

### Another Example — The Medical Test (Classic Bayes Problem)

This is **the most famous Bayes' Theorem example** because the answer shocks everyone.

#### The Setup

A disease affects **1%** of the population. A test exists:
- If you **have** the disease → test is positive **99%** of the time (called **sensitivity**)
- If you are **healthy** → test is negative **98%** of the time (called **specificity**)

**You take the test. It comes back POSITIVE. What's the probability you actually have the disease?**

Most people guess "99%". Let's see why that's wrong.

---

#### Step 1 — Convert to frequencies (concrete numbers)

Percentages are abstract. Let's use **100,000 people**:

| Group | Count | Test Result |
|---|---|---|
| Has disease (1%) | **1,000** | 99% positive = **990** positive, 10 negative |
| Healthy (99%) | **99,000** | 2% positive = **1,980** positive, 97,020 negative |

Where did the numbers come from?

**Diseased people:** 1% of 100,000 = 1,000
- Test catches 99% of them: 1,000 × 0.99 = **990 positive**
- Test misses 1%: 1,000 × 0.01 = 10 negative

**Healthy people:** 99% of 100,000 = 99,000
- Test correctly says negative for 98%: 99,000 × 0.98 = 97,020 negative
- Test **wrongly** says positive for 2%: 99,000 × 0.02 = **1,980 positive**

---

#### Step 2 — Look at the positives only

You tested positive. So you're in the **positive group**:

| Source | Positive count |
|---|---|
| Diseased (true positive) | 990 |
| Healthy (false positive) | 1,980 |
| **Total positive** | **2,970** |

Now the question becomes simple:

**Out of all positives, what fraction actually has the disease?**

```
P(Disease | Positive) = 990 / 2970 = 0.333... = 33.3%
```

---

#### Step 3 — Why is it only 33% not 99%?

Because **healthy people outnumber sick people 99:1**.

Even though the false positive rate is small (2%), when you multiply it by the massive healthy population (99,000), you get **1,980 false positives**.

Compare:
- True positives = 990 (small group × high accuracy)
- False positives = 1,980 (huge group × small error)

False positives **outnumber** true positives 2:1.

**Visualizing it:**
```
All 100,000 people:
┌────────────────────────────────────────────────────┐
│   Healthy (99,000)                                 │
│   ┌──────────────────────────────────────────┐     │
│   │  Tested negative (97,020)                │     │
│   │                                          │     │
│   │  Tested POSITIVE (1,980) ← YOU ARE HERE │     │
│   └──────────────────────────────────────────┘     │
│                                                    │
│   Diseased (1,000)                                 │
│   ┌──────────────────┐                             │
│   │ Positive (990)   │ ← YOU COULD BE HERE        │
│   │ Negative (10)    │                             │
│   └──────────────────┘                             │
└────────────────────────────────────────────────────┘
```

Among positive results (1,980 + 990 = 2,970), only 990/2,970 = 1/3 are actually sick.

---

#### Step 4 — Now do it with formulas (Bayes' Theorem)

Let D = "has disease", T⁺ = "tests positive"

**Prior information (what we know before the test):**
```
P(D) = 0.01        (1% of population has disease)
P(D') = 0.99       (99% are healthy)
```

**Likelihood (test accuracy):**
```
P(T⁺ | D) = 0.99   (sensitivity: 99% of sick test positive)
P(T⁺ | D') = 0.02  (false positive rate: 2% of healthy test positive)
```

**Step 4.1 — Evidence: Total probability of positive test**

Using Law of Total Probability:
```
P(T⁺) = P(T⁺|D)·P(D) + P(T⁺|D')·P(D')
      = 0.99 × 0.01  +  0.02 × 0.99
      = 0.0099       +  0.0198
      = 0.0297
```

Interpretation: **2.97%** of the entire population will test positive (both true and false).

**Step 4.2 — Posterior: Probability of disease given positive**

Using Bayes' Theorem:
```
P(D | T⁺) = P(T⁺ | D) × P(D) / P(T⁺)
          = 0.99 × 0.01 / 0.0297
          = 0.0099 / 0.0297
          = 0.3333
```

**Answer: 33.3%**

---

#### Step 5 — Why the intuition fails

| What people think | What actually happens |
|---|---|
| "Test is 99% accurate" | Accuracy = (990 + 97,020) / 100,000 = **98.01%** |
| "If positive, 99% chance I'm sick" | **33%** chance — because base rate matters |
| "2% false positive is small" | 2% of 99,000 = 1,980 is **larger** than 99% of 1,000 = 990 |

This is called the **Base Rate Fallacy** — ignoring the rarity of the disease and focusing only on test accuracy.

---

#### Key Takeaway

Bayes' Theorem tells us: **Your belief after seeing evidence depends on your belief before seeing evidence.**

If the disease were more common, the posterior probability would be higher:
- If P(D) = 10% → P(D|T⁺) = **84.6%**
- If P(D) = 50% → P(D|T⁺) = **98.0%**

The same test, same accuracy — but different prior → different posterior.

This is why doctors don't mass-screen rare diseases — too many false positives cause panic and unnecessary procedures.

---

## Part 5: Conditional Expectation

### 5.1 Review: What is Expectation?

**Intuition first:** If you roll a die many times, what's the **average** number you'll get?

You'd sum all the outcomes and divide by count: `(1+2+3+4+5+6)/6 = 3.5`

That's the **expectation**. But formally, since each outcome has probability 1/6:

```
E[X] = 1×(1/6) + 2×(1/6) + 3×(1/6) + 4×(1/6) + 5×(1/6) + 6×(1/6)
     = (1+2+3+4+5+6)/6
     = 3.5
```

**General definition:** For a discrete random variable X with values x₁, x₂, ..., xₙ:

```
E[X] = Σᵢ xᵢ · P(X = xᵢ)
```

It's a **probability-weighted average** — each value is weighted by how likely it is.

### 5.2 Conditional Expectation — The Idea

Sometimes we have **extra information**. "Given that it's an even roll, what's the expected value?"

We don't use the original probabilities anymore — we use **conditional probabilities** given the event.

```
E[X | B] = Σᵢ xᵢ · P(X = xᵢ | B)
```

### 5.3 Example — Step by Step

**Roll a fair die.** X = number shown.

**Unconditional expectation (no information):**
```
E[X] = 1·(1/6) + 2·(1/6) + 3·(1/6) + 4·(1/6) + 5·(1/6) + 6·(1/6)
     = 21/6 = 3.5
```

**Now we're told: the outcome is EVEN.** B = {2, 4, 6}

Step 1 — Find conditional probabilities:
```
P(X=2 | B) = P(X=2 ∩ B) / P(B) = P({2}) / P({2,4,6}) = (1/6) / (3/6) = 1/3
P(X=4 | B) = 1/3
P(X=6 | B) = 1/3
```

Step 2 — Compute conditional expectation:
```
E[X | B] = 2·(1/3) + 4·(1/3) + 6·(1/3)
         = (2+4+6)/3
         = 12/3
         = 4
```

**Interpretation:** Knowing the outcome is even raises our expected value from 3.5 to 4.

### 5.4 Conditional Expectation given a Random Variable

Often we condition on **another random variable Y** rather than a fixed event.

#### Derivation of the formula

**Step 1 — Recall the definition of conditional probability:**
```
P(X = xᵢ | Y = yⱼ) = P(X = xᵢ, Y = yⱼ) / P(Y = yⱼ)
```

This is the probability that X = xᵢ **within the subgroup where Y = yⱼ**.

**Step 2 — Conditional expectation is just expectation using these conditional probabilities:**

For a fixed Y = yⱼ, we compute the weighted average of X's values, where the weights are the conditional probabilities:

```
E[X | Y = yⱼ] = Σᵢ xᵢ · P(X = xᵢ | Y = yⱼ)
```

**Step 3 — Expanding using the definition:**
```
E[X | Y = yⱼ] = Σᵢ xᵢ · P(X = xᵢ, Y = yⱼ) / P(Y = yⱼ)
```

This makes it computable from the **joint distribution** of X and Y.

**Key insight:** For each possible value yⱼ, we get a different number E[X | Y = yⱼ]. This means E[X | Y] is a **function** of Y — call it g(Y).

#### Concrete example — Joint distribution table

Let X = {1, 2} and Y = {0, 1} with joint probabilities:

| X\Y | Y=0 | Y=1 | P(X) |
|---|---|---|---|
| X=1 | 0.2 | 0.3 | 0.5 |
| X=2 | 0.4 | 0.1 | 0.5 |
| P(Y) | 0.6 | 0.4 | 1 |

**Step 1 — Compute P(Y = yⱼ):**
```
P(Y=0) = 0.2 + 0.4 = 0.6
P(Y=1) = 0.3 + 0.1 = 0.4
```

**Step 2 — Compute conditional probabilities P(X | Y = 0):**
```
P(X=1 | Y=0) = P(X=1, Y=0) / P(Y=0) = 0.2/0.6 = 1/3
P(X=2 | Y=0) = P(X=2, Y=0) / P(Y=0) = 0.4/0.6 = 2/3
```

**Step 3 — Compute E[X | Y = 0]:**
```
E[X | Y=0] = 1·(1/3) + 2·(2/3) = 1/3 + 4/3 = 5/3 ≈ 1.667
```

**Step 4 — Compute conditional probabilities P(X | Y = 1):**
```
P(X=1 | Y=1) = 0.3/0.4 = 3/4
P(X=2 | Y=1) = 0.1/0.4 = 1/4
```

**Step 5 — Compute E[X | Y = 1]:**
```
E[X | Y=1] = 1·(3/4) + 2·(1/4) = 3/4 + 2/4 = 5/4 = 1.25
```

**Step 6 — E[X|Y] as a function:**
```
E[X | Y] = { 5/3  if Y=0
           { 5/4  if Y=1
```

This is a random variable! It takes value 5/3 with probability 0.6 and value 5/4 with probability 0.4.

**Step 7 — Verify Law of Total Expectation:**
```
E[E[X|Y]] = (5/3)(0.6) + (5/4)(0.4)
          = (5/3)(3/5) + (5/4)(2/5)
          = 1 + 0.5
          = 1.5

E[X] = 1·0.5 + 2·0.5 = 1.5 ✅
```

### 5.5 Law of Total Expectation — Derivation

#### First, the intuition (no formulas)

Imagine you want the average height of **all students** in a school.

You could:
- Method 1: Measure every single student and average them → **E[X]**
- Method 2: 
  1. Find average height of **boys** → E[X | Boy]
  2. Find average height of **girls** → E[X | Girl]
  3. Average those two: `E[X|Boy] × (%boys) + E[X|Girl] × (%girls)` → **also E[X]**

**Y is just the "grouping variable."** Here Y = gender. It splits the population into groups. Within each group, we compute the average. Then we average those group averages.

We introduce Y because **sometimes it's easier to compute group averages first** and then combine them.

---

#### Step-by-step with the school example

**Data:**
- 60 boys with average height **170 cm**
- 40 girls with average height **160 cm**

**What's the overall average height?**

Without grouping:
```
You'd need every single student's height → not always possible
```

With grouping (Law of Total Expectation):
```
E[Height] = E[Height | Boy] × P(Boy) + E[Height | Girl] × P(Girl)
          = 170 × 0.6 + 160 × 0.4
          = 102 + 64
          = 166 cm
```

The grouping variable is **Y = Gender**, which takes values {Boy, Girl}.

This is ALL that Law of Total Expectation does. The formula `E[X] = E[E[X|Y]]` is just a fancy way of writing: **average of group averages, weighted by group size**.

---

#### Now the math — derived from scratch

**Statement:**
```
E[X] = E[ E[X | Y] ]
```

**Step 1 — What is E[X]?**
```
E[X] = Σᵢ xᵢ · P(X = xᵢ)
```
Just the weighted average of all X values.

**Step 2 — Break P(X = xᵢ) using Y as the grouping variable**

Y splits the world into groups {y₁, y₂, ..., yₘ}. Any X value must happen **within one of these groups**. So:

```
P(X = xᵢ) = P(X = xᵢ AND Y = y₁) + P(X = xᵢ AND Y = y₂) + ... + P(X = xᵢ AND Y = yₘ)
```

Or in short:
```
P(X = xᵢ) = Σⱼ P(X = xᵢ, Y = yⱼ)
```

**Step 3 — Substitute into E[X]:**
```
E[X] = Σᵢ xᵢ · [ Σⱼ P(X = xᵢ, Y = yⱼ) ]
```

**Step 4 — Swap the sums (just rearranging terms):**
```
E[X] = Σⱼ [ Σᵢ xᵢ · P(X = xᵢ, Y = yⱼ) ]
```

**Step 5 — Rewrite joint probability using conditional probability:**

Recall: `P(X = xᵢ, Y = yⱼ) = P(X = xᵢ | Y = yⱼ) · P(Y = yⱼ)`

So:
```
E[X] = Σⱼ [ Σᵢ xᵢ · P(X = xᵢ | Y = yⱼ) · P(Y = yⱼ) ]
```

**Step 6 — Factor out P(Y = yⱼ)** (it doesn't depend on the inner sum i):
```
E[X] = Σⱼ [ Σᵢ xᵢ · P(X = xᵢ | Y = yⱼ) ] · P(Y = yⱼ)
```

**Step 7 — Recognize the inner sum:**

`Σᵢ xᵢ · P(X = xᵢ | Y = yⱼ)` is exactly **E[X | Y = yⱼ]** — the average of X **within group yⱼ**.

So:
```
E[X] = Σⱼ E[X | Y = yⱼ] · P(Y = yⱼ)
```

This is: **average of group-averages, weighted by group size**.

**Step 8 — Recognize the right side as E[E[X|Y]]:**

The expression `Σⱼ (something) × P(Y = yⱼ)` is exactly the **expectation of that something** over Y.

Here the "something" is `E[X | Y = yⱼ]` — which is a function of Y. So:

```
E[X] = E[ E[X | Y] ]
```

---

#### The "Y comes out of nowhere" confusion — resolved

**Question:** Why introduce Y at all? Why not just compute E[X] directly?

**Answer:** You don't need Y if you have direct access to X's distribution. But in many real problems:

- You know the average within each group but not the overall average
- The joint distribution with Y is easier to work with
- It lets you break a hard problem into smaller pieces

**Example where it's useful:**

A store's sales depend on whether it's a weekday or weekend:
- Weekdays (5 days, 71.4% of week): average sales = **$1000**
- Weekends (2 days, 28.6% of week): average sales = **$3000**

What's the expected daily sales?

```
E[Sales] = E[Sales|Weekday]·P(Weekday) + E[Sales|Weekend]·P(Weekend)
         = 1000 × (5/7) + 3000 × (2/7)
         = 714.29 + 857.14
         = 1571.43
```

Here Y = {Weekday, Weekend}. Without grouping by Y, you'd need every single day's sales.

**This is NOT introducing Y randomly — it's choosing a grouping that simplifies the problem.**

### 5.6 Example — Factory Machines

**Problem:** A factory has two machines:
- Machine A: produces 60% of items, average weight = 10g
- Machine B: produces 40% of items, average weight = 12g

**What's the expected weight of a random item?**

We want E[W] where W = weight.

```
E[W] = E[W | A]·P(A) + E[W | B]·P(B)
     = 10 × 0.6 + 12 × 0.4
     = 6 + 4.8
     = 10.8g
```

**Check with Law of Total Expectation:**
E[W | machine] is a random variable (depends on which machine).
- E[W | A] = 10 with probability 0.6
- E[W | B] = 12 with probability 0.4

```
E[E[W | machine]] = 10·0.6 + 12·0.4 = 10.8 = E[W] ✅
```

---

## Part 6: Conditional Variance

### 6.1 Review: What is Variance?

**Intuition:** Expectation tells us the **center**. Variance tells us the **spread**.

Two datasets with same mean: {5, 5, 5} and {0, 5, 10} both have mean = 5, but the second is more spread out.

**Definition:** Variance = average squared distance from the mean.

```
Var(X) = E[(X - μ)²]    where μ = E[X]
```

#### Derivation of the shortcut formula

**Step 1 — Expand the square:**
```
Var(X) = E[(X - μ)²]
       = E[X² - 2μX + μ²]
```

**Step 2 — Apply linearity of expectation:** E[A + B] = E[A] + E[B], and E[cX] = c·E[X] for constant c.
```
Var(X) = E[X²] - E[2μX] + E[μ²]
```

**Step 3 — Simplify each term:**
- `E[2μX] = 2μ·E[X] = 2μ·μ = 2μ²` (since μ is a constant)
- `E[μ²] = μ²` (μ² is a constant)

```
Var(X) = E[X²] - 2μ² + μ²
       = E[X²] - μ²
       = E[X²] - (E[X])²
```

**Final shortcut formula:**
```
Var(X) = E[X²] - (E[X])²
```

This is easier to compute: find the average of squares, then subtract the square of the average.

#### Example

X = die roll: {1, 2, 3, 4, 5, 6}

```
E[X] = 3.5
E[X²] = (1² + 2² + 3² + 4² + 5² + 6²)/6 = (1+4+9+16+25+36)/6 = 91/6 ≈ 15.167

Var(X) = 91/6 - (3.5)² = 15.167 - 12.25 = 2.917
```

### 6.2 Conditional Variance

Just like conditional expectation, conditional variance is the variance **within a subgroup**:

```
Var(X | Y) = E[(X - E[X|Y])² | Y]
```

And the shortcut form (same derivation as above, just conditional):

```
Var(X | Y) = E[X² | Y] - (E[X | Y])²
```

### 6.3 Law of Total Variance — Full Derivation

**Statement:**
```
Var(X) = E[Var(X | Y)] + Var(E[X | Y])
```

**In words:** Total variance = average of within-group variances + variance of group means.

#### Derivation step by step

**Step 1 — Start with the shortcut formula:**
```
Var(X) = E[X²] - (E[X])²                    ...(1)
```

**Step 2 — Apply Law of Total Expectation to E[X²]:**
```
E[X²] = E[ E[X² | Y] ]                     ...(2)
```
This is just the Law of Total Expectation applied to the random variable X².

**Step 3 — Apply Law of Total Expectation to E[X]:**
```
E[X] = E[ E[X | Y] ]                       ...(3)
```

**Step 4 — Substitute (2) and (3) into (1):**
```
Var(X) = E[ E[X² | Y] ] - (E[ E[X | Y] ])²   ...(4)
```

**Step 5 — Express E[X² | Y] in terms of conditional variance and conditional mean:**

From the shortcut formula for conditional variance:
```
Var(X | Y) = E[X² | Y] - (E[X | Y])²
```
Rearrange:
```
E[X² | Y] = Var(X | Y) + (E[X | Y])²         ...(5)
```

**Step 6 — Substitute (5) into (4):**
```
Var(X) = E[ Var(X | Y) + (E[X | Y])² ] - (E[ E[X | Y] ])²
```

**Step 7 — Split the expectation using linearity:**
```
Var(X) = E[ Var(X | Y) ] + E[ (E[X | Y])² ] - (E[ E[X | Y] ])²
```

**Step 8 — Recognize the last two terms as variance of E[X|Y]:**

The expression `E[Z²] - (E[Z])²` is exactly `Var(Z)` where Z = E[X|Y].

Therefore:
```
Var(X) = E[ Var(X | Y) ] + Var( E[X | Y] )
```

#### Intuition with the factory example

Two machines: A produces items with mean 10g, variance 1g²; B produces mean 12g, variance 2g².

**Within-group variances:** Machine A: 1, Machine B: 2
**Between-group variance:** The group means (10 and 12) vary around the overall mean (10.8).

```
E[Var(W | machine)] = 1 × 0.6 + 2 × 0.4 = 0.6 + 0.8 = 1.4
Var(E[W | machine]) = (10-10.8)²×0.6 + (12-10.8)²×0.4 = 0.64×0.6 + 1.44×0.4 = 0.384 + 0.576 = 0.96

Total Var(W) = 1.4 + 0.96 = 2.36
```

The total variance comes partly from **variation within each machine** (1.4) and partly from **difference between machines** (0.96).

---

## Part 7: Covariance & Correlation

### 7.1 Covariance — What It Actually Measures

**Variance** told us: "How much does a single variable X spread around its mean?"

**Covariance** tells us: "When X is above its mean, does Y also tend to be above its mean? Or below?"

#### The Four Quadrants Intuition

Draw a scatter plot. Divide it into 4 quadrants using the means μx and μy as axes:

$$
\begin{array}{c}
\text{Y} \uparrow \\[4pt]
\begin{array}{c|c}
\begin{array}{l}
\text{Quadrant II} \\
X < \mu_x,\; Y > \mu_y \\
(-) \times (+) = \textbf{-}
\end{array}
&
\begin{array}{l}
\text{Quadrant I} \\
X > \mu_x,\; Y > \mu_y \\
(+) \times (+) = \textbf{+}
\end{array} \\[4pt]
\hline \\[4pt]
\begin{array}{l}
\text{Quadrant III} \\
X < \mu_x,\; Y < \mu_y \\
(-) \times (-) = \textbf{+}
\end{array}
&
\begin{array}{l}
\text{Quadrant IV} \\
X > \mu_x,\; Y < \mu_y \\
(+) \times (-) = \textbf{-}
\end{array}
\end{array} \\[4pt]
\longleftarrow \mu_x \longrightarrow \\
\downarrow \\
\text{X}
\end{array}
$$

For each data point, compute: $(X - \mu_x) \times (Y - \mu_y)$

| Point location | X vs μx | Y vs μy | Product | Contribution to Cov |
|---|---|---|---|---|
| Quadrant I | X > μx (+) | Y > μy (+) | (+) × (+) = **+** | Increases Cov |
| Quadrant III | X < μx (−) | Y < μy (−) | (−) × (−) = **+** | Increases Cov |
| Quadrant II | X < μx (−) | Y > μy (+) | (−) × (+) = **−** | Decreases Cov |
| Quadrant IV | X > μx (+) | Y < μy (−) | (+) × (−) = **−** | Decreases Cov |

**If most points are in Quadrants I and III** → most products are positive → Cov > 0 (X and Y move together)

**If most points are in Quadrants II and IV** → most products are negative → Cov < 0 (X and Y move opposite)

**If points are scattered equally** → products cancel out → Cov ≈ 0 (no linear relationship)

### 7.2 Definition of Covariance

The population covariance of two random variables X and Y is:

$$
\text{Cov}(X, Y) = E[(X - \mu_x)(Y - \mu_y)] \quad \text{where } \mu_x = E[X],\; \mu_y = E[Y]
$$

It is the **average of the products of deviations from the means**.

### 7.3 Full Walkthrough — Small Dataset (Step by Step)

Let's compute covariance from scratch using a real dataset.

#### Dataset: Hours studied (X) vs Exam score (Y)

| Student | X (hours) | Y (score) |
|---|---|---|
| A | 1 | 40 |
| B | 2 | 50 |
| C | 3 | 60 |
| D | 4 | 70 |
| E | 5 | 80 |

**Step 1 — Compute the means:**
$$
\mu_x = \frac{1+2+3+4+5}{5} = \frac{15}{5} = 3, \qquad
\mu_y = \frac{40+50+60+70+80}{5} = \frac{300}{5} = 60
$$

**Step 2 — Compute deviations and their products for each point:**

| Student | X | Y | X - μx | Y - μy | (X-μx)(Y-μy) |
|---|---|---|---|---|---|
| A | 1 | 40 | 1-3 = -2 | 40-60 = -20 | (-2)×(-20) = +40 |
| B | 2 | 50 | 2-3 = -1 | 50-60 = -10 | (-1)×(-10) = +10 |
| C | 3 | 60 | 3-3 = 0 | 60-60 = 0 | 0×0 = 0 |
| D | 4 | 70 | 4-3 = +1 | 70-60 = +10 | (+1)×(+10) = +10 |
| E | 5 | 80 | 5-3 = +2 | 80-60 = +20 | (+2)×(+20) = +40 |

All 5 students fall in Quadrants I or III → all products are positive.

**Step 3 — Average the products:**
$$
\text{Cov}(X, Y) = \frac{40 + 10 + 0 + 10 + 40}{5} = \frac{100}{5} = 20
$$

**Interpretation:** Cov = 20. Positive → more study hours → higher score.

---

#### Dataset 2: Price (X) vs Demand (Y) — Negative Covariance

| Day | X (price $) | Y (units sold) |
|---|---|---|
| Mon | 10 | 100 |
| Tue | 20 | 80 |
| Wed | 30 | 60 |
| Thu | 40 | 40 |
| Fri | 50 | 20 |

**Step 1 — Means:**
$$
\mu_x = \frac{10+20+30+40+50}{5} = 30,\qquad
\mu_y = \frac{100+80+60+40+20}{5} = 60
$$

**Step 2 — Products:**

| Day | X | Y | X-μx | Y-μy | (X-μx)(Y-μy) |
|---|---|---|---|---|---|
| Mon | 10 | 100 | -20 | +40 | -800 |
| Tue | 20 | 80 | -10 | +20 | -200 |
| Wed | 30 | 60 | 0 | 0 | 0 |
| Thu | 40 | 40 | +10 | -20 | -200 |
| Fri | 50 | 20 | +20 | -40 | -800 |

**Step 3 — Average:**
$$
\text{Cov}(X, Y) = \frac{-800 + (-200) + 0 + (-200) + (-800)}{5} = \frac{-2000}{5} = -400
$$

**Interpretation:** Cov = -400. Negative → price goes up → demand goes down.

---

#### Dataset 3: Shoe Size (X) vs IQ Score (Y) — Zero Covariance

| Person | X (shoe size) | Y (IQ) |
|---|---|---|
| P | 6 | 100 |
| Q | 7 | 110 |
| R | 8 | 90 |
| S | 9 | 105 |
| T | 10 | 95 |

**Step 1 — Means:**
$$
\mu_x = \frac{6+7+8+9+10}{5} = 8,\qquad
\mu_y = \frac{100+110+90+105+95}{5} = \frac{500}{5} = 100
$$

**Step 2 — Products:**

| Person | X | Y | X-μx | Y-μy | (X-μx)(Y-μy) |
|---|---|---|---|---|---|
| P | 6 | 100 | -2 | 0 | 0 |
| Q | 7 | 110 | -1 | +10 | -10 |
| R | 8 | 90 | 0 | -10 | 0 |
| S | 9 | 105 | +1 | +5 | +5 |
| T | 10 | 95 | +2 | -5 | -10 |

**Step 3 — Average:**
$$
\text{Cov}(X, Y) = \frac{0 + (-10) + 0 + 5 + (-10)}{5} = \frac{-15}{5} = -3
$$

Cov ≈ -3, which is very close to 0 relative to the scale of the data. This suggests **no meaningful linear relationship** between shoe size and IQ (as expected).

### 7.4 Derivation of the Shortcut Formula (Detailed)

The definition $\text{Cov}(X, Y) = E[(X - \mu_x)(Y - \mu_y)]$ requires computing deviations for every point. There's a much easier formula:

$$
\text{Cov}(X, Y) = E[XY] - E[X]\cdot E[Y]
$$

Let's derive it step by step.

**Step 1 — Start with the definition:**
$$
\text{Cov}(X, Y) = E[(X - \mu_x)(Y - \mu_y)]
$$

**Step 2 — Expand the product:**
$$
\text{Cov}(X, Y) = E[\,X\cdot Y - X\cdot\mu_y - \mu_x\cdot Y + \mu_x\cdot\mu_y\,]
$$

**Step 3 — Apply linearity of expectation:**

Linearity says: $E[A + B] = E[A] + E[B]$ and $E[c\cdot A] = c\cdot E[A]$ for constant $c$.

$$
\text{Cov}(X, Y) = E[XY] - E[X\cdot\mu_y] - E[\mu_x\cdot Y] + E[\mu_x\cdot\mu_y]
$$

**Step 4 — Pull out constants:**

$\mu_y$ is a constant, so $E[X\cdot\mu_y] = \mu_y\cdot E[X]$.

Similarly, $E[\mu_x\cdot Y] = \mu_x\cdot E[Y]$.

And $E[\mu_x\cdot\mu_y] = \mu_x\cdot\mu_y$ (both are constants).

$$
\text{Cov}(X, Y) = E[XY] - \mu_y\cdot E[X] - \mu_x\cdot E[Y] + \mu_x\cdot\mu_y
$$

**Step 5 — Substitute $E[X] = \mu_x$ and $E[Y] = \mu_y$:**
$$
\text{Cov}(X, Y) = E[XY] - \mu_y\cdot\mu_x - \mu_x\cdot\mu_y + \mu_x\cdot\mu_y
$$

**Step 6 — Simplify:**
$$
\text{Cov}(X, Y) = E[XY] - \mu_x\cdot\mu_y
                 = E[XY] - E[X]\cdot E[Y]
$$

**Final shortcut formula:**
$$
\text{Cov}(X, Y) = E[XY] - E[X]\cdot E[Y]
$$

### 7.5 Verification — Both Formulas Give the Same Answer

Let's verify with the study hours dataset $(X = \{1,2,3,4,5\},\; Y = \{40,50,60,70,80\})$:

**Using the definition method (we already did this):**
$$
\text{Cov} = \frac{40 + 10 + 0 + 10 + 40}{5} = 20
$$

**Using the shortcut method:**

Step 1 — $E[X]$ and $E[Y]$:
$$
E[X] = 3,\qquad E[Y] = 60
$$

Step 2 — $E[XY]$:
$$
E[XY] = \frac{1\times40 + 2\times50 + 3\times60 + 4\times70 + 5\times80}{5}
      = \frac{40 + 100 + 180 + 280 + 400}{5}
      = \frac{1000}{5} = 200
$$

Step 3 — Cov:
$$
\text{Cov} = 200 - 3\times60 = 200 - 180 = 20 \;\;\checkmark
$$

Same answer, much less work.

### 7.6 Interpreting Covariance

| Cov(X,Y) | Sign | What it means | Example |
|---|---|---|---|
| > 0 | + | X↑ → Y↑, X↓ → Y↓ | Study hours vs Score |
| < 0 | − | X↑ → Y↓, X↓ → Y↑ | Price vs Demand |
| = 0 | 0 | No **linear** relationship | Shoe size vs IQ |

**Important:** Cov = 0 does NOT mean "no relationship." There could still be a **non-linear** relationship (e.g., $X^2$, $\sin(X)$, etc.)

$$
\begin{aligned}
X &= \{-2,\; -1,\; 0,\; 1,\; 2\} \\
Y &= \{4,\; 1,\; 0,\; 1,\; 4\} \quad (Y = X^2) \\
\text{Cov}(X,Y) &= 0 \;\longleftarrow\; \text{but clearly } Y \text{ depends on } X!
\end{aligned}
$$

### 7.7 The Scale Problem

Covariance is **not normalized** — it changes with the units of measurement.

**Example:** Height in meters vs Height in centimeters

| Person | Height (m) | Height (cm) | Weight (kg) |
|---|---|---|---|
| A | 1.5 | 150 | 50 |
| B | 1.6 | 160 | 60 |
| C | 1.7 | 170 | 70 |
| D | 1.8 | 180 | 80 |

Cov(Height_m, Weight) = ? 

Let's compute:

$$
\begin{aligned}
\mu_{x_m} &= \frac{1.5+1.6+1.7+1.8}{4} = 1.65 \\
\mu_y &= \frac{50+60+70+80}{4} = 65 \\[4pt]
\text{Cov}(H_m, W) &= \frac{(1.5-1.65)(50-65) + (1.6-1.65)(60-65) + (1.7-1.65)(70-65) + (1.8-1.65)(80-65)}{4} \\
&= \frac{(-0.15)(-15) + (-0.05)(-5) + (0.05)(5) + (0.15)(15)}{4} \\
&= \frac{2.25 + 0.25 + 0.25 + 2.25}{4} \\
&= \frac{5}{4} = 1.25
\end{aligned}
$$

Now compute $\text{Cov}(H_{cm}, W)$:

$$
\begin{aligned}
\mu_{x_{cm}} &= \frac{150+160+170+180}{4} = 165 \\[4pt]
\text{Cov}(H_{cm}, W) &= \frac{(150-165)(50-65) + (160-165)(60-65) + (170-165)(70-65) + (180-165)(80-65)}{4} \\
&= \frac{(-15)(-15) + (-5)(-5) + (5)(5) + (15)(15)}{4} \\
&= \frac{225 + 25 + 25 + 225}{4} \\
&= \frac{500}{4} = 125
\end{aligned}
$$

**Cov changed from 1.25 to 125** just by switching meters to centimeters! The relationship between height and weight is the same, but the covariance number is completely different. We can't compare covariances across datasets.

### 7.8 Correlation Coefficient — The Fix

To solve the scaling problem, we **normalize** covariance by dividing by both standard deviations:

$$
\rho(X, Y) = \frac{\text{Cov}(X, Y)}{\sigma_x \cdot \sigma_y}
$$

**Why this works:** 
- $\sigma_x$ has the same units as $X$
- $\sigma_y$ has the same units as $Y$
- $\text{Cov}$ has units of $(\text{units of }X) \times (\text{units of }Y)$
- Dividing: $[X\text{-units} \times Y\text{-units}] / [X\text{-units} \times Y\text{-units}] = \textbf{unitless!}$

Let's verify with the height example:

$$
\begin{aligned}
\sigma_{x_m} &= \sqrt{\text{Var}(H_m)} = \sqrt{\frac{(-0.15)^2 + (-0.05)^2 + (0.05)^2 + (0.15)^2}{4}}
             = \sqrt{\frac{0.05}{4}} = \sqrt{0.0125} \approx 0.112 \\[4pt]
\sigma_{x_{cm}} &= \sqrt{\text{Var}(H_{cm})} = \sqrt{\frac{(-15)^2 + (-5)^2 + (5)^2 + (15)^2}{4}}
                = \sqrt{\frac{500}{4}} = \sqrt{125} \approx 11.18 \\[4pt]
\sigma_y &= \sqrt{\text{Var}(W)} = \sqrt{\frac{(-15)^2 + (-5)^2 + (5)^2 + (15)^2}{4}}
          = \sqrt{\frac{500}{4}} = \sqrt{125} \approx 11.18
\end{aligned}
$$

Using meters: $\rho = \dfrac{1.25}{0.112 \times 11.18} = \dfrac{1.25}{1.25} = 1$

Using cm: $\rho = \dfrac{125}{11.18 \times 11.18} = \dfrac{125}{125} = 1$

**Same answer!** $\rho = 1$ regardless of units. That's why we use correlation, not covariance, to compare relationships.

### 7.9 Properties of Correlation

- `-1 ≤ ρ ≤ 1` (proven below)
- ρ = 1: perfect **positive** linear relationship (points on a rising line)
- ρ = -1: perfect **negative** linear relationship (points on a falling line)
- ρ = 0: no **linear** relationship
- ρ is **symmetric**: ρ(X,Y) = ρ(Y,X)
- ρ is **unitless**: doesn't depend on measurement scale

### 7.10 Proof that -1 ≤ ρ ≤ 1 (Cauchy-Schwarz Inequality)

**Goal:** Show that $|\text{Cov}(X,Y)| \leq \sigma_x \cdot \sigma_y$, therefore $|\rho| \leq 1$.

**Step 1 — Consider the variance of a linear combination:**
For any real number $t$:
$$
\text{Var}(tX + Y) \geq 0 \quad (\text{variance is always non-negative})
$$

**Step 2 — Expand using variance properties:**
$$
\text{Var}(tX + Y) = t^2 \text{Var}(X) + 2t \cdot \text{Cov}(X, Y) + \text{Var}(Y) \geq 0
$$

**Step 3 — This is a quadratic in $t$:** $a \cdot t^2 + b \cdot t + c \geq 0$ for ALL $t$, where:
- $a = \text{Var}(X) \quad (\geq 0)$
- $b = 2 \cdot \text{Cov}(X,Y)$
- $c = \text{Var}(Y) \quad (\geq 0)$

For a quadratic to be $\geq 0$ for ALL $t$, its discriminant must be $\leq 0$ (the parabola never dips below zero):

$$
b^2 - 4ac \leq 0
$$

**Step 4 — Substitute $a$, $b$, $c$:**
$$
\begin{aligned}
(2 \cdot \text{Cov}(X,Y))^2 - 4 \cdot \text{Var}(X) \cdot \text{Var}(Y) &\leq 0 \\
4 \cdot \text{Cov}^2(X,Y) - 4 \cdot \text{Var}(X) \cdot \text{Var}(Y) &\leq 0
\end{aligned}
$$

**Step 5 — Divide by 4:**
$$
\text{Cov}^2(X,Y) \leq \text{Var}(X) \cdot \text{Var}(Y)
$$

**Step 6 — Take square root of both sides:**
$$
|\text{Cov}(X,Y)| \leq \sqrt{\text{Var}(X) \cdot \text{Var}(Y)}
$$
$$
|\text{Cov}(X,Y)| \leq \sigma_x \cdot \sigma_y
$$

**Step 7 — Divide both sides by $\sigma_x \cdot \sigma_y$:**
$$
\frac{|\text{Cov}(X,Y)|}{\sigma_x \cdot \sigma_y} \leq 1
$$
$$
|\rho| \leq 1
$$

Therefore: $\,-1 \leq \rho \leq 1\,$ ✅

**When does $\rho = 1$ or $\rho = -1$?**
When $Y = aX + b$ (perfect linear relationship). The sign of $a$ determines the sign of $\rho$.

### 7.11 Full Worked Example — Perfect Correlation

| X | Y |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 6 |

**Step 1 — Marginal expectations:**
$$
E[X] = \frac{1+2+3}{3} = 2,\qquad
E[Y] = \frac{2+4+6}{3} = 4
$$

**Step 2 — $E[XY]$:**
$$
E[XY] = \frac{1\times2 + 2\times4 + 3\times6}{3} = \frac{2+8+18}{3} = \frac{28}{3}
$$

**Step 3 — Covariance:**
$$
\text{Cov}(X,Y) = \frac{28}{3} - 2\times4 = \frac{28}{3} - \frac{24}{3} = \frac{4}{3}
$$

**Step 4 — Variances:**
$$
\begin{aligned}
E[X^2] &= \frac{1+4+9}{3} = \frac{14}{3}, \quad
\text{Var}(X) = \frac{14}{3} - 4 = \frac{2}{3}, \quad
\sigma_x = \sqrt{\frac{2}{3}} \\[4pt]
E[Y^2] &= \frac{4+16+36}{3} = \frac{56}{3}, \quad
\text{Var}(Y) = \frac{56}{3} - 16 = \frac{8}{3}, \quad
\sigma_y = \sqrt{\frac{8}{3}}
\end{aligned}
$$

**Step 5 — Correlation:**
$$
\rho = \frac{4/3}{\sqrt{2/3} \times \sqrt{8/3}}
     = \frac{4/3}{\sqrt{16/9}}
     = \frac{4/3}{4/3}
     = 1
$$

$Y = 2X$ exactly → perfect positive correlation.

### 7.12 Important Caveat — Correlation ≠ Causation

Even if ρ = 0.9:
- **Does NOT mean** X causes Y
- Could be a **third variable** Z causing both (e.g., ice cream sales and drowning both rise in summer — ρ > 0, but ice cream doesn't cause drowning)
- Could be **coincidence**
- Could be **reverse causation** (Y causes X)

ρ measures **linear association only**, not causation.

---

## Summary of Formulas in This Session

---

### Conditional Probability
$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$

> [!info]- First-principle derivation
> **Step 1 — Intuition:** When we know B occurred, the sample space shrinks from S to B. We want the fraction of B that also belongs to A.
>
> **Step 2 — Using counts (equally likely outcomes):**
> $$P(A \mid B) = \frac{|A \cap B|}{|B|}$$
>
> **Step 3 — Convert to probabilities** (divide numerator and denominator by $|S|$):
> $$P(A \mid B) = \frac{|A \cap B|/|S|}{|B|/|S|} = \frac{P(A \cap B)}{P(B)}$$
>
> This is a **definition** derived from the intuitive notion of "restricting the sample space."

---

### Multiplication Rule
$$P(A \cap B) = P(A \mid B) \cdot P(B)$$

> [!info]- First-principle derivation
> **Step 1 — Start with conditional probability definition:**
> $$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$
>
> **Step 2 — Multiply both sides by $P(B)$:**
> $$P(A \mid B) \cdot P(B) = P(A \cap B)$$
>
> **Step 3 — Rearrange:**
> $$P(A \cap B) = P(A \mid B) \cdot P(B)$$
>
> **Intuition:** The probability both A and B happen = (probability B happens) × (probability A happens given B already happened). This is the chain rule: first B occurs, then A occurs within B.

---

### Law of Total Probability
$$P(A) = \sum_i P(A \mid B_i) \cdot P(B_i)$$

> [!info]- First-principle derivation
> **Step 1 — Partition the sample space:** Let $B_1, B_2, ..., B_k$ be mutually exclusive and exhaustive events (they form a partition of S).
>
> **Step 2 — Express A as a union of disjoint parts:**
> $$A = (A \cap B_1) \cup (A \cap B_2) \cup ... \cup (A \cap B_k)$$
>
> Since the $B_i$'s are disjoint, the $A \cap B_i$'s are also disjoint.
>
> **Step 3 — Apply Axiom 3 (additivity):**
> $$P(A) = P(A \cap B_1) + P(A \cap B_2) + ... + P(A \cap B_k)$$
>
> **Step 4 — Apply multiplication rule to each term:**
> $$P(A) = P(A|B_1) \cdot P(B_1) + P(A|B_2) \cdot P(B_2) + ... + P(A|B_k) \cdot P(B_k)$$
> $$P(A) = \sum_i P(A \mid B_i) \cdot P(B_i)$$
>
> **Intuition:** The total probability of A is the weighted average of A's probability within each group, weighted by group size.

---

### Bayes' Theorem
$$P(B \mid A) = \frac{P(A \mid B) \cdot P(B)}{P(A)}$$

> [!info]- First-principle derivation
> **Step 1 — Start with the definition of $P(B \mid A)$:**
> $$P(B \mid A) = \frac{P(B \cap A)}{P(A)}$$
>
> **Step 2 — Joint probability is symmetric:** $P(B \cap A) = P(A \cap B)$
>
> **Step 3 — Rewrite $P(A \cap B)$ using the multiplication rule:**
> $$P(A \cap B) = P(A \mid B) \cdot P(B)$$
>
> **Step 4 — Substitute:**
> $$P(B \mid A) = \frac{P(A \mid B) \cdot P(B)}{P(A)}$$
>
> **General form** (when $P(A)$ is expanded using Law of Total Probability):
> $$P(B_i \mid A) = \frac{P(A \mid B_i) \cdot P(B_i)}{\sum_j P(A \mid B_j) \cdot P(B_j)}$$
>
> **Intuition:** Bayes' Theorem "inverts" the conditional — it tells us how to update our belief about B after seeing evidence A. The posterior (updated belief) = likelihood × prior / evidence.

---

### Conditional Expectation
$$E[X \mid B] = \sum_i x_i \cdot P(X = x_i \mid B)$$

> [!info]- First-principle derivation
> **Step 1 — Recall regular expectation:** $E[X] = \sum_i x_i \cdot P(X = x_i)$
> This is the **probability-weighted average** of X's values.
>
> **Step 2 — When we know B occurred,** the probabilities change. Replace regular probabilities with conditional probabilities (since B is now the restricted sample space):
> $$E[X \mid B] = \sum_i x_i \cdot P(X = x_i \mid B)$$
>
> **Step 3 — Expanding $P(X = x_i \mid B)$:**
> $$E[X \mid B] = \sum_i x_i \cdot \frac{P(X = x_i \cap B)}{P(B)}$$
>
> This is simply the **same expectation formula** but using the conditional distribution instead of the marginal distribution.

---

### Law of Total Expectation
$$E[X] = E[\,E[X \mid Y]\,]$$

> [!info]- First-principle derivation
> **Step 1 — Start with definition:**
> $$E[X] = \sum_i x_i \cdot P(X = x_i)$$
>
> **Step 2 — Use Y to partition the space:**
> $$P(X = x_i) = \sum_j P(X = x_i, Y = y_j)$$
>
> **Step 3 — Substitute and rearrange:**
> $$E[X] = \sum_i x_i \cdot \sum_j P(X = x_i, Y = y_j) = \sum_j \sum_i x_i \cdot P(X = x_i, Y = y_j)$$
>
> **Step 4 — Use $P(X=x_i, Y=y_j) = P(X=x_i \mid Y=y_j) \cdot P(Y=y_j)$:**
> $$E[X] = \sum_j \left[\sum_i x_i \cdot P(X=x_i \mid Y=y_j)\right] \cdot P(Y=y_j)$$
>
> **Step 5 — Recognize the inner sum as $E[X \mid Y = y_j]$:**
> $$E[X] = \sum_j E[X \mid Y = y_j] \cdot P(Y = y_j)$$
>
> **Step 6 — The right side is the expectation of $E[X \mid Y]$ over Y:**
> $$E[X] = E[\,E[X \mid Y]\,]$$
>
> **Intuition:** The overall average = weighted average of group averages.

---

### Law of Total Variance
$$\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$$

> [!info]- First-principle derivation
> **Step 1 — Start with the shortcut formula:**
> $$\text{Var}(X) = E[X^2] - (E[X])^2$$
>
> **Step 2 — Apply Law of Total Expectation to both terms:**
> $$E[X^2] = E[\,E[X^2 \mid Y]\,], \qquad E[X] = E[\,E[X \mid Y]\,]$$
>
> **Step 3 — Substitute:**
> $$\text{Var}(X) = E[\,E[X^2 \mid Y]\,] - (E[\,E[X \mid Y]\,])^2$$
>
> **Step 4 — Express $E[X^2 \mid Y]$ using conditional variance:**
> $$E[X^2 \mid Y] = \text{Var}(X \mid Y) + (E[X \mid Y])^2$$
>
> **Step 5 — Substitute this in:**
> $$\text{Var}(X) = E[\text{Var}(X \mid Y) + (E[X \mid Y])^2] - (E[E[X \mid Y]])^2$$
>
> **Step 6 — Split the expectation:**
> $$\text{Var}(X) = E[\text{Var}(X \mid Y)] + E[(E[X \mid Y])^2] - (E[E[X \mid Y]])^2$$
>
> **Step 7 — Recognize the last two terms as $\text{Var}(E[X \mid Y])$:**
> $$\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$$
>
> **Intuition:** Total variance = average variance within groups + variance of group means.

---

### Covariance
$$\text{Cov}(X,Y) = E[XY] - E[X] \cdot E[Y]$$

> [!info]- First-principle derivation
> **Step 1 — Start with definition:**
> $$\text{Cov}(X,Y) = E[(X - \mu_x)(Y - \mu_y)], \quad \mu_x = E[X],\; \mu_y = E[Y]$$
>
> **Step 2 — Expand the product:**
> $$\text{Cov}(X,Y) = E[\,XY - X\mu_y - \mu_x Y + \mu_x \mu_y\,]$$
>
> **Step 3 — Apply linearity of expectation:**
> $$\text{Cov}(X,Y) = E[XY] - \mu_y E[X] - \mu_x E[Y] + \mu_x \mu_y$$
>
> **Step 4 — Substitute $E[X] = \mu_x$, $E[Y] = \mu_y$:**
> $$\text{Cov}(X,Y) = E[XY] - \mu_y \mu_x - \mu_x \mu_y + \mu_x \mu_y$$
>
> **Step 5 — Simplify:**
> $$\text{Cov}(X,Y) = E[XY] - \mu_x \mu_y = E[XY] - E[X]E[Y]$$
>
> **Intuition:** Covariance measures whether X and Y move together. The shortcut formula says: find the average of the product, then subtract the product of the averages. If they're independent, $E[XY] = E[X]E[Y]$, so Cov = 0.

---

### Correlation
$$\rho = \frac{\text{Cov}(X,Y)}{\sigma_x \cdot \sigma_y}$$

> [!info]- First-principle derivation
> **Step 1 — The problem with covariance:** Covariance changes with units (e.g., measuring height in meters vs centimeters changes Cov by 100×). We need a **unitless** measure.
>
> **Step 2 — Solution:** Divide covariance by the product of standard deviations:
> $$\rho = \frac{\text{Cov}(X,Y)}{\sigma_x \cdot \sigma_y}$$
>
> **Why this works:** If X is in meters, $\sigma_x$ is also in meters. Cov is in meter·kg. Dividing: (meter·kg)/(meter·kg) = unitless.
>
> **Step 3 — Range proof (Cauchy-Schwarz):**
> For any t: $\text{Var}(tX + Y) = t^2 \text{Var}(X) + 2t \cdot \text{Cov}(X,Y) + \text{Var}(Y) \geq 0$
> This quadratic in t has discriminant $\leq 0$:
> $$(2\text{Cov})^2 - 4\text{Var}(X)\text{Var}(Y) \leq 0$$
> $$\text{Cov}^2 \leq \text{Var}(X) \cdot \text{Var}(Y)$$
> $$|\text{Cov}| \leq \sigma_x \cdot \sigma_y$$
> $$\frac{|\text{Cov}|}{\sigma_x \cdot \sigma_y} \leq 1 \quad \Rightarrow \quad -1 \leq \rho \leq 1$$
>
> **Intuition:** $\rho$ measures the **strength and direction** of a linear relationship, independent of measurement units.

---

---

## Practice Problems

### Formula Revision — Before You Begin

| Concept | Formula |
|---|---|
| Conditional Probability | $P(A\|B) = \dfrac{P(A \cap B)}{P(B)}$ |
| Multiplication Rule | $P(A \cap B) = P(A\|B) \cdot P(B)$ |
| Law of Total Probability | $P(A) = \sum_i P(A\|B_i) \cdot P(B_i)$ |
| Bayes' Theorem | $P(B\|A) = \dfrac{P(A\|B) \cdot P(B)}{P(A)}$ |
| Conditional Expectation | $E[X\|B] = \sum_i x_i \cdot P(X=x_i\|B)$ |
| Law of Total Expectation | $E[X] = E[E[X\|Y]]$ |
| Covariance | $\text{Cov}(X,Y) = E[XY] - E[X]\cdot E[Y]$ |
| Correlation | $\rho = \dfrac{\text{Cov}(X,Y)}{\sigma_x \cdot \sigma_y}$ |
| Law of Total Variance | $\text{Var}(X) = E[\text{Var}(X\|Y)] + \text{Var}(E[X\|Y])$ |

---

### 🟢 EASY (Start Here)

---

#### Problem E1: Conditional Probability — Card Draw

A standard 52-card deck. You draw one card.

a) What's the probability it's a King?
b) Given the card is a face card (Jack, Queen, King), what's the probability it's a King?
c) Given the card is a heart, what's the probability it's a King?

> [!success]- Solution
> a) $P(\text{King}) = \dfrac{4}{52} = \dfrac{1}{13}$
> b) Face cards: 3 per suit × 4 suits = 12. $P(\text{King}|\text{Face}) = \dfrac{4}{12} = \dfrac{1}{3}$
> c) Hearts: 13 cards. $P(\text{King}|\text{Heart}) = \dfrac{1}{13}$
> Notice: King and Heart are independent since $P(\text{King}|\text{Heart}) = P(\text{King}) = 1/13$

---

#### Problem E2: Bayes — Factory Defects

A factory produces widgets. 5% of all widgets are defective. The quality test:
- Detects 98% of defective widgets (true positive)
- Falsely flags 4% of good widgets as defective (false positive)

A widget is tested and flagged as defective. What's the probability it's actually defective?

> [!success]- Solution
> Let D = defective, T = test positive.
> $P(D) = 0.05$, $P(T|D) = 0.98$, $P(T|D') = 0.04$
> $P(T) = 0.98×0.05 + 0.04×0.95 = 0.049 + 0.038 = 0.087$
> $P(D|T) = 0.98×0.05 / 0.087 = 0.049/0.087 \approx 0.5632$ (56.32%)
> Even with a good test, only ~56% of flagged items are actually defective due to low base rate.

---

#### Problem E3: Joint & Marginal from a Table

| X\Y | 1 | 2 | 3 |
|---|---|---|---|
| **0** | 0.1 | 0.2 | 0.1 |
| **1** | 0.15 | 0.05 | 0.4 |

Find:
a) $P(X=0, Y=2)$
b) $P(X=0)$ and $P(Y=2)$
c) $P(X=1 \mid Y=2)$

> [!success]- Solution
> a) $P(X=0, Y=2) = 0.2$
> b) $P(X=0) = 0.1+0.2+0.1 = 0.4$
> $P(Y=2) = 0.2+0.05 = 0.25$
> c) $P(X=1 \mid Y=2) = P(X=1, Y=2)/P(Y=2) = 0.05/0.25 = 0.2$

---

### 🟡 MEDIUM (Once You're Comfortable)

---

#### Problem M1: Bayes with 3 Machines

A factory has 3 machines producing items:
- Machine A: 50% of output, 2% defective
- Machine B: 30% of output, 4% defective
- Machine C: 20% of output, 1% defective

An item is randomly selected and found defective. What's the probability it came from Machine B?

> [!success]- Solution
> Let D = defective.
> $P(A) = 0.5$, $P(B) = 0.3$, $P(C) = 0.2$
> $P(D|A) = 0.02$, $P(D|B) = 0.04$, $P(D|C) = 0.01$
> $P(D) = 0.02×0.5 + 0.04×0.3 + 0.01×0.2 = 0.01 + 0.012 + 0.002 = 0.024$
> $P(B|D) = 0.04×0.3 / 0.024 = 0.012/0.024 = 0.5$ (50%)

---

#### Problem M2: Conditional Expectation — Two Dice

Roll two fair dice. Let X = their sum.

a) Find $E[X \mid \text{first die is 4}]$
b) Find $E[X \mid \text{first die is odd}]$
c) Given that the sum is even, find $E[X \mid \text{even sum}]$

> [!success]- Solution
> a) First die = 4. Second die: {1,...,6} equally likely.
> $E[X|\text{first}=4] = (4+1)+(4+2)+...+(4+6) / 6 = (5+6+7+8+9+10)/6 = 45/6 = 7.5$
> b) First die odd: {1,3,5}. For each, second die avg = 3.5.
> $E[X|\text{first odd}] = (1+3.5 + 3+3.5 + 5+3.5)/3 = (4.5+6.5+8.5)/3 = 19.5/3 = 6.5$
> c) P(even sum) = 18/36 = 0.5. Even sums: 2,4,6,8,10,12.
> By symmetry of fair dice: $E[X|\text{even sum}] = 7$ (same as unconditional $E[X]$)

---

#### Problem M3: Covariance — Two Assets

Returns of Stock A (X) and Stock B (Y) have joint distribution:

| X\Y | -5% | 0% | 10% |
|---|---|---|---|
| **-3%** | 0.1 | 0.05 | 0.05 |
| **2%** | 0.1 | 0.2 | 0.1 |
| **8%** | 0.05 | 0.05 | 0.3 |

Find $\text{Cov}(X, Y)$ and interpret.

> [!success]- Solution
> **Marginals:**
> $P(X=-3) = 0.1+0.05+0.05 = 0.2$
> $P(X=2) = 0.1+0.2+0.1 = 0.4$
> $P(X=8) = 0.05+0.05+0.3 = 0.4$
> $P(Y=-5) = 0.1+0.1+0.05 = 0.25$
> $P(Y=0) = 0.05+0.2+0.05 = 0.30$
> $P(Y=10) = 0.05+0.1+0.3 = 0.45$
>
> **Expectations:**
> $E[X] = -3×0.2 + 2×0.4 + 8×0.4 = -0.6 + 0.8 + 3.2 = 3.4\%$
> $E[Y] = -5×0.25 + 0×0.30 + 10×0.45 = -1.25 + 0 + 4.5 = 3.25\%$
>
> **$E[XY]$:**
> $= (-3)(-5)(0.1) + (-3)(0)(0.05) + (-3)(10)(0.05)$
> $+ (2)(-5)(0.1) + (2)(0)(0.2) + (2)(10)(0.1)$
> $+ (8)(-5)(0.05) + (8)(0)(0.05) + (8)(10)(0.3)$
> $= 1.5 + 0 + (-1.5) + (-1) + 0 + 2 + (-2) + 0 + 24 = 23$
>
> $\text{Cov}(X,Y) = 23 - (3.4)(3.25) = 23 - 11.05 = 11.95$
> **Interpretation:** Strong positive — when X is high, Y tends to be high too.

---

#### Problem M4: Law of Total Expectation — Shipping

A warehouse ships packages via 3 carriers:
- Carrier 1: 40% of packages, avg delivery = 2 days
- Carrier 2: 35% of packages, avg delivery = 4 days
- Carrier 3: 25% of packages, avg delivery = 5 days

a) Find expected delivery time $E[D]$
b) Each carrier's variance: $\text{Var}(D|C_1)=1$, $\text{Var}(D|C_2)=2$, $\text{Var}(D|C_3)=3$. Find $\text{Var}(D)$ using Law of Total Variance.

> [!success]- Solution
> a) $E[D] = 2×0.4 + 4×0.35 + 5×0.25 = 0.8 + 1.4 + 1.25 = 3.45$ days
>
> b) **$E[\text{Var}(D|\text{carrier})]$** = $1×0.4 + 2×0.35 + 3×0.25 = 0.4 + 0.7 + 0.75 = 1.85$
>
> **$\text{Var}(E[D|\text{carrier}])$:**
> $E[D|\text{carrier}]$ takes values {2, 4, 5} with probs {0.4, 0.35, 0.25}
> $E[(E[D|C])^2] = 4×0.4 + 16×0.35 + 25×0.25 = 1.6 + 5.6 + 6.25 = 13.45$
> $(E[E[D|C]])^2 = (3.45)^2 = 11.9025$
> $\text{Var}(E[D|C]) = 13.45 - 11.9025 = 1.5475$
>
> $\text{Var}(D) = 1.85 + 1.5475 = 3.3975$ days²

---

#### Problem M5: Sequential Bayes — Two-Stage Test

A disease affects 1% of people. A two-stage testing protocol:
- **Stage 1:** Sensitivity = 90%, Specificity = 80%
- **Stage 2 (only if Stage 1 positive):** Sensitivity = 99%, Specificity = 95%

What's the probability a person has the disease given they tested positive on **both** stages?
*Assume tests are independent given disease status.*

> [!success]- Solution
> Let D = disease, $T_1^+$ = Stage 1 positive, $T_2^+$ = Stage 2 positive.
> $P(D) = 0.01$, $P(H) = 0.99$
> $P(T_1^+|D) = 0.9$, $P(T_1^+|H) = 0.2$
> $P(T_2^+|D) = 0.99$, $P(T_2^+|H) = 0.05$
>
> Since tests independent given disease status:
> $P(T_1^+, T_2^+ | D) = 0.9 × 0.99 = 0.891$
> $P(T_1^+, T_2^+ | H) = 0.2 × 0.05 = 0.01$
>
> $P(T_1^+, T_2^+) = 0.891×0.01 + 0.01×0.99 = 0.00891 + 0.0099 = 0.01881$
>
> $P(D | T_1^+, T_2^+) = 0.891×0.01 / 0.01881 = 0.00891/0.01881 ≈ 0.4737$ (47.37%)
>
> Two positive tests jump the probability from 1% → 47.37%.

---

#### Problem M6: Covariance — Sum and Difference

Let X and Y be random variables with $\text{Var}(X) = 4$, $\text{Var}(Y) = 9$, and $\text{Cov}(X,Y) = 3$.

Define $U = X + Y$ and $V = X - Y$.

a) Find $\text{Cov}(U, V)$
b) Find $\rho_{UV}$ (correlation between U and V)
c) What happens to $\rho_{UV}$ if $\text{Cov}(X,Y) = 0$?

> [!success]- Solution
> a) $\text{Cov}(U,V) = \text{Cov}(X+Y, X-Y)$
> $= \text{Cov}(X,X) - \text{Cov}(X,Y) + \text{Cov}(Y,X) - \text{Cov}(Y,Y)$
> $= \text{Var}(X) - \text{Cov}(X,Y) + \text{Cov}(X,Y) - \text{Var}(Y)$
> $= 4 - 3 + 3 - 9 = -5$
>
> b) $\text{Var}(U) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y) = 4 + 9 + 6 = 19$
> $\text{Var}(V) = \text{Var}(X) + \text{Var}(Y) - 2\text{Cov}(X,Y) = 4 + 9 - 6 = 7$
> $\sigma_U = \sqrt{19}$, $\sigma_V = \sqrt{7}$
> $\rho_{UV} = -5 / (\sqrt{19}\sqrt{7}) \approx -5 / 11.53 \approx -0.434$
>
> c) If $\text{Cov}(X,Y) = 0$:
> $\text{Cov}(U,V) = 4 - 0 + 0 - 9 = -5$ (same!)
> $\text{Var}(U) = 13$, $\text{Var}(V) = 13$
> $\rho_{UV} = -5/13 \approx -0.385$
> So U and V are always negatively correlated regardless of X,Y relationship.

---

### 🔴 TOUGH (For When You're Feeling Sharp)

---

#### Problem T1: Bayes — Monty Hall with 4 Doors

A game show has 4 doors. Behind 1 door is a car, behind the other 3 are goats.
You pick a door. The host (who knows where the car is) opens 2 doors that have goats.

a) Should you switch to the remaining unopened door? What's your probability of winning if you switch vs stay?
b) Generalize: for n doors, host opens $n-2$ goat doors. Probability of winning by switching?

> [!success]- Solution
> a) Let C = car behind your initial pick, G = goat behind your pick.
> $P(C) = 1/4$, $P(G) = 3/4$
>
> If you initially picked car (prob 1/4): host opens 2 goats, the remaining door has goat → switching loses. Winning by switching = 0.
> If you initially picked goat (prob 3/4): host opens the other 2 goats, the remaining door has car → switching wins. Winning by switching = 1.
>
> $P(\text{win by switching}) = P(G) × 1 + P(C) × 0 = 3/4$
> $P(\text{win by staying}) = P(C) = 1/4$
>
> **Always switch!** 75% vs 25%.
>
> b) For n doors: $P(C) = 1/n$, $P(G) = (n-1)/n$
> $P(\text{win by switching}) = (n-1)/n × 1 + 1/n × 0 = (n-1)/n$
> As n grows, switching is almost surely a win.

---

#### Problem T2: Law of Total Variance — Portfolio

A portfolio invests in 3 sectors:
- **Tech (50%):** $E[R] = 12\%$, $\text{Var}(R) = 25$
- **Healthcare (30%):** $E[R] = 8\%$, $\text{Var}(R) = 9$
- **Energy (20%):** $E[R] = 5\%$, $\text{Var}(R) = 4$

a) Find the portfolio's expected return $E[R]$
b) Using Law of Total Variance, decompose total risk into within-sector and between-sector components
c) Which component dominates? What does this mean for diversification?

> [!success]- Solution
> a) $E[R] = 12×0.5 + 8×0.3 + 5×0.2 = 6 + 2.4 + 1 = 9.4\%$
>
> b) **$E[\text{Var}(R|\text{sector})]$** (within-sector):
> $= 25×0.5 + 9×0.3 + 4×0.2 = 12.5 + 2.7 + 0.8 = 16$
>
> **$\text{Var}(E[R|\text{sector}])$** (between-sector):
> $E[R|\text{sector}]$: {12, 8, 5} with probs {0.5, 0.3, 0.2}
> $E[(E[R|S])^2] = 144×0.5 + 64×0.3 + 25×0.2 = 72 + 19.2 + 5 = 96.2$
> $(E[E[R|S]])^2 = (9.4)^2 = 88.36$
> $\text{Var}(E[R|S]) = 96.2 - 88.36 = 7.84$
>
> $\text{Var}(R) = 16 + 7.84 = 23.84$
>
> c) Within-sector fraction: $16/23.84 \approx 0.671$ (67.1%)
> Between-sector fraction: $7.84/23.84 \approx 0.329$ (32.9%)
>
> **Within-sector risk dominates** — most volatility comes from sector-specific fluctuations, not the difference between sectors. Diversifying across sectors helps (between-sector component), but you can't eliminate within-sector risk.

---

#### Problem T3: Correlation and Linear Transformation

Let X and Y be random variables with:
$$E[X] = 10,\; \text{Var}(X) = 16,\; E[Y] = 5,\; \text{Var}(Y) = 25,\; \text{Cov}(X,Y) = 12$$

Define: $U = 2X + 3$, $V = -Y + 1$

a) Find $\text{Cov}(U, V)$ and $\rho_{UV}$
b) If $W = aX + bY$, find values of $a, b$ (not both zero) such that $\text{Cov}(W, X) = 0$ and $E[W] = 0$
c) Prove that $|\rho_{XY}| \leq 1$ using the fact that $\text{Var}(tX + Y) \geq 0$ for all t

> [!success]- Solution
> a) $\text{Cov}(U, V) = \text{Cov}(2X+3, -Y+1)$
> Constants don't affect covariance: $\text{Cov}(2X, -Y) = -2\cdot\text{Cov}(X,Y) = -2×12 = -24$
>
> $\text{Var}(U) = \text{Var}(2X+3) = 4\text{Var}(X) = 64$, $\sigma_U = 8$
> $\text{Var}(V) = \text{Var}(-Y+1) = \text{Var}(Y) = 25$, $\sigma_V = 5$
>
> $\rho_{UV} = -24 / (8×5) = -24/40 = -0.6$
>
> b) $\text{Cov}(W, X) = \text{Cov}(aX + bY, X) = a\text{Var}(X) + b\text{Cov}(Y,X) = 16a + 12b = 0$
> $\Rightarrow 4a + 3b = 0 \Rightarrow b = -\frac{4}{3}a$
>
> $E[W] = aE[X] + bE[Y] = 10a + 5b = 0$
> Substitute $b = -\frac{4}{3}a$: $10a + 5(-\frac{4}{3}a) = 10a - \frac{20}{3}a = \frac{10}{3}a = 0 \Rightarrow a = 0$
> If $a = 0$, then $b = 0$. **No non-trivial solution** — can't simultaneously satisfy both constraints.
>
> c) For any t: $\text{Var}(tX + Y) = t^2\text{Var}(X) + 2t\text{Cov}(X,Y) + \text{Var}(Y) \geq 0$
> This quadratic in t has discriminant $\leq 0$ (since it never dips below 0):
> $(2\text{Cov})^2 - 4\text{Var}(X)\text{Var}(Y) \leq 0$
> $\text{Cov}^2 \leq \text{Var}(X)\text{Var}(Y)$
> $|\text{Cov}| \leq \sigma_X\sigma_Y$
> $\frac{|\text{Cov}|}{\sigma_X\sigma_Y} \leq 1 \Rightarrow |\rho_{XY}| \leq 1$ ✓

---

### Difficulty Progress Map

```
E1  E2  E3  →  M1  M2  M3  M4  M5  M6  →  T1  T2  T3
🟢  🟢  🟢      🟡  🟡  🟡  🟡  🟡  🟡      🔴  🔴  🔴
```

Don't jump to Tough until you've comfortably solved all Easy and Medium problems.

---

---

## Ready for Session 003?

Reply **"done session-002"** when you've studied everything and solved the practice problems. Next: **Session 003 — Random Variables & Probability Distributions** (PMF, PDF, CDF, Bernoulli, Binomial, Uniform, etc.)
