# Session 001 — Counting & Probability Foundations

> **📅 Expected:** Jun 13 – Jun 17 | **Buffer:** +13 days 🟢 | **Status:** ✅ Completed (doc ready day-of)

## Topics Covered in This Session
- Fundamental Principle of Counting
- Permutations (with and without repetition)
- Combinations
- Probability Axioms
- Sample Space & Events
- Independent & Mutually Exclusive Events

---

## Part 1: Fundamental Principle of Counting

### The Multiplication Principle

**Statement:** If a task can be broken into two independent steps, where step 1 has `m` ways and step 2 has `n` ways, then the total number of ways to complete the task is `m × n`.

**Generalized:** If there are `k` steps with `n₁, n₂, ..., nₖ` ways respectively, the total is:
```
Total = n₁ × n₂ × ... × nₖ
```

**Example:** How many 3-digit numbers can be formed using digits 1-9 if repetition is allowed?
- Step 1 (hundreds): 9 choices (1-9)
- Step 2 (tens): 9 choices (1-9)
- Step 3 (units): 9 choices (1-9)
- Total = 9 × 9 × 9 = 729

**Example:** How many 3-digit numbers if repetition is NOT allowed?
- Step 1: 9 choices
- Step 2: 8 choices (one digit already used)
- Step 3: 7 choices
- Total = 9 × 8 × 7 = 504

---

## Part 2: Permutations (Ordered Arrangements)

### Definition
A permutation is an arrangement of objects in a **specific order**. The number of permutations of `n` distinct objects taken `r` at a time is denoted by:
```
P(n, r)  or  ⁿPᵣ  or  Pᵣⁿ
```

### Derivation of the Formula

We want to arrange `r` objects from `n` distinct objects where order matters.

Using the multiplication principle:

| Position | Items already used | Remaining choices |
|---|---|---|
| 1st | 0 | `n - 0` = `n` |
| 2nd | 1 | `n - 1` |
| 3rd | 2 | `n - 2` |
| ... | ... | ... |
| r-th | `(r - 1)` | `n - (r - 1)` = **`n - r + 1`** |

The `+1` is because we've only placed `(r - 1)` items so far, not `r`.

**Edge case check:** `n = 10, r = 10`
- Last position: `10 - 10 + 1 = 1` ✅ (only 1 item left)

**Edge case check:** `n = 10, r = 1`
- Only position: `10 - 1 + 1 = 10` ✅ (all 10 available)

So the product becomes:
```
P(n, r) = n × (n - 1) × (n - 2) × ... × (n - r + 1)
```

Multiply and divide by `(n - r)!`:
```
P(n, r) = [n × (n - 1) × ... × (n - r + 1) × (n - r)!] / (n - r)!
        = n! / (n - r)!
```

**Final formula:**
```
P(n, r) = n! / (n - r)!
```

### Derivation of n! (factorial)
```
n! = n × (n - 1) × (n - 2) × ... × 3 × 2 × 1
```
Convention: `0! = 1`

This comes from the empty product — there is exactly 1 way to arrange 0 objects.

### Special Cases
- `P(n, 0) = 1` (only one way to choose nothing)
- `P(n, 1) = n`
- `P(n, n) = n!` (arranging all n objects)

### Example with Derivation

**Problem:** How many ways to arrange 3 books (A, B, C) on a shelf from 5 books {1, 2, 3, 4, 5}?

**Manual listing reasoning:**
- Slot 1 (leftmost): 5 possible books
- Slot 2: 4 remaining books
- Slot 3: 3 remaining books
- Total = 5 × 4 × 3 = 60

**Using formula:**
```
P(5, 3) = 5! / (5 - 3)! = 5! / 2! = 120 / 2 = 60
```

### Permutations with Repetition

When repetition is allowed, each position has `n` choices regardless of previous picks:
```
Total = nʳ
```

**Example:** 4-digit PIN from digits 0-9 with repetition = `10⁴ = 10,000`

