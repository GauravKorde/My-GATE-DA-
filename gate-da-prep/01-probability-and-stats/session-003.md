# Session 003 — Random Variables: The Documentary

> **📅 Expected:** Jun 21 – Jun 24 | **Buffer:** +13 days 🟢 | **Status:** 📄 Doc ready (written ahead of schedule)
>
> A first-principles journey from "outcomes" to "numbers" to "distributions."
> Read like a story — each chapter builds on the last.

---

## Chapter 1: The Bridge

### The problem with events

So far, every probability question has been about **events**:
- "What's the probability of getting exactly 3 heads?"
- "What's the probability that the die shows an even number?"
- "What's the probability that the temperature exceeds 30°C?"

Events are fine for answering isolated questions. But they're clumsy for mathematics. You can't add events, multiply events, or take averages of events.

You **can** add numbers, multiply numbers, and average numbers.

### The big idea

What if we could assign a **number** to each outcome of an experiment?

Instead of saying "the coin shows heads," say "X = 1." Instead of "the coin shows tails," say "X = 0."

Now X is a **random variable** — it takes different numerical values with different probabilities. And because it's a number, we can do arithmetic with it. We can compute its average, its spread, its relationships with other random variables.

**A random variable is a function that maps outcomes of a random experiment to real numbers.**

```
   Sample Space Ω                Real Numbers ℝ
   ┌──────────┐                   
   │  heads   │──── X(ω) ────→    1
   │  tails   │──── X(ω) ────→    0
   └──────────┘                   
```

That's it. A random variable is just a **label** — a numerical label for each outcome.

### Why this simple shift changes everything

Before random variables:
- We could only ask: "Does event A occur?"
- Probability was about sets and Boolean logic

After random variables:
- We can ask: "What's the average value of X?"
- We can ask: "How spread out is X?"
- We can ask: "How does X relate to Y?"
- We can build **models** of the world

**Random variables are the language of all modern statistics and machine learning.** Every algorithm, every model, every test is expressed in terms of random variables.

### Two species

Random variables come in two flavors:

1. **Discrete:** Takes countably many values (coin flips, dice rolls, counts)
2. **Continuous:** Takes uncountably many values (temperature, time, distance)

These two species need slightly different mathematical tools. Let's meet them both.

---

## Chapter 2: Discrete Random Variables

### Definition

A random variable is **discrete** if it can only take a finite (or countably infinite) number of values.

Examples:
- Number of heads in 3 coin flips: values {0, 1, 2, 3}
- Roll of a die: values {1, 2, 3, 4, 5, 6}
- Number of customers arriving in an hour: values {0, 1, 2, ...}

### The Probability Mass Function (PMF)

For a discrete random variable, every possible value has a specific probability attached to it. The function that maps values to probabilities is called the **PMF**:

$$p_X(x) = P(X = x)$$

**Properties:**
1. $0 \leq p_X(x) \leq 1$ for all $x$
2. $\sum_x p_X(x) = 1$ (all probability sums to 1)
3. $P(X \in A) = \sum_{x \in A} p_X(x)$ (probability of any set = sum of probabilities in that set)

### Example: Fair die

$X$ = outcome of a fair six-sided die.

$p_X(1) = p_X(2) = ... = p_X(6) = \frac{1}{6}$

$$P(X \leq 2) = p_X(1) + p_X(2) = \frac{1}{6} + \frac{1}{6} = \frac{1}{3}$$

$$P(X \text{ is even}) = p_X(2) + p_X(4) + p_X(6) = \frac{3}{6} = \frac{1}{2}$$

### Example: Biased coin

$X$ = outcome of a biased coin (heads with probability 0.6, tails with 0.4).

$p_X(1) = 0.6$, $p_X(0) = 0.4$

$$E[X] = 1(0.6) + 0(0.4) = 0.6$$

This is the connection back to Sessions 001-002: all the expectation and variance formulas we derived work because random variables turn events into numbers.

### Visualizing a PMF

A PMF is a **bar chart**:
- Horizontal axis: possible values of X
- Vertical axis: probability of each value
- Each bar height = $P(X = x)$
- All bar heights sum to 1

---

## Chapter 3: Continuous Random Variables

### The problem with continuous outcomes

Consider: "The temperature tomorrow at noon."

It could be 25.0°C, 25.1°C, 25.01°C, 25.001°C — **infinitely many** possible values.

If we try to assign a probability to each individual value, something breaks:

$$P(T = 25.0) = ?$$

If all values are equally likely, there are infinitely many, so each has probability 0. If we assign non-zero probability to each, they'd sum to infinity, not 1.

**The probability of any specific exact value in a continuous distribution is zero.** This sounds weird, but it's true. The probability that the temperature is *exactly* 25.000000...°C is vanishingly small. We can only talk about ranges: $P(24.5 < T < 25.5)$.

### The Probability Density Function (PDF)

Instead of probability at a point, we talk about **density** — how concentrated the probability is around a point.

The PDF $f_X(x)$ has these properties:

1. $f_X(x) \geq 0$ for all $x$ (density can't be negative)
2. $\int_{-\infty}^{\infty} f_X(x)\,dx = 1$ (total probability = 1)
3. $P(a \leq X \leq b) = \int_a^b f_X(x)\,dx$ (probability = area under the curve)

**Critical distinction: $f_X(x)$ is NOT a probability!** It's a density. It can be greater than 1. Only the **area** under $f_X$ is a probability.

### Height ≠ Probability

This is the most common confusion with PDFs.

For a discrete PMF: $p_X(3) = P(X = 3)$ — the height IS the probability.

For a continuous PDF: $f_X(3)$ is a **density**, not a probability. $P(X = 3) = 0$. Only $\int_a^b f_X(x)dx$ gives a probability.

Think of density like physical density (kg/m³). A material can have density 10,000 kg/m³ (very dense!) but the mass at a single point is zero. You need volume to get mass. Likewise, you need interval length to get probability.

### Visualizing a PDF

A PDF is a **smooth curve**:
- Horizontal axis: possible values of X
- Vertical axis: probability **density** (not probability)
- Probability = **area under the curve** over an interval
- Total area under the curve = 1

---

## Chapter 4: The CDF — Universal Language

### The Great Unifier

PMFs work for discrete variables. PDFs work for continuous variables. But what if we want one function that works for **both**?

Enter the **Cumulative Distribution Function (CDF)**:

$$F_X(x) = P(X \leq x)$$

This is defined the same way for discrete and continuous variables. It's the probability that X is at most some value x.

### For discrete variables

$$F_X(x) = \sum_{t \leq x} p_X(t)$$

A step function — jumps at each possible value, flat in between.

**Example — Fair die:**
- $F(1) = P(X \leq 1) = 1/6$
- $F(2) = P(X \leq 2) = 1/6 + 1/6 = 1/3$
- $F(3) = 1/2$, $F(4) = 2/3$, $F(5) = 5/6$, $F(6) = 1$
- $F(2.5) = P(X \leq 2.5) = P(X \leq 2) = 1/3$ (flat between jumps)

### For continuous variables

$$F_X(x) = \int_{-\infty}^x f_X(t)\,dt$$

A smooth, continuous function — no jumps because there's no probability mass at any single point.

**Example — Uniform(0,1):**
$$F_X(x) = \begin{cases} 0 & x < 0 \\ x & 0 \leq x \leq 1 \\ 1 & x > 1 \end{cases}$$

### Properties of any CDF

1. $F(x)$ is non-decreasing: if $x_1 < x_2$, then $F(x_1) \leq F(x_2)$
2. $\lim_{x \to -\infty} F(x) = 0$ (nothing below minus infinity)
3. $\lim_{x \to \infty} F(x) = 1$ (everything below infinity)
4. $P(a < X \leq b) = F(b) - F(a)$ (probability of an interval)

**Property 4 is the most useful.** To find the probability that X falls between a and b, just subtract two CDF values. No integration needed if you already have the CDF.

### The CDF connects PMF, PDF, and probability

```
              CDF
            F(x) = P(X ≤ x)
            ↗         ↖
    Discrete           Continuous
   F(x) = ∑ p(t)     F(x) = ∫ f(t)dt
       t≤x              -∞
         ↕                  ↕
        PMF                PDF
   p(x) = P(X = x)   f(x) = F'(x)
```

Every random variable, discrete or continuous, has a CDF. It's the most general description.

---

## Chapter 5: Bernoulli — The Atom

### The simplest possible random variable

Imagine a single coin flip. Not a fair coin — a biased one. Heads with probability $p$, tails with probability $1-p$.

We encode heads as 1, tails as 0. This gives us:

$$X = \begin{cases} 1 & \text{with probability } p \\ 0 & \text{with probability } 1-p \end{cases}$$

This is a **Bernoulli** random variable: $X \sim \text{Bernoulli}(p)$.

### Deriving the PMF

The PMF needs to produce $p$ when $x=1$ and $1-p$ when $x=0$.

One formula that does this:

$$p_X(x) = p^x(1-p)^{1-x}, \quad x \in \{0, 1\}$$

Let's verify:
- When $x=1$: $p^1(1-p)^{0} = p \times 1 = p$ ✅
- When $x=0$: $p^0(1-p)^{1} = 1 \times (1-p) = 1-p$ ✅

This compact form is useful for proofs, but it's just a trick of exponents.

### Deriving the CDF

The CDF is $F(x) = P(X \leq x)$. Since X only takes values 0 and 1:

- For $x < 0$: $P(X \leq x) = 0$ (nothing is below 0)
- For $0 \leq x < 1$: $P(X \leq x) = P(X=0) = 1-p$ (only 0 qualifies)
- For $x \geq 1$: $P(X \leq x) = P(X=0) + P(X=1) = 1-p + p = 1$

$$F_X(x) = \begin{cases} 0 & x < 0 \\ 1-p & 0 \leq x < 1 \\ 1 & x \geq 1 \end{cases}$$

This is a **step function** — a hallmark of discrete distributions. It jumps at each possible value.

### Deriving the mean

The mean $E[X] = \sum_x x \cdot P(X=x)$ is a weighted average:

$$E[X] = 1 \cdot P(X=1) + 0 \cdot P(X=0)$$
$$= 1(p) + 0(1-p)$$
$$= p$$

**The mean of a Bernoulli is just the probability of success.** This makes sense: if you flip a coin with p=0.6 many times, the average outcome is 0.6 — closer to 1 than 0 because success is more likely.

### Deriving the variance

Variance needs $E[X^2]$. Let's compute it from first principles:

$$E[X^2] = \sum_x x^2 \cdot P(X=x)$$
$$= 1^2(p) + 0^2(1-p)$$
$$= p$$

**Key insight:** For a 0/1 variable, $X^2 = X$ because $0^2 = 0$ and $1^2 = 1$. So $E[X^2] = E[X] = p$ always. This is only true for Bernoulli — it's a special property of 0/1 variables.

Now apply the shortcut formula:

$$\text{Var}(X) = E[X^2] - (E[X])^2$$
$$= p - p^2$$
$$= p(1-p)$$

**Let's understand this formula:**

- If $p = 0$ (success never happens): $\text{Var} = 0(1) = 0$ — no uncertainty, X is always 0
- If $p = 1$ (success always happens): $\text{Var} = 1(0) = 0$ — no uncertainty, X is always 1
- If $p = 0.5$ (maximum uncertainty): $\text{Var} = 0.5(0.5) = 0.25$ — maximum variance

The variance is zero at the extremes and maximal at p=0.5. This is the signature of a Bernoulli: **uncertainty peaks when the outcome is most balanced.**

### Why Bernoulli matters

Bernoulli is the **atom** of probability. Everything bigger is built from it:

- **Binomial:** Sum of $n$ independent Bernoullis
- **Geometric:** Number of trials until first success
- **Negative Binomial:** Number of trials until $r$ successes
- **Poisson:** Limit of many rare Bernoullis

If you understand Bernoulli, you understand the building block of all discrete probability.

---

## Chapter 6: Binomial — Many Independent Trials

### The story

You flip a biased coin (heads with probability $p$) $n$ times. Each flip is independent. You count the total number of heads.

Each individual flip is $\text{Bernoulli}(p)$. The total $X$ is the **sum**:

$$X = X_1 + X_2 + ... + X_n, \quad \text{where each } X_i \sim \text{Bernoulli}(p)$$

We write: $X \sim \text{Binomial}(n, p)$.

### Deriving the PMF — Step by Step

**The question:** What's the probability of getting exactly $k$ heads in $n$ flips?

**Step 1: Probability of one specific sequence.**

Consider the sequence: H, H, T, H, T, ... (k heads, n-k tails, in a specific order).

Since flips are independent, multiply probabilities:
- Each head contributes factor $p$
- Each tail contributes factor $1-p$
- Total: $p \times p \times (1-p) \times p \times (1-p) \times ...$

The order doesn't matter for the product — only the counts matter. Any sequence with exactly $k$ heads and $n-k$ tails has probability:

$$p^k (1-p)^{n-k}$$

**Step 2: How many such sequences exist?**

We need to choose which $k$ of the $n$ positions are heads. The remaining $n-k$ positions are automatically tails.

This is the combinatorial choice problem: "choose $k$ from $n$":

$$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$

**Step 3: Multiply.**

Total probability = (number of favorable sequences) × (probability of each sequence):

$$\boxed{P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}}$$

This is the **binomial formula**. It has two distinct parts:
1. $\binom{n}{k}$ — the **combinatorial** part: how many ways to arrange $k$ successes
2. $p^k(1-p)^{n-k}$ — the **probability** part: chance of one specific arrangement

### Example: 3 coin flips, fair coin (p = 0.5)

$$P(X=0) = \binom{3}{0}(0.5)^0(0.5)^3 = 1 \times 1 \times 0.125 = 0.125$$
$$P(X=1) = \binom{3}{1}(0.5)^1(0.5)^2 = 3 \times 0.5 \times 0.25 = 0.375$$
$$P(X=2) = \binom{3}{2}(0.5)^2(0.5)^1 = 3 \times 0.25 \times 0.5 = 0.375$$
$$P(X=3) = \binom{3}{3}(0.5)^3(0.5)^0 = 1 \times 0.125 \times 1 = 0.125$$

**Check:** $0.125 + 0.375 + 0.375 + 0.125 = 1.0$ ✅

### Deriving the Binomial mean — two ways

**Method 1: From definition.**

$$E[X] = \sum_{k=0}^n k \cdot \binom{n}{k} p^k (1-p)^{n-k}$$

This sum looks hard. But there's a trick: factor out $np$:

$$E[X] = np \sum_{k=1}^n \binom{n-1}{k-1} p^{k-1} (1-p)^{n-k}$$

The sum is just the total probability of a Binomial$(n-1, p)$, which equals 1. So:

$$E[X] = np$$

**Method 2: Sum of Bernoullis (elegant).**

Since $X = X_1 + X_2 + ... + X_n$ where each $X_i \sim \text{Bernoulli}(p)$:

$$E[X] = E[X_1 + X_2 + ... + X_n]$$
$$= E[X_1] + E[X_2] + ... + E[X_n] \quad (\text{linearity of expectation})$$
$$= p + p + ... + p$$
$$= np$$

**Method 2 is simpler and more insightful.** It shows that the mean of a Binomial is just $n$ copies of the Bernoulli mean added up. This is why understanding Bernoulli first makes everything easier.

### Deriving the Binomial variance

**Method 1: From the PMF (painful).**

You can compute $E[X^2] = \sum k^2 \binom{n}{k} p^k(1-p)^{n-k}$ using identities with factorial moments. It works but it's messy.

**Method 2: Sum of independent Bernoullis (elegant).**

Since $X = X_1 + ... + X_n$ and the $X_i$ are **independent**:

$$\text{Var}(X) = \text{Var}(X_1 + X_2 + ... + X_n)$$
$$= \text{Var}(X_1) + \text{Var}(X_2) + ... + \text{Var}(X_n) \quad (\text{independence!})$$
$$= p(1-p) + p(1-p) + ... + p(1-p)$$
$$= np(1-p)$$

**Why independence matters here:** If the $X_i$ were correlated, we'd need covariance terms. But coin flips are independent, so variances add cleanly.

### Understanding $np(1-p)$

- $np$ is the typical number of successes
- $(1-p)$ is the probability of failure — the "opposite force"
- The product $np(1-p)$ is largest when $p=0.5$ (maximum uncertainty) and zero when $p=0$ or $p=1$ (certainty)
- For fixed $p$, variance grows linearly with $n$ — more trials = more spread

---

## Chapter 7: Uniform — The Fair Distribution

### The core philosophy

Some distributions are fair by design. A fair die doesn't favor any face. A well-shuffled deck doesn't favor any card. A properly programmed random number generator doesn't favor any interval.

This "fairness" — equal probability for all equally-sized outcomes — is the soul of the **Uniform distribution**.

We'll meet two versions: the **discrete** uniform (finitely many equally likely outcomes) and the **continuous** uniform (infinitely many equally likely outcomes over an interval). They look different mathematically, but they share the same spirit.

---

### Part 1: Discrete Uniform

#### The setup

Imagine a random number generator that picks an integer from 1 to $n$, with every integer equally likely. No favorites. No bias.

We write:

$$X \sim \text{Uniform}\{1, 2, ..., n\}$$

The curly braces remind us: these are discrete points, not a continuous range.

#### Deriving the PMF

If all $n$ outcomes are equally likely, each must have probability:

$$P(X = i) = \frac{1}{n}, \quad i = 1, 2, ..., n$$

**Check:** The sum of all probabilities must be 1:

$$\sum_{i=1}^n \frac{1}{n} = n \cdot \frac{1}{n} = 1$$ ✅

That's the entire PMF. There's nothing more to it.

#### The PMF in compact form

$$p_X(x) = \begin{cases} \frac{1}{n} & x \in \{1, 2, ..., n\} \\ 0 & \text{otherwise} \end{cases}$$

#### Deriving the CDF

The CDF is $F(x) = P(X \leq x)$. Since X takes integer values, the CDF jumps at each integer:

For $x < 1$: $F(x) = 0$ (nothing below the minimum)

For $1 \leq x < 2$: $F(x) = P(X = 1) = \frac{1}{n}$

For $2 \leq x < 3$: $F(x) = P(X=1) + P(X=2) = \frac{2}{n}$

In general, for $k \leq x < k+1$ where $k = 1, 2, ..., n-1$:

$$F(x) = \frac{k}{n}$$

For $x \geq n$: $F(x) = 1$

The CDF is a staircase with $n$ steps, each of height $1/n$.

#### Deriving the mean — the story of the sum

The mean is:

$$E[X] = \sum_{x=1}^n x \cdot P(X=x) = \sum_{x=1}^n x \cdot \frac{1}{n} = \frac{1}{n}\sum_{x=1}^n x$$

So the mean is just the arithmetic average — makes sense since all outcomes are equally weighted.

Now we need $\sum_{x=1}^n x = 1 + 2 + 3 + ... + n$.

**How to sum 1 through n?** There's a famous trick. Pair up the numbers:

$$1 + 2 + 3 + ... + (n-2) + (n-1) + n$$

Pair the first and last: $1 + n = n+1$
Pair the second and second-last: $2 + (n-1) = n+1$
Pair the third and third-last: $3 + (n-2) = n+1$

Each pair sums to $n+1$. How many pairs? $\frac{n}{2}$ pairs (if $n$ is even. If $n$ is odd, the middle term is $(n+1)/2$, but the formula still works).

$$\sum_{i=1}^n i = \frac{n(n+1)}{2}$$

This is one of the most useful formulas in all of mathematics. Memorize it.

Now substitute:

$$E[X] = \frac{1}{n} \cdot \frac{n(n+1)}{2} = \frac{n+1}{2}$$

**The mean of integers 1 through n is exactly the midpoint.** For a fair die ($n=6$):

$$E[X] = \frac{6+1}{2} = 3.5$$ ✅

The mean doesn't have to be a possible outcome! 3.5 is not on the die, but it's the center of mass.

#### Deriving the variance — building up step by step

We need $\text{Var}(X) = E[X^2] - (E[X])^2$.

First, $E[X^2]$:

$$E[X^2] = \sum_{x=1}^n x^2 \cdot \frac{1}{n} = \frac{1}{n}\sum_{x=1}^n x^2$$

**The sum of squares formula.** There's a pattern here:

$$1^2 + 2^2 + 3^2 + ... + n^2 = \frac{n(n+1)(2n+1)}{6}$$

Let me show you why this works (briefly). The sum of squares can be derived from:

$$(k+1)^3 - k^3 = 3k^2 + 3k + 1$$

Summing both sides from $k=1$ to $n$, the left telescopes to $(n+1)^3 - 1$, and the right gives $3\sum k^2 + 3\sum k + n$. Solve for $\sum k^2$:

$$\sum_{k=1}^n k^2 = \frac{n(n+1)(2n+1)}{6}$$

Now substitute:

$$E[X^2] = \frac{1}{n} \cdot \frac{n(n+1)(2n+1)}{6} = \frac{(n+1)(2n+1)}{6}$$

Now compute variance:

$$\text{Var}(X) = E[X^2] - (E[X])^2$$

$$= \frac{(n+1)(2n+1)}{6} - \left(\frac{n+1}{2}\right)^2$$

Let me take this step by step. Square the second term:

$$\left(\frac{n+1}{2}\right)^2 = \frac{(n+1)^2}{4}$$

So:

$$\text{Var}(X) = \frac{(n+1)(2n+1)}{6} - \frac{(n+1)^2}{4}$$

Factor out $(n+1)$:

$$= (n+1) \left[ \frac{2n+1}{6} - \frac{n+1}{4} \right]$$

Common denominator of 12:

$$= (n+1) \left[ \frac{2(2n+1)}{12} - \frac{3(n+1)}{12} \right]$$

$$= (n+1) \left[ \frac{4n+2 - 3n - 3}{12} \right]$$

$$= (n+1) \left[ \frac{n - 1}{12} \right]$$

And since $(n+1)(n-1) = n^2 - 1$:

$$\boxed{\text{Var}(X) = \frac{n^2 - 1}{12}}$$

#### Testing on a fair die ($n=6$)

$$\text{Var}(X) = \frac{36 - 1}{12} = \frac{35}{12} \approx 2.917$$

**Sanity check:** The die values {1, 2, 3, 4, 5, 6} have a range of 5. The standard deviation $\sqrt{2.917} \approx 1.708$ is roughly 1/3 of the range — reasonable for a uniform spread.

---

### Part 2: The Bridge — Why continuous is different

Now imagine: instead of picking an integer from 1 to 6, you pick a **real number** between 0 and 1. Any real number — 0.5, 0.12345, 0.9999999, $\pi/4$, etc.

There are infinitely many possibilities. Actually, uncountably infinitely many.

If each individual value had equal probability, each would have probability $1/\infty = 0$. We can't build a PMF this way.

But we CAN build a **density** — a function where the area under the curve gives probability, not the height.

---

### Part 3: Continuous Uniform

#### The setup

$$X \sim \text{Uniform}(a, b)$$

This means: X is equally likely to fall anywhere in the interval $[a, b]$.

#### Deriving the PDF from first principles

We want a function $f(x)$ such that:
1. $f(x) \geq 0$ for all $x$
2. $\int_{-\infty}^{\infty} f(x)\,dx = 1$ (total area = 1)
3. Equal-sized intervals have equal probability

Condition 3 is the key. If we split $[a, b]$ into 10 equal subintervals, each should have probability $1/10$. This forces $f(x)$ to be **constant** on $[a, b]$.

Let $f(x) = c$ for $a \leq x \leq b$, and 0 elsewhere.

Condition 2 gives us $c$:

$$\int_{-\infty}^{\infty} f(x)\,dx = \int_a^b c\,dx = c(b-a) = 1$$

So:

$$c = \frac{1}{b-a}$$

Therefore:

$$f_X(x) = \begin{cases} \frac{1}{b-a} & a \leq x \leq b \\ 0 & \text{otherwise} \end{cases}$$

**Visualizing the PDF:** It's a flat horizontal line at height $1/(b-a)$. The total area is a rectangle of width $(b-a)$ and height $1/(b-a)$, so area = 1.

**Why the height can be > 1:** If $b-a < 1$, the height $1/(b-a) > 1$. This is fine because $f(x)$ is a **density**, not a probability. A density can be any non-negative number. Only the **area** must be 1.

**Example:** Uniform(0, 0.5): height = $1/0.5 = 2$. Area = $0.5 \times 2 = 1$. ✅

#### Deriving the CDF

The CDF is the accumulated area from the left:

$$F(x) = \int_{-\infty}^x f(t)\,dt$$

We handle three regions:

**Region 1: $x < a$**

Nothing accumulated yet:

$$F(x) = \int_{-\infty}^x 0\,dt = 0$$

**Region 2: $a \leq x \leq b$**

We accumulate from $a$ to $x$. Since $f(t) = 1/(b-a)$:

$$F(x) = \int_a^x \frac{1}{b-a}\,dt = \frac{1}{b-a} \cdot (x - a) = \frac{x-a}{b-a}$$

This is a **straight line** starting at 0 (when $x=a$) and ending at 1 (when $x=b$).

**Region 3: $x > b$**

All probability accumulated:

$$F(x) = 1$$

**The complete CDF:**

$$F_X(x) = \begin{cases} 0 & x < a \\ \dfrac{x-a}{b-a} & a \leq x \leq b \\ 1 & x > b \end{cases}$$

**Understanding the CDF shape:** It's a linear ramp. The slope is $1/(b-a)$ — steeper for narrow intervals, gentler for wide ones. This linearity means: **probability grows proportionally with interval length**. An interval of length $L$ has probability $L/(b-a)$.

#### Computing probabilities from the CDF

The CDF makes probability calculations trivial:

$$P(c < X < d) = F(d) - F(c) = \frac{d-a}{b-a} - \frac{c-a}{b-a} = \frac{d-c}{b-a}$$

**The result is beautifully simple:** probability = (length of interval) / (total length). This is the continuous analogue of "favorable outcomes / total outcomes" — we just replace counting with measuring length.

**Example:** For Uniform(0, 10):
- $P(2 < X < 5) = (5-2)/(10-0) = 3/10 = 0.3$
- $P(X > 7) = (10-7)/10 = 0.3$
- $P(X = 4) = 0$ (a single point has zero length)

**Why $P(X = 4) = 0$:** This is the defining weirdness of continuous distributions. The probability of any exact value is zero. But the probability of being *near* 4 (say, between 3.9 and 4.1) is positive — it's $0.2/10 = 0.02$. This distinction — between "exact" and "nearby" — is the key to understanding continuous probability.

#### Deriving the mean

$$E[X] = \int_a^b x \cdot f(x)\,dx = \int_a^b x \cdot \frac{1}{b-a}\,dx$$

$$= \frac{1}{b-a} \int_a^b x\,dx$$

The integral of $x$ is $x^2/2$:

$$= \frac{1}{b-a} \cdot \left[ \frac{x^2}{2} \right]_a^b$$

$$= \frac{1}{b-a} \cdot \frac{b^2 - a^2}{2}$$

Factor $b^2 - a^2 = (b-a)(b+a)$:

$$= \frac{1}{b-a} \cdot \frac{(b-a)(b+a)}{2}$$

$$= \frac{a+b}{2}$$

**The mean is exactly the midpoint.** This makes sense: the distribution is perfectly symmetric around $(a+b)/2$, so the center of mass is the center of the interval.

**Example:** Uniform(0, 10): $E[X] = (0+10)/2 = 5$. The average of a random number between 0 and 10 is 5.

#### Deriving the variance — the full journey

We need $\text{Var}(X) = E[X^2] - (E[X])^2$. We already have $E[X] = (a+b)/2$. Now we need $E[X^2]$.

**Step 1: Compute $E[X^2]$.**

$$E[X^2] = \int_a^b x^2 \cdot \frac{1}{b-a}\,dx = \frac{1}{b-a} \int_a^b x^2\,dx$$

The integral of $x^2$ is $x^3/3$:

$$= \frac{1}{b-a} \cdot \left[ \frac{x^3}{3} \right]_a^b$$

$$= \frac{1}{b-a} \cdot \frac{b^3 - a^3}{3}$$

$$= \frac{b^3 - a^3}{3(b-a)}$$

**Step 2: Simplify $b^3 - a^3$.**

Recall the factorization:

$$b^3 - a^3 = (b-a)(b^2 + ab + a^2)$$

This is the difference of cubes. Verify: $(b-a)(b^2 + ab + a^2) = b^3 + ab^2 + a^2b - a^2b - a^2b - ab^2 - a^3...$ wait, let me be careful:

$$(b-a)(b^2 + ab + a^2)$$
$$= b(b^2 + ab + a^2) - a(b^2 + ab + a^2)$$
$$= b^3 + ab^2 + a^2b - ab^2 - a^2b - a^3$$
$$= b^3 - a^3$$ ✅