### Permutations of Identical Objects

If you have `n` objects where `n₁` are of type 1, `n₂` of type 2, ..., `nₖ` of type k:
```
Total = n! / (n₁! × n₂! × ... × nₖ!)
```

**Derivation:** Among the `n!` arrangements of distinct objects, the identical ones swap without creating new arrangements, so we divide by the factorial of each group's size.

**Example:** Number of distinct arrangements of "MISSISSIPPI":
- M: 1, I: 4, S: 4, P: 2
- Total = 11! / (1! × 4! × 4! × 2!)
- = 39916800 / (1 × 24 × 24 × 2)
- = 39916800 / 1152
- = 34650

---

## Part 3: Combinations (Unordered Selections)

### Definition
A combination is a selection of objects where **order does NOT matter**. The number of combinations of `n` distinct objects taken `r` at a time is denoted by:
```
C(n, r)  or  ⁿCᵣ  or  (ⁿᵣ)
```

### Derivation of the Formula — Step by Step

#### Step 1: Start with a concrete example

Take 5 letters: {A, B, C, D, E}. We want to **select** 3 letters (order doesn't matter).

Let's first list how many **ordered arrangements** (permutations) of 3 letters exist:
```
P(5, 3) = 5! / 2! = 120/2 = 60
```

That means there are 60 ordered triplets like (A,B,C), (A,C,B), (B,A,C), etc.

#### Step 2: Group permutations that belong to the same combination

Consider the set {A, B, C}. How many different ways can we arrange these 3 letters?
```
(A,B,C), (A,C,B), (B,A,C), (B,C,A), (C,A,B), (C,B,A)  →  6 ways
```

That's `3! = 6`. So all 6 permutations of {A, B, C} correspond to the **same** combination — because in a selection, {A, B, C} is just {A, B, C} regardless of order.

#### Step 3: The key insight

Every combination of 3 letters produces exactly `3!` permutations (all possible orderings of those 3 letters).

So:
```
Total Permutations = (Number of Combinations) × (Orderings per Combination)
```

Which gives us:
```
P(5, 3) = C(5, 3) × 3!
```

#### Step 4: Solve for C(5, 3)

```
C(5, 3) = P(5, 3) / 3!
        = 60 / 6
        = 10
```

Indeed, the 10 combinations of 3 from {A, B, C, D, E} are:
```
{A,B,C}, {A,B,D}, {A,B,E}, {A,C,D}, {A,C,E},
{A,D,E}, {B,C,D}, {B,C,E}, {B,D,E}, {C,D,E}
```

#### Step 5: Generalize to n and r

The same logic applies for any `n` and `r`:

- `P(n, r)` = total ordered arrangements of r items from n
- Each combination of r items produces `r!` ordered arrangements
- Therefore:

```
P(n, r) = C(n, r) × r!
```

#### Step 6: Rearrange to get the combination formula

```
C(n, r) = P(n, r) / r!
        = [n! / (n - r)!] / r!
        = n! / [r! × (n - r)!]
```

**Final formula:**
```
C(n, r) = n! / [r! × (n - r)!]
```

#### Step 7: Verify with edge cases

| Case | Formula | Result | Interpretation |
|---|---|---|---|
| `C(n, 0)` | `n! / [0! × n!]` | 1 | One way to select nothing |
| `C(n, 1)` | `n! / [1! × (n-1)!]` | n | Select any 1 item |
| `C(n, n)` | `n! / [n! × 0!]` | 1 | One way to select all |
| `C(5, 2)` | `5! / [2! × 3!] = 120/12` | 10 | Same as C(5, 3) |

### Key Properties

| Property | Formula | Reason |
|---|---|---|
| Symmetry | `C(n, r) = C(n, n - r)` | Choosing r to keep = choosing n-r to discard |
| Boundary | `C(n, 0) = C(n, n) = 1` | Only one way: pick none or all |
| Identity | `C(n, r) = C(n-1, r-1) + C(n-1, r)` | Pascal's rule |

### Derivation of Pascal's Identity

`C(n, r) = C(n-1, r-1) + C(n-1, r)`

**Proof (combinatorial):**
Consider a specific object X among the `n`. Every r-combination either:
1. **Includes X:** We need `r-1` more from the remaining `n-1` objects → `C(n-1, r-1)`
2. **Excludes X:** We need all `r` from the remaining `n-1` objects → `C(n-1, r)`

Since these are mutually exclusive and cover all cases:
```
C(n, r) = C(n-1, r-1) + C(n-1, r)
```

This is why Pascal's Triangle works:
```
        1
      1   1
    1   2   1
  1   3   3   1
1   4   6   4   1
```

### Example with Derivation

**Problem:** From a group of 20 students, how many ways to select a committee of 3?

```
C(20, 3) = 20! / (3! × 17!)
         = (20 × 19 × 18) / (3 × 2 × 1)
         = 6840 / 6
         = 1140
```

**Why divide by 3!?** Because for any chosen set of 3 students (say Alice, Bob, Charlie), the permutations (A,B,C), (A,C,B), (B,A,C), (B,C,A), (C,A,B), (C,B,A) are all the **same committee** — order irrelevant. So we take `P(20,3)=6840` and divide by `3!=6` to remove overcounting.

### Quick Comparison Table

| | Permutation | Combination |
|---|---|---|
| Order matters? | Yes | No |
| Formula | `n!/(n-r)!` | `n!/[r!(n-r)!]` |
| Example: 5 books pick 3 | 60 arrangements | 10 selections |
| Real-world | Ranking, passwords | Teams, lottery |

---

## Part 4: Probability Foundations

### Key Terminology

| Term | Definition | Example |
|---|---|---|
| **Experiment** | Any process with uncertain outcome | Rolling a die |
| **Outcome** | A single result of the experiment | Getting a 4 |
| **Sample Space (S)** | Set of **all** possible outcomes | `{1, 2, 3, 4, 5, 6}` |
| **Event (E)** | A subset of the sample space | `{2, 4, 6}` ("even") |
| **Null Event (∅)** | Empty set, impossible event | Rolling a 7 |

### Probability Definition (Relative Frequency)

If an experiment is repeated `n` times and event E occurs `f` times:
```
P(E) = lim_{n→∞} f/n
```

For a finite sample space with equally likely outcomes:
```
P(E) = |E| / |S| = (Number of favorable outcomes) / (Total outcomes)
```

### The Three Kolmogorov Axioms

These are the **foundation of all probability theory**:

#### Axiom 1: Non-negativity
```
P(E) ≥ 0  for any event E
```
Probability cannot be negative.

#### Axiom 2: Normalization
```
P(S) = 1
```
The probability that **something** happens in the sample space is 100%.

#### Axiom 3: Finite Additivity
If events `A₁, A₂, A₃, ...` are **mutually exclusive** (no two can occur together):
```
P(A₁ ∪ A₂ ∪ A₃ ∪ ...) = P(A₁) + P(A₂) + P(A₃) + ...
```

### Theorems Derived from Axioms

#### Theorem 1: Probability of the complement
```
P(A') = 1 - P(A)   where A' = "not A"
```
**Proof:**
- A and A' are mutually exclusive (can't both happen)
- A ∪ A' = S (they cover everything)
- By Axiom 3: P(A) + P(A') = P(S)
- By Axiom 2: P(S) = 1
- Therefore: P(A) + P(A') = 1 → P(A') = 1 - P(A)

#### Theorem 2: Probability of impossible event
```
P(∅) = 0
```
**Proof:**
- ∅' = S
- P(∅) = 1 - P(S) = 1 - 1 = 0

#### Theorem 3: Inclusion-Exclusion (for ANY two events)
```
P(A ∪ B) = P(A) + P(B) - P(A ∩ B)
```
**Proof:**
- A ∪ B can be partitioned into three mutually exclusive sets: (A∩B'), (A∩B), (A'∩B)
- P(A ∪ B) = P(A∩B') + P(A∩B) + P(A'∩B)
- P(A) = P(A∩B') + P(A∩B)
- P(B) = P(A'∩B) + P(A∩B)
- Adding P(A) + P(B) = P(A∩B') + P(A'∩B) + 2·P(A∩B)
- So P(A) + P(B) - P(A∩B) = P(A∩B') + P(A'∩B) + P(A∩B) = P(A ∪ B)

#### Theorem 4: For three events
```
P(A ∪ B ∪ C) = P(A) + P(B) + P(C)
             - P(A∩B) - P(B∩C) - P(A∩C)
             + P(A∩B∩C)
```

---

## Part 5: Types of Events — Deep Dive

### Mutually Exclusive Events — Venn Diagram

**Definition:** Events A and B are mutually exclusive (disjoint) if they **cannot occur simultaneously**:
```
A ∩ B = ∅
```

**Venn diagram:**
```
    ┌─────────────────────┐
    │                     │
    │   ┌──────┐          │
    │   │      │          │
    │   │  A   │          │
    │   │      │          │
    │   └──────┘          │
    │                     │
    │          ┌──────┐   │
    │          │      │   │
    │          │  B   │   │
    │          │      │   │
    │          └──────┘   │
    │                     │
    └─────────────────────┘
       Sample Space S
```

**Notice:** A and B have **zero overlap**. They don't touch. The intersection is empty.

**What this means in practice:**
- If A happens, B **cannot** happen. They block each other.
- `P(A ∩ B) = 0` (empty intersection = zero probability)

**Consequence — by Axiom 3:**
```
P(A ∪ B) = P(A) + P(B)
```
Since there's no overlap, we don't subtract anything.

**Example:** Rolling a die once:
- A = "roll a 2" = {2}
- B = "roll a 5" = {5}
- Can you roll both 2 and 5 on the same die? **No.** A ∩ B = ∅
- P(A ∪ B) = P(A) + P(B) = 1/6 + 1/6 = 1/3

**Real-world examples:**
- A = "it is raining", B = "it is not raining" — both can't be true
- A = "card is a heart", B = "card is a spade" — a single card can't be both

---

### Independent Events — Venn Diagram

**Definition:** Events A and B are independent if knowing that one occurred gives **no information** about whether the other occurred:
```
P(A ∩ B) = P(A) × P(B)
```

**Venn diagram:**
```
    ┌─────────────────────┐
    │                     │
    │   ┌────────────┐    │
    │   │      A     │    │
    │   │   ┌─────┐  │    │
    │   │   │A∩B  │  │    │
    │   │   └─────┘  │    │
    │   └────────────┘    │
    │        B            │
    │   ┌────────────┐    │
    │   │            │    │
    │   └────────────┘    │
    │                     │
    └─────────────────────┘
       Sample Space S
```

**Notice:** A and B **overlap**. Their intersection is **not empty**.

**But here's the subtle part:** The overlap size isn't arbitrary. It must be exactly `P(A) × P(B)`. The circles overlap **proportionally** — the fraction of B that A covers equals P(A), and the fraction of A that B covers equals P(B).

**Equivalent definitions (all mean the same thing):**
```
1. P(A ∩ B) = P(A) × P(B)
2. P(A | B) = P(A)     ← knowing B happened doesn't change P(A)
3. P(B | A) = P(B)     ← knowing A happened doesn't change P(B)
```

**Example:** Tossing a fair coin twice:
- A = "first toss is heads" → P(A) = 1/2
- B = "second toss is heads" → P(B) = 1/2
- Does the first toss affect the second? **No.**
- P(A ∩ B) = P(H,H) = 1/4 = 1/2 × 1/2 = P(A) × P(B) ✓

**Real-world examples:**
- A = "first coin flip is heads", B = "second coin flip is heads" — independent
- A = "it rains in Tokyo today", B = "stock market goes up" — roughly independent

---

### Side-by-Side Venn Comparison

| Mutually Exclusive    | Independent             |
| --------------------- | ----------------------- |
| ![mutually exclusive] | ![independent]          |
| ```                   | ```                     |
| ┌──────────┐          | ┌─────────────────────┐ |
| │  A      │           | │                     │ |
| │         │   B       | │  ┌──────────┐       │ |
| │         │  ┌──┐     | │  │    A     │       │ |
| │         │  │  │     | │  │  ┌───┐   │       │ |
| └──────────┘  │  │    | │  │  │∩  │   │       │ |
| │  │                  | │  │  │   │   │       │ |
| └──┘                  | │  │  └───┘   │       │ |
| ```                   | │  └──────────┘       │ |
|                       | │     B              │  |
| **No overlap**        | └─────────────────────┘ |
| Overlap = 0           | ```                     |
|                       | **Has overlap**         |
|                       | Overlap = P(A) × P(B)   |

---

### Critical Distinction — Why We Treat Them Differently

| Property | Mutually Exclusive | Independent |
|---|---|---|
| **Venn overlap** | None (A ∩ B = ∅) | Exists (A ∩ B ≠ ∅) |
| **P(A ∩ B)** | **0** | **P(A) × P(B)** |
| **Can both happen?** | **No** (impossible) | **Yes** (possible) |
| **If A happens → B?** | Impossible (B blocked) | Unchanged (same chance) |
| **P(A ∪ B)** | P(A) + P(B) | P(A) + P(B) - P(A)P(B) |

**The most important rule to remember:**

> **Mutually exclusive events with positive probability are NEVER independent.**

**Proof:** If A and B are mutually exclusive → `P(A ∩ B) = 0`
If P(A) > 0 and P(B) > 0 → `P(A) × P(B) > 0`
So `P(A ∩ B) ≠ P(A) × P(B)` → **not independent.**

**In plain English:** If two events can't happen together (mutually exclusive), then knowing one happened **definitely tells you** the other didn't happen — which means they're the **opposite of independent**.

### Common EXAM Trap

Many students confuse these two concepts. Here's a test:

> Q: If P(A) = 0.3, P(B) = 0.4, and A and B are mutually exclusive, what is P(A ∩ B)?
> A: **0** (because mutually exclusive = no overlap)

> Q: If P(A) = 0.3, P(B) = 0.4, and A and B are independent, what is P(A ∩ B)?
> A: **0.12** (because independent = P(A) × P(B))

> Q: Can A and B be both mutually exclusive AND independent?
> A: **Only if P(A) = 0 or P(B) = 0.** If both have positive probability, impossible.

### Exhaustive Events

A set of events is exhaustive if their union covers the entire sample space:
```
A₁ ∪ A₂ ∪ ... ∪ Aₖ = S
```

If they are also mutually exclusive, they form a **partition** of the sample space.

### Exhaustive Events

A set of events is exhaustive if their union covers the entire sample space:
```
A₁ ∪ A₂ ∪ ... ∪ Aₖ = S
```

If they are also mutually exclusive, they form a **partition** of the sample space.

### Practice Problems

Solve these with **full derivation** — show each step.

---

#### Problem 1: PIN Codes

How many 4-digit PINs can be formed from digits 0-9:
a) If repetition is allowed?
b) If repetition is NOT allowed?

<details>
<summary>Solution (try first!)</summary>

a) With repetition: `10⁴ = 10,000`
b) Without repetition: `P(10,4) = 10! / 6! = 10·9·8·7 = 5,040`
</details>