So:

$$E[X^2] = \frac{(b-a)(b^2 + ab + a^2)}{3(b-a)} = \frac{a^2 + ab + b^2}{3}$$

**Step 3: Apply the variance shortcut.**

$$\text{Var}(X) = \frac{a^2 + ab + b^2}{3} - \left(\frac{a+b}{2}\right)^2$$

**Step 4: Expand $(a+b)^2/4$.**

$$\left(\frac{a+b}{2}\right)^2 = \frac{a^2 + 2ab + b^2}{4}$$

**Step 5: Get a common denominator of 12.**

$$\text{Var}(X) = \frac{4(a^2 + ab + b^2)}{12} - \frac{3(a^2 + 2ab + b^2)}{12}$$

**Step 6: Combine.**

$$\text{Var}(X) = \frac{4a^2 + 4ab + 4b^2 - 3a^2 - 6ab - 3b^2}{12}$$

**Step 7: Simplify.**

$$= \frac{(4a^2 - 3a^2) + (4ab - 6ab) + (4b^2 - 3b^2)}{12}$$

$$= \frac{a^2 - 2ab + b^2}{12}$$

**Step 8: Recognize the perfect square.**

$$a^2 - 2ab + b^2 = (a - b)^2 = (b - a)^2$$

Since $(a-b)^2 = (b-a)^2$, we can write either. The standard form uses $(b-a)^2$ (positive):

$$\boxed{\text{Var}(X) = \frac{(b-a)^2}{12}}$$

**This is the formula.** It's beautifully simple: the variance of a Uniform depends only on the width squared, divided by 12.

#### Understanding the variance formula

Let's test some cases:

**Uniform(0, 1):** Width = 1. $\text{Var} = 1^2/12 = 1/12 \approx 0.0833$. Standard deviation $\approx 0.289$.

**Uniform(0, 10):** Width = 10. $\text{Var} = 100/12 \approx 8.333$. Standard deviation $\approx 2.887$.

**Uniform(-5, 5):** Width = 10. $\text{Var} = 100/12 \approx 8.333$. Same as Uniform(0,10) — only width matters, not location.

**Why 12?** The number 12 comes from the algebra — specifically from the ratio of the coefficients when we combine the fractions. There's no deep physical meaning; it's just what falls out of the derivation. But it's always 12 for any uniform distribution, which is why you should memorize it.

#### Why Uniform matters in the real world

**1. Random number generation.** Every programming language has a function like `rand()` that generates a Uniform(0,1) random number. All other random distributions (Normal, Binomial, Poisson, etc.) are generated by transforming Uniform random numbers. The Uniform is the raw material.

**2. Complete ignorance.** In Bayesian statistics, when you know nothing about a parameter except its possible range, you assign a Uniform prior. It represents "all values equally plausible."

**3. Round-off error.** If you measure something to the nearest integer, the round-off error is approximately Uniform(-0.5, 0.5).

**4. The simplest test case.** When developing new statistical methods, Uniform data is the first test because the calculations are simplest. If a method doesn't work on Uniform data, it won't work on anything.

---

### Summary: Discrete vs Continuous Uniform

| Property | Discrete Uniform | Continuous Uniform |
|----------|-----------------|-------------------|
| **What it models** | $n$ equally likely points | All points in $[a, b]$ equally likely |
| **PMF/PDF** | $P(X=x) = 1/n$ | $f(x) = 1/(b-a)$ |
| **Mean** | $(n+1)/2$ | $(a+b)/2$ |
| **Variance** | $(n^2-1)/12$ | $(b-a)^2/12$ |
| **CDF** | Staircase | Linear ramp |

The formulas look different, but they share the same DNA. Both say: "everything is equally likely." The mathematical tools differ (sums vs integrals), but the philosophy is identical.

---

## Summary of Formulas

| Distribution | PMF/PDF | Mean | Variance |
|-------------|---------|------|----------|
| Bernoulli(p) | $p^x(1-p)^{1-x}$ for $x\in\{0,1\}$ | $p$ | $p(1-p)$ |
| Binomial(n,p) | $\binom{n}{k}p^k(1-p)^{n-k}$ for $k=0..n$ | $np$ | $np(1-p)$ |
| Uniform(a,b) (cont.) | $\frac{1}{b-a}$ for $a\leq x\leq b$ | $\frac{a+b}{2}$ | $\frac{(b-a)^2}{12}$ |
| Uniform{1..n} (disc.) | $\frac{1}{n}$ for $x=1..n$ | $\frac{n+1}{2}$ | $\frac{n^2-1}{12}$ |

---

## Practice Problems

---

### Problem E1: Bernoulli Basics

A factory produces items with 5% defect rate. Let X = 1 if a randomly selected item is defective, 0 otherwise.

a) What distribution does X follow?
b) Find E[X] and Var(X)
c) Find the CDF of X

> [!info]- First-principle derivation
>
> **The story of a Bernoulli variable:**
>
> Imagine you pick one item from the factory. You're asking a binary question: defective or not? That's it — one trial, two outcomes.
>
> The random variable X maps "defective" → 1, "not defective" → 0. This mapping is a choice. We could have reversed it. What matters is that we've turned an event into a number.
>
> **Where does $E[X] = p$ come from?**
>
> The definition of expectation is: $E[X] = \sum x \cdot P(X=x)$. There are exactly two terms:
>
> $$E[X] = 1 \cdot P(X=1) + 0 \cdot P(X=0)$$
>
> The $0 \cdot P(X=0)$ term is zero, no matter what $P(X=0)$ is. So:
>
> $$E[X] = P(X=1) = p$$
>
> This is a profound result: **the mean of a 0/1 variable equals the probability of 1.** It's not an approximation — it's exact.
>
> **Where does $\text{Var}(X) = p(1-p)$ come from?**
>
> Start with the shortcut: $\text{Var}(X) = E[X^2] - (E[X])^2$.
>
> First, $E[X^2]$. Since X is 0 or 1, $X^2 = X$ (because $0^2 = 0$ and $1^2 = 1$). So $E[X^2] = E[X] = p$.
>
> Therefore:
> $$\text{Var}(X) = p - p^2 = p(1-p)$$
>
> **Understanding $p(1-p)$:**
> - When $p=0$: variance = $0 \times 1 = 0$ — certainty (always defective... wait, that's confusing. Let me rephrase.)
> - When $p=0$: no items are defective. X is always 0. Zero variance.
> - When $p=1$: all items are defective. X is always 1. Zero variance.
> - When $p=0.5$: half defective, half not. Maximum uncertainty. Variance = $0.5 \times 0.5 = 0.25$, which is the maximum possible for a Bernoulli.
>
> The CDF tells the same story: it stays at $1-p$ until x reaches 1, then jumps to 1. The jump height at $x=0$ is $P(X=0) = 1-p$. The jump at $x=1$ is $p$.

> [!success]- Solution (with theory)
>
> a) $X \sim \text{Bernoulli}(p = 0.05)$
>
> b) $E[X] = p = 0.05$
> $\text{Var}(X) = p(1-p) = 0.05(0.95) = 0.0475$
>
> **Interpretation:** The mean (0.05) equals the defect rate. The variance (0.0475) is small because p is close to 0 — there's not much uncertainty when defects are rare.
>
> c)
> $$F_X(x) = \begin{cases} 0 & x < 0 \\ 0.95 & 0 \leq x < 1 \\ 1 & x \geq 1 \end{cases}$$
>
> Reading the CDF: $P(X < 0) = 0$, $P(X \leq 0) = 0.95$ (95% chance of no defect), $P(X \leq 1) = 1$ (certain that X is at most 1).

---

### Problem E2: Uniform Probability

A random number generator produces $X \sim \text{Uniform}(0, 10)$.

a) Find $P(X > 7)$
b) Find $P(2 < X < 5)$
c) Find $P(X = 4)$

> [!info]- First-principle derivation
>
> For a continuous Uniform(a,b), probability of an interval = (length of interval) / (total length):
> $$P(c < X < d) = \frac{d-c}{b-a}$$
>
> This comes from the PDF: $f(x) = 1/(b-a)$, so:
> $$P(c < X < d) = \int_c^d \frac{1}{b-a}dx = \frac{d-c}{b-a}$$
>
> The probability of any exact value is 0 because the integral over a single point is 0.

> [!success]- Solution (with theory)
>
> a) $P(X > 7) = \frac{10-7}{10-0} = \frac{3}{10} = 0.3$
>
> b) $P(2 < X < 5) = \frac{5-2}{10-0} = \frac{3}{10} = 0.3$
>
> c) $P(X = 4) = 0$ (continuous distribution — probability at a single point is always 0)
>
> **Key insight:** Both (a) and (b) give 0.3 because both intervals have length 3. In a uniform distribution, only the length matters, not the location.

---

### Problem E3: Binomial PMF

A fair coin is tossed 5 times. Let X = number of heads.

a) Find $P(X = 3)$
b) Find $P(X \geq 4)$
c) Find $P(1 \leq X \leq 3)$

> [!info]- First-principle derivation
>
> The binomial formula $P(X = k) = \binom{n}{k}p^k(1-p)^{n-k}$ has two parts:
> 1. **$\binom{n}{k}$**: Number of sequences with exactly k heads. For a fair coin, all sequences are equally likely, so this counts favorable outcomes.
> 2. **$p^k(1-p)^{n-k}$**: Probability of one specific sequence. For fair coin, $p^n = (0.5)^n$ for any sequence, so every sequence has the same probability.
>
> For a fair coin, $P(X = k) = \binom{n}{k}(0.5)^n$.

> [!success]- Solution (with theory)
>
> a) $P(X = 3) = \binom{5}{3}(0.5)^3(0.5)^2 = 10 \times 0.125 \times 0.25 = 10 \times 0.03125 = 0.3125$
>
> b) $P(X \geq 4) = P(X = 4) + P(X = 5)$
> $= \binom{5}{4}(0.5)^5 + \binom{5}{5}(0.5)^5$
> $= 5(0.03125) + 1(0.03125) = 0.15625 + 0.03125 = 0.1875$
>
> c) $P(1 \leq X \leq 3) = P(X=1) + P(X=2) + P(X=3)$
> $= \binom{5}{1}(0.5)^5 + \binom{5}{2}(0.5)^5 + 0.3125$
> $= 5(0.03125) + 10(0.03125) + 0.3125$
> $= 0.15625 + 0.3125 + 0.3125 = 0.78125$
>
> **Check:** $P(X=0) = 0.03125$. Total = 0.03125 + 0.78125 + 0.1875 = 1.0 ✅

---

### Problem M1: From CDF to Probability

The CDF of a random variable X is:

$$F_X(x) = \begin{cases} 0 & x < 0 \\ x^2 & 0 \leq x \leq 1 \\ 1 & x > 1 \end{cases}$$

a) Is X discrete or continuous? How can you tell?
b) Find $P(0.2 < X \leq 0.6)$
c) Find the PDF $f_X(x)$
d) Find $E[X]$

> [!info]- First-principle derivation
>
> The CDF is the "universal translator" for probability questions:
> - $P(a < X \leq b) = F(b) - F(a)$ — works for any distribution
> - For continuous X, $f(x) = F'(x)$ — derivative of CDF gives PDF
> - For discrete X, $p(x) = F(x) - F(x^-)$ — jump height at x gives PMF
>
> How to tell discrete vs continuous from CDF:
> - **Continuous:** CDF is a smooth, continuous function (no jumps)
> - **Discrete:** CDF is a step function (jumps at each possible value)
> - **Mixed:** CDF has some jumps and some smooth parts (rare)

> [!success]- Solution (with theory)
>
> a) **Continuous.** The CDF has no jumps — it's a smooth curve $F(x) = x^2$ on [0,1]. A discrete CDF would jump at specific values and be flat in between.
>
> b) $P(0.2 < X \leq 0.6) = F(0.6) - F(0.2) = (0.6)^2 - (0.2)^2 = 0.36 - 0.04 = 0.32$
>
> c) $f_X(x) = F'(x) = \begin{cases} 0 & x < 0 \\ 2x & 0 \leq x \leq 1 \\ 0 & x > 1 \end{cases}$
>
> **Verification:** $\int_0^1 2x\,dx = [x^2]_0^1 = 1$ ✅
>
> d) $E[X] = \int_{-\infty}^{\infty} x f(x)\,dx = \int_0^1 x(2x)\,dx = \int_0^1 2x^2\,dx = \left[\frac{2x^3}{3}\right]_0^1 = \frac{2}{3}$

---

### Problem M2: Bernoulli + Binomial Connection

A multiple-choice test has 10 questions, each with 4 options. A student guesses randomly on every question. Let X = number of correct answers.

a) What distribution does X follow?
b) Find the probability of exactly 3 correct answers
c) Find the probability of at least 2 correct answers
d) Find $E[X]$ and $\text{Var}(X)$
e) How many questions must the student answer to expect at least 5 correct by guessing?

> [!info]- First-principle derivation
>
> Each question is a Bernoulli trial: correct (p=1/4) or incorrect (3/4). The sum of 10 independent Bernoullis is Binomial(10, 1/4).
>
> The mean $np = 10(0.25) = 2.5$ tells us: even with pure guessing, the student averages 2.5 correct answers. For part (e), we solve $np \geq 5$ → $n \geq 20$.

> [!success]- Solution (with theory)
>
> a) $X \sim \text{Binomial}(n=10, p=0.25)$
>
> b) $P(X=3) = \binom{10}{3}(0.25)^3(0.75)^7$
> $= 120 \times 0.015625 \times 0.13348 \approx 120 \times 0.002086 \approx 0.2503$
>
> c) $P(X \geq 2) = 1 - P(X=0) - P(X=1)$
> $P(X=0) = \binom{10}{0}(0.25)^0(0.75)^{10} = (0.75)^{10} \approx 0.0563$
> $P(X=1) = \binom{10}{1}(0.25)^1(0.75)^9 = 10 \times 0.25 \times (0.75)^9$
> $= 10 \times 0.25 \times 0.07508 \approx 0.1877$
> $P(X \geq 2) = 1 - 0.0563 - 0.1877 = 0.7560$
>
> **Interpretation:** 75.6% chance of getting at least 2 right by guessing alone.
>
> d) $E[X] = np = 10(0.25) = 2.5$
> $\text{Var}(X) = np(1-p) = 10(0.25)(0.75) = 1.875$
> $\sigma_X = \sqrt{1.875} \approx 1.369$
>
> e) Need $E[X] = n(0.25) \geq 5$ → $n \geq 20$ questions.