---

#### Problem 2: Sum of 7

A fair die is rolled twice. What is the probability the sum is 7?

<details>
<summary>Solution (try first!)</summary>

Sample space: `|S| = 6 × 6 = 36`
Favorable pairs summing to 7: {(1,6), (2,5), (3,4), (4,3), (5,2), (6,1)} → 6 outcomes
P(sum = 7) = 6/36 = 1/6
</details>

---

#### Problem 3: Card Drawing

In a standard 52-card deck:
a) P(drawing a King)?
b) P(drawing a Red card)?
c) P(drawing a Face card: J, Q, K)?
d) P(drawing a Red King)?
e) P(drawing a Red card OR a King)?

<details>
<summary>Solution (try first!)</summary>

a) 4 Kings → P = 4/52 = 1/13
b) 26 Red cards → P = 26/52 = 1/2
c) 12 face cards → P = 12/52 = 3/13
d) 2 Red Kings → P = 2/52 = 1/26
e) P(Red ∪ King) = P(Red) + P(King) - P(Red∩King) = 26/52 + 4/52 - 2/52 = 28/52 = 7/13
</details>

---

#### Problem 4: Independence Check

Given `P(A) = 0.4`, `P(B) = 0.5`, `P(A ∩ B) = 0.2`. Are A and B:
a) Independent?
b) Mutually exclusive?