---

### Problem M3: PDF Properties

A random variable X has PDF:

$$f_X(x) = \begin{cases} kx & 0 \leq x \leq 2 \\ 0 & \text{otherwise} \end{cases}$$

a) Find k so that this is a valid PDF
b) Find $P(0.5 < X < 1.5)$
c) Find the CDF
d) Find $E[X]$ and $\text{Var}(X)$

> [!info]- First-principle derivation
>
> **The anatomy of a PDF problem:**
>
> A PDF must satisfy two conditions. Think of them as the "rules of the road" for density functions:
>
> **Rule 1: Non-negativity.** $f(x) \geq 0$. Probability can't be negative. Here, $f(x) = kx$ on $[0,2]$. Since $x \geq 0$, we need $k \geq 0$ for the PDF to be non-negative.
>
> **Rule 2: Total area = 1.** $\int_{-\infty}^{\infty} f(x)\,dx = 1$. This is the continuous equivalent of $\sum p(x) = 1$. The total probability must be exactly 1.
>
> Integrating $kx$ from 0 to 2:
> $$\int_0^2 kx\,dx = k\left[\frac{x^2}{2}\right]_0^2 = k \cdot \frac{4}{2} = 2k$$
>
> Setting this equal to 1: $2k = 1 \rightarrow k = 0.5$.
>
> **Finding the CDF from PDF:**
>
> The CDF is $F(x) = \int_{-\infty}^x f(t)\,dt$. This is a cumulative sum — at each point x, it tells you the total probability accumulated so far.
>
> For $x < 0$: nothing accumulated yet → $F(x) = 0$.
>
> For $0 \leq x \leq 2$: accumulate from 0 to x:
> $$F(x) = \int_0^x 0.5t\,dt = 0.5\left[\frac{t^2}{2}\right]_0^x = \frac{x^2}{4}$$
>
> For $x > 2$: everything accumulated → $F(x) = 1$.
>
> **Check:** $F(2) = 4/4 = 1$ — the CDF reaches 1 exactly at the upper bound. This confirms our normalization is correct.
>
> **Computing expectation:**
>
> $E[X] = \int x f(x)\,dx$. Plug in $f(x) = 0.5x$:
> $$E[X] = \int_0^2 x(0.5x)\,dx = 0.5\int_0^2 x^2\,dx$$
>
> This is the first moment of the distribution — the center of mass of the density shape.

> [!success]- Solution (with theory)
>
> a) $\int_0^2 kx\,dx = \left[\frac{kx^2}{2}\right]_0^2 = \frac{k(4)}{2} = 2k = 1$
> So $k = 0.5$.
>
> **Check:** $f(x) = 0.5x \geq 0$ on [0,2] ✅
>
> b) $P(0.5 < X < 1.5) = \int_{0.5}^{1.5} 0.5x\,dx = \left[\frac{x^2}{4}\right]_{0.5}^{1.5} = \frac{2.25}{4} - \frac{0.25}{4} = \frac{2}{4} = 0.5$
>
> c) For $x < 0$: $F(x) = 0$
> For $0 \leq x \leq 2$: $F(x) = \int_0^x 0.5t\,dt = \left[\frac{t^2}{4}\right]_0^x = \frac{x^2}{4}$
> For $x > 2$: $F(x) = 1$
>
> $$F_X(x) = \begin{cases} 0 & x < 0 \\ \frac{x^2}{4} & 0 \leq x \leq 2 \\ 1 & x > 2 \end{cases}$$
>
> **Check:** $F(2) = 4/4 = 1$ ✅
>
> d) $E[X] = \int_0^2 x(0.5x)\,dx = \int_0^2 0.5x^2\,dx = \left[\frac{x^3}{6}\right]_0^2 = \frac{8}{6} = \frac{4}{3}$
>
> $E[X^2] = \int_0^2 x^2(0.5x)\,dx = \int_0^2 0.5x^3\,dx = \left[\frac{x^4}{8}\right]_0^2 = \frac{16}{8} = 2$
>
> $\text{Var}(X) = 2 - \left(\frac{4}{3}\right)^2 = 2 - \frac{16}{9} = \frac{18-16}{9} = \frac{2}{9}$

---

### Problem M4: Binomial Parameter Estimation (Reverse Problem)

In a survey of 200 randomly selected voters, 120 support a policy.

a) If $X$ = number of supporters in a sample of 200, what's the distribution if true support is p?
b) Find the value of p that makes the observed result most likely (hint: maximize $P(X=120)$)
c) What's the expected number of supporters if p = 0.55? The standard deviation?

> [!info]- First-principle derivation
>
> This problem reverses the typical Binomial question. Instead of "given p, find probability," we ask "given the observation, what's the most plausible p?"
>
> The function $L(p) = \binom{200}{120}p^{120}(1-p)^{80}$ is the **likelihood** of p. Maximizing it gives p̂ = 120/200 = 0.6 — the sample proportion.
>
> This is the foundation of **Maximum Likelihood Estimation (MLE)**: the MLE for p in a Binomial is always the sample proportion.

> [!success]- Solution (with theory)
>
> a) $X \sim \text{Binomial}(200, p)$
>
> b) $P(X=120) = \binom{200}{120}p^{120}(1-p)^{80}$
>
> To find the p that maximizes this: the sample proportion $p = \frac{120}{200} = 0.6$ is the maximum likelihood estimate.
>
> **Why?** Intuitively, the most likely p is the one that matches what we observed. Formally, take log, differentiate, set to 0:
> $$\frac{d}{dp}[120\ln p + 80\ln(1-p)] = \frac{120}{p} - \frac{80}{1-p} = 0$$
> $$120(1-p) = 80p$$
> $$120 - 120p = 80p$$
> $$120 = 200p$$
> $$p = 0.6$$
>
> c) If $p = 0.55$:
> $E[X] = np = 200(0.55) = 110$
> $\text{Var}(X) = 200(0.55)(0.45) = 49.5$
> $\sigma_X = \sqrt{49.5} \approx 7.04$

---

### Problem T1: Mixed Distribution (Discrete + Continuous)

A random variable X is defined as follows:
- $P(X = 0) = 0.3$
- For $0 < x \leq 1$, the density is $f(x) = 0.7$ (constant)

a) Verify this is a valid distribution
b) Find the CDF
c) Find $P(0.2 < X < 0.8)$
d) Find $E[X]$