<details>
<summary>Solution (try first!)</summary>

a) `P(A)·P(B) = 0.4 × 0.5 = 0.2 = P(A∩B)`. Yes, independent.
b) `P(A∩B) = 0.2 ≠ 0`. No, not mutually exclusive.
</details>

---

#### Problem 5: Balls in a Bag

A bag has 3 red, 4 blue, 5 green balls (12 total). Two balls are drawn **without replacement**. What's the probability both are the same color?

<details>
<summary>Solution (try first!)</summary>

P(both same) = P(both red) + P(both blue) + P(both green)

P(both red) = (3/12) × (2/11) = 6/132
P(both blue) = (4/12) × (3/11) = 12/132
P(both green) = (5/12) × (4/11) = 20/132

P(both same) = (6 + 12 + 20) / 132 = 38/132 = 19/66
</details>

---

#### Problem 6: Derivation Challenge

Derive Pascal's Identity `C(n, r) = C(n-1, r-1) + C(n-1, r)` **algebraically** using the formula `C(n, r) = n! / [r!(n-r)!]`.

<details>
<summary>Solution (try first!)</summary>

C(n-1, r-1) + C(n-1, r)
= (n-1)! / [(r-1)!(n-r)!] + (n-1)! / [r!(n-1-r)!]
= (n-1)! / [(r-1)!(n-r)!] + (n-1)! / [r!(n-r-1)!]

First term multiply by r/r: = r·(n-1)! / [r!(n-r)!]
Second term multiply by (n-r)/(n-r): = (n-r)·(n-1)! / [r!(n-r)!]

Sum = (n-1)!·[r + (n-r)] / [r!(n-r)!]
    = (n-1)!·n / [r!(n-r)!]
    = n! / [r!(n-r)!]
    = C(n, r)
</details>

---

## Summary of Formulas in This Session

| Concept | Formula |
|---|---|
| Permutation | `P(n, r) = n!/(n-r)!` |
| Permutation (with repetition) | `nʳ` |
| Permutation (identical objects) | `n!/(n₁!·n₂!·...·nₖ!)` |
| Combination | `C(n, r) = n!/[r!(n-r)!]` |
| Complement | `P(A') = 1 - P(A)` |
| Union (general) | `P(A∪B) = P(A) + P(B) - P(A∩B)` |
| Union (mutually exclusive) | `P(A∪B) = P(A) + P(B)` |
| Intersection (independent) | `P(A∩B) = P(A)·P(B)` |

---

## Ready for Session 002?

Reply **"done session-001"** when you've studied everything and solved the practice problems. I'll verify your answers, and if you're solid, we move to **Session 002**: Conditional Probability & Bayes' Theorem.