> [!info]- First-principle derivation
>
> **What is a mixed distribution?**
>
> Most random variables are either purely discrete (like coin flips) or purely continuous (like temperature). But some variables are **mixed** — they have both discrete atoms AND continuous density.
>
> **Example from real life:** Your total wealth. There's a discrete atom at 0 (many people have exactly $0), but for positive values, wealth is continuous.
>
> **How the total probability works:**
>
> A mixed distribution must still satisfy the total probability = 1 rule. But now the total has two parts:
>
> $$1 = \underbrace{P(X = 0)}_{\text{discrete mass}} + \underbrace{\int_0^1 f(x)\,dx}_{\text{continuous density}}$$
>
> Here, $P(X=0) = 0.3$ means 30% of the probability is concentrated at the single point $x=0$. This is a "spike" of probability mass.
>
> The remaining 70% is spread continuously over $(0, 1]$ with constant density $f(x) = 0.7$. The area under this density is $0.7 \times 1 = 0.7$.
>
> Total: $0.3 + 0.7 = 1.0$ ✅
>
> **How the CDF behaves:**
>
> The CDF accumulates probability from left to right:
> - Below 0: nothing → $F = 0$
> - At $x=0$: we hit the discrete atom. The CDF jumps from 0 to 0.3 **instantaneously**. This jump height = $P(X=0) = 0.3$.
> - Between 0 and 1: the CDF grows continuously as we accumulate density: $F(x) = 0.3 + \int_0^x 0.7\,dt = 0.3 + 0.7x$
> - At $x=1$: we've accumulated everything → $F = 1$
>
> **How expectation works for mixed distributions:**
>
> The expectation is the sum of two parts:
> $$E[X] = \underbrace{\sum_{\text{atoms}} x \cdot P(X=x)}_{\text{discrete contribution}} + \underbrace{\int x f(x)\,dx}_{\text{continuous contribution}}$$
>
> The discrete part contributes $0 \times 0.3 = 0$ (since the atom is at 0). The continuous part contributes $\int_0^1 0.7x\,dx = 0.35$. Total: $E[X] = 0.35$.
>
> **Key insight:** Mixed distributions are just "both types combined." You handle each part with its own tool (sum for discrete, integral for continuous), then add the results.

> [!success]- Solution (with theory)
>
> a) Discrete atom at 0 contributes probability 0.3.
> Continuous part: $\int_0^1 0.7\,dx = 0.7$
> Total: $0.3 + 0.7 = 1.0$ ✅
>
> b) For $x < 0$: $F(x) = 0$
> At $x = 0$: $F(0) = P(X \leq 0) = P(X=0) = 0.3$ (jump!)
> For $0 < x < 1$: $F(x) = 0.3 + \int_0^x 0.7\,dt = 0.3 + 0.7x$
> For $x \geq 1$: $F(x) = 1$
>
> $$F_X(x) = \begin{cases} 0 & x < 0 \\ 0.3 + 0.7x & 0 \leq x < 1 \\ 1 & x \geq 1 \end{cases}$$
>
> **Note:** There's a jump of 0.3 at x=0, then a linear ramp from 0.3 to 1.
>
> c) $P(0.2 < X < 0.8) = F(0.8) - F(0.2) = (0.3 + 0.7 \times 0.8) - (0.3 + 0.7 \times 0.2)$
> $= (0.3 + 0.56) - (0.3 + 0.14) = 0.86 - 0.44 = 0.42$
>
> (Could also compute directly: $\int_{0.2}^{0.8} 0.7\,dx = 0.7 \times 0.6 = 0.42$)
>
> d) $E[X] = \underbrace{0 \times 0.3}_{\text{atom at 0}} + \int_0^1 x(0.7)\,dx = 0.7\left[\frac{x^2}{2}\right]_0^1 = 0.7 \times 0.5 = 0.35$

---

### Problem T2: CDF to Distribution Type

For each CDF below, determine if the distribution is discrete, continuous, or mixed:

a) $F(x) = \begin{cases} 0 & x < 0 \\ 1 - e^{-x} & x \geq 0 \end{cases}$
b) $F(x) = \begin{cases} 0 & x < 0 \\ 0.5 & 0 \leq x < 2 \\ 1 & x \geq 2 \end{cases}$
c) $F(x) = \begin{cases} 0 & x < 0 \\ \frac{x}{2} & 0 \leq x < 1 \\ \frac{2x-1}{2} & 1 \leq x < 2 \\ 1 & x \geq 2 \end{cases}$

> [!info]- First-principle derivation
>
> The shape of the CDF tells you the distribution type:
> - **Smooth, continuous** → continuous distribution (CDF has no jumps)
> - **Step function** (flat, jumps) → discrete distribution
> - **Jumps + smooth curves** → mixed distribution
>
> Jumps in the CDF indicate probability mass at that point (discrete atoms). The height of the jump = $P(X = \text{that point})$.

> [!success]- Solution (with theory)
>
> a) **Continuous.** The CDF is $F(x) = 1 - e^{-x}$ for $x \geq 0$, which is smooth with no jumps. At $x=0$, $F(0) = 0$ (no jump). This is the **Exponential distribution**, which we'll cover soon.
>
> b) **Discrete.** The CDF is flat except for jumps at $x=0$ (jump of 0.5) and $x=2$ (jump of 0.5). This means $P(X=0) = 0.5$, $P(X=2) = 0.5$. Two equally likely points.
>
> c) **Mixed.** There's a jump at $x=0$: $F(0) - F(0^-) = 0 - 0 = 0$... Wait, let's check more carefully.
>
> At $x=0$: $F(0) = 0/2 = 0$. No jump at 0.
> At $x=1$: $F(1^-) = 1/2$, $F(1) = (2(1)-1)/2 = 1/2$. No jump at 1 either.
>
> The function is continuous everywhere (no jumps) but piecewise linear with different slopes: slope = 1/2 on [0,1) and slope = 1 on [1,2). This is a **continuous** distribution with a piecewise PDF:
> $$f(x) = \begin{cases} 1/2 & 0 < x < 1 \\ 1 & 1 < x < 2 \end{cases}$$

---

### Problem T3: Sum of Independent Binomials

Two students take different tests:
- Student A answers 15 true/false questions by guessing: $X \sim \text{Binomial}(15, 0.5)$
- Student B answers 10 multiple-choice questions (4 options each) by guessing: $Y \sim \text{Binomial}(10, 0.25)$

If they take the tests independently:
a) Find $E[X + Y]$ and $\text{Var}(X + Y)$
b) Find $P(X + Y \geq 15)$ approximately (use normal approximation — preview of CLT!)

> [!info]- First-principle derivation
>
> When independent random variables are added:
> - Means add: $E[X+Y] = E[X] + E[Y]$ (always true)
> - Variances add: $\text{Var}(X+Y) = \text{Var}(X) + \text{Var}(Y)$ (only if independent)
>
> The sum of independent Binomials is NOT binomial unless they have the same p. Here, p differs (0.5 vs 0.25), so X+Y follows some other distribution.

> [!success]- Solution (with theory)
>
> a) $E[X] = 15(0.5) = 7.5$, $\text{Var}(X) = 15(0.5)(0.5) = 3.75$
> $E[Y] = 10(0.25) = 2.5$, $\text{Var}(Y) = 10(0.25)(0.75) = 1.875$
>
> By independence:
> $E[X+Y] = 7.5 + 2.5 = 10$
> $\text{Var}(X+Y) = 3.75 + 1.875 = 5.625$
> $\sigma_{X+Y} = \sqrt{5.625} \approx 2.372$
>
> b) Normal approximation to the sum (both n are large enough):
> $X+Y \approx \text{Normal}(\mu=10, \sigma=2.372)$
>
> $P(X+Y \geq 15) = P\left(Z \geq \frac{15-10}{2.372}\right) \approx P(Z \geq 2.108)$
> From standard normal tables: $P(Z \geq 2.108) \approx 0.0175$
>
> **Interpretation:** Only about 1.75% chance that the combined guessing score reaches 15. This is why tests with enough questions can reliably distinguish guessers from prepared students.

---

> Say **"done session-003"** when you've worked through these. Next: Session 004 — More Distributions (Poisson, Exponential, Normal, Standard Normal).
