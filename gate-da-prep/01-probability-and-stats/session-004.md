# Session 004 — Poisson Distribution: The Documentary

> **📅 Expected:** Jun 21 – Jun 24 | **Buffer:** +13 days 🟢 | **Status:** 📄 Doc ready (written ahead of schedule)
>
> A first-principles journey through the law of rare events.
> Read like a story — every formula is derived, never stated.

---

## Chapter 1: The Bridge — From Binomial to the Law of Rare Events

### The problem with Binomial

The Binomial distribution works beautifully when you have:
- A fixed number of trials $n$
- A fixed probability of success $p$
- Independent trials

But what about this scenario: **horse kicks in the Prussian army**.

In 1898, Ladislaus Bortkiewicz studied 20 years of data across 10 army corps. He counted deaths by horse kick. Most years: zero deaths. Some years: one. Rarely: two. Almost never: three or more.

Can the Binomial describe this? Let's try. To use Binomial, you'd need $n$ (the number of "opportunities" for a horse kick in a year) and $p$ (the probability of a kick per opportunity).

But what's $n$? Every moment, every horse *could* kick. $n$ is basically infinite. And $p$? Vanishingly tiny.

The Binomial breaks here. Not because it's wrong — but because you'd need to know two numbers ($n$ and $p$) that you simply can't measure.

### The big idea

What if we could have a distribution that needs only **one number** — the average rate at which events happen?

Here's the setup. Imagine a Binomial situation where:
- $n$ is huge (approaching infinity)
- $p$ is tiny (approaching zero)
- But the product $np$ stays fixed at some constant value $\lambda$

Why fix $np$? Because $np$ is the **expected count** — the average number of events. If you let $n$ blow up and $p$ shrink without controlling the product:
- If $np$ grows → expected count explodes to infinity
- If $np$ shrinks → expected count collapses to zero

Neither is useful. But keeping $np = \lambda$ fixed means: "the average number of events stays the same, but the events become infinitely rare and the opportunities infinitely many."

This is the **law of rare events**: when you have a huge number of opportunities for something to happen, each with a tiny probability, the count follows a Poisson distribution.

Let's derive it.

---

## Chapter 2: The Derivation — From Binomial to Poisson, Step by Step

### Step 1: Start from the Binomial PMF

The Binomial PMF:

$$P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}$$

Now substitute $p = \lambda/n$ (since $np = \lambda$, we have $p = \lambda/n$):

$$P(X = k) = \binom{n}{k} \left(\frac{\lambda}{n}\right)^k \left(1 - \frac{\lambda}{n}\right)^{n-k}$$

### Step 2: Expand the binomial coefficient

$$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$

But there's a more useful form for limits. Write it as:

$$\binom{n}{k} = \frac{n(n-1)(n-2)...(n-k+1)}{k!}$$

The numerator has $k$ terms, starting at $n$ and counting down. For example, for $k=3$:

$$\binom{n}{3} = \frac{n(n-1)(n-2)}{3!}$$

So:

$$P(X = k) = \frac{n(n-1)(n-2)...(n-k+1)}{k!} \cdot \frac{\lambda^k}{n^k} \cdot \left(1 - \frac{\lambda}{n}\right)^{n-k}$$

### Step 3: Reorganize into four factors

Let me separate the parts that depend on $n$ from the parts that don't:

$$P(X = k) = \frac{\lambda^k}{k!} \cdot \frac{n(n-1)...(n-k+1)}{n^k} \cdot \left(1 - \frac{\lambda}{n}\right)^n \cdot \left(1 - \frac{\lambda}{n}\right)^{-k}$$

Why did I split $(1 - \lambda/n)^{n-k}$ into $(1 - \lambda/n)^n \cdot (1 - \lambda/n)^{-k}$? Because each part has a different limit behavior, and separating them lets us handle each one independently.

**Verification of the split:**

$$\left(1 - \frac{\lambda}{n}\right)^n \cdot \left(1 - \frac{\lambda}{n}\right)^{-k} = \left(1 - \frac{\lambda}{n}\right)^{n + (-k)} = \left(1 - \frac{\lambda}{n}\right)^{n-k}$$ ✅

Now we have:

$$P(X = k) = \underbrace{\frac{\lambda^k}{k!}}_{\text{Fixed}} \cdot \underbrace{\frac{n(n-1)...(n-k+1)}{n^k}}_{\text{Factor A}} \cdot \underbrace{\left(1 - \frac{\lambda}{n}\right)^n}_{\text{Factor B}} \cdot \underbrace{\left(1 - \frac{\lambda}{n}\right)^{-k}}_{\text{Factor C}}$$

The first term $\frac{\lambda^k}{k!}$ doesn't depend on $n$ at all. The three factors A, B, C all involve $n$, and we need to see what happens to each as $n \to \infty$.

### Step 4: Take the limit $n \to \infty$ for each factor

**Factor A: $\frac{n(n-1)...(n-k+1)}{n^k}$**

Write this as a product of $k$ separate fractions:

$$\frac{n}{n} \cdot \frac{n-1}{n} \cdot \frac{n-2}{n} \cdot ... \cdot \frac{n-k+1}{n}$$

Each fraction is $\frac{n-j}{n} = 1 - \frac{j}{n}$, where $j$ goes from $0$ to $k-1$.

As $n$ gets huge, $\frac{j}{n}$ becomes tiny. Let's test with numbers:

If $n = 1,000,000$ and $j = 3$:
$$1 - \frac{3}{1,000,000} = 0.999997$$

That's basically 1. In the limit:

$$\lim_{n\to\infty} \left(1 - \frac{j}{n}\right) = 1 \quad \text{for any fixed } j$$

So each of the $k$ fractions approaches 1, and their product approaches $1^k = 1$:

$$\boxed{\text{Factor A} \to 1}$$

**Factor B: $\left(1 - \frac{\lambda}{n}\right)^n$**

This is the most important limit in all of probability — it's the one that defines $e$:

$$e = \lim_{n\to\infty} \left(1 + \frac{1}{n}\right)^n$$

More generally, for any constant $x$:

$$e^x = \lim_{n\to\infty} \left(1 + \frac{x}{n}\right)^n$$

Here we have $-\lambda$ instead of $x$:

$$\boxed{\lim_{n\to\infty} \left(1 - \frac{\lambda}{n}\right)^n = e^{-\lambda}}$$

**Why does this work?** As $n$ grows, the base $(1 - \lambda/n)$ inches toward 1, but the exponent $n$ grows large. These two effects balance each other to produce $e^{-\lambda}$. For any finite $n$, $(1 - \lambda/n)^n$ is an approximation to $e^{-\lambda}$, and the approximation gets better as $n$ grows.

**Numerical check for $\lambda = 2$:**

| $n$ | $(1 - 2/n)^n$ | $e^{-2}$ |
|---|---|---|
| 10 | $(0.8)^{10} \approx 0.107$ | 0.1353 |
| 100 | $(0.98)^{100} \approx 0.133$ | 0.1353 |
| 1000 | $(0.998)^{1000} \approx 0.135$ | 0.1353 |
| 10000 | $(0.9998)^{10000} \approx 0.1353$ | 0.1353 |

The numbers are homing in on $e^{-2}$. ✅

**Factor C: $\left(1 - \frac{\lambda}{n}\right)^{-k}$**

As $n \to \infty$, $\frac{\lambda}{n} \to 0$, so the base $(1 - \lambda/n) \to 1$. No matter what $k$ is:

$$\lim_{n\to\infty} \left(1 - \frac{\lambda}{n}\right)^{-k} = 1^{-k} = 1$$

$$\boxed{\text{Factor C} \to 1}$$

### Step 5: The Poisson PMF emerges

Now put all three factors together:

$$\lim_{n\to\infty} P(X = k) = \frac{\lambda^k}{k!} \cdot 1 \cdot e^{-\lambda} \cdot 1 = \frac{e^{-\lambda} \lambda^k}{k!}$$

$$\boxed{P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!}, \quad k = 0, 1, 2, ...}$$

This is the **Poisson distribution**. We write: $X \sim \text{Poisson}(\lambda)$.

### Understanding what we just did

We started with the Binomial — a distribution with two parameters $(n, p)$. We took the limit $n \to \infty$, $p \to 0$, while keeping $np = \lambda$ fixed. The result is a distribution with a single parameter $\lambda$.

The Poisson is what the Binomial **becomes** when events are numerous but individually rare. That's why it's called the "law of rare events."

---

## Chapter 3: Verifying It's a Valid PMF

### Does it sum to 1?

A valid PMF must have all probabilities sum to 1:

$$\sum_{k=0}^{\infty} P(X = k) = \sum_{k=0}^{\infty} \frac{e^{-\lambda} \lambda^k}{k!} = e^{-\lambda} \sum_{k=0}^{\infty} \frac{\lambda^k}{k!}$$

The sum $\sum_{k=0}^{\infty} \frac{\lambda^k}{k!}$ is the Taylor series expansion of $e^{\lambda}$:

$$e^{\lambda} = 1 + \lambda + \frac{\lambda^2}{2!} + \frac{\lambda^3}{3!} + ... = \sum_{k=0}^{\infty} \frac{\lambda^k}{k!}$$

So:

$$\sum_{k=0}^{\infty} P(X = k) = e^{-\lambda} \cdot e^{\lambda} = e^{0} = 1 \quad \text{✅}$$

### Is it non-negative?

$e^{-\lambda} > 0$, $\lambda^k \geq 0$, and $k! > 0$ for all $k$. So:

$$P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!} \geq 0 \quad \text{for all } k$$ ✅

### The PMF in words

The Poisson PMF has two competing forces:
- $\lambda^k$ grows with $k$ (makes larger $k$ more likely, up to a point)
- $k!$ grows even faster (factorial always beats power eventually)
- $e^{-\lambda}$ is a constant normalizing factor

The peak occurs near $k = \lambda$ (the mean), and the probabilities decay rapidly beyond that.

---

## Chapter 4: Deriving the CDF

### The CDF definition

For a discrete distribution, the CDF is:

$$F(k) = P(X \leq k) = \sum_{i=0}^{k} \frac{e^{-\lambda} \lambda^i}{i!}$$

There's no closed-form simplification — the sum doesn't collapse to a simple algebraic expression. So the Poisson CDF is usually evaluated numerically or using tables.

### The incomplete gamma function connection

For the mathematically curious: the Poisson CDF is related to the incomplete gamma function:

$$P(X \leq k) = \frac{\Gamma(k+1, \lambda)}{k!}$$

where $\Gamma(a, x) = \int_x^{\infty} t^{a-1} e^{-t} dt$ is the upper incomplete gamma function. You don't need to memorize this for GATE, but it's why you'll see "Poisson CDF" in statistical tables.

### Using the CDF for probability calculations

The CDF is most useful for computing cumulative probabilities:

$$P(a \leq X \leq b) = F(b) - F(a-1)$$

$$P(X > k) = 1 - F(k)$$

$$P(X \geq k) = 1 - F(k-1)$$

**Example:** For $\lambda = 4$, find $P(2 \leq X \leq 4)$:

$$P(2 \leq X \leq 4) = P(X=2) + P(X=3) + P(X=4)$$

$$= F(4) - F(1)$$

We'll compute individual terms since the CDF doesn't simplify:

$$P(X=2) = \frac{e^{-4} \cdot 16}{2} = 8e^{-4} \approx 0.1465$$
$$P(X=3) = \frac{e^{-4} \cdot 64}{6} \approx 10.667e^{-4} \approx 0.1954$$
$$P(X=4) = \frac{e^{-4} \cdot 256}{24} \approx 10.667e^{-4} \approx 0.1954$$

$$P(2 \leq X \leq 4) \approx 0.1465 + 0.1954 + 0.1954 = 0.5373$$

---

## Chapter 5: Deriving the Mean — $E[X] = \lambda$

### Setting up the sum

$$E[X] = \sum_{k=0}^{\infty} k \cdot \frac{e^{-\lambda} \lambda^k}{k!}$$

The $k=0$ term is $0 \cdot e^{-\lambda} \lambda^0/0! = 0$, so we can start from $k=1$:

$$E[X] = \sum_{k=1}^{\infty} k \cdot \frac{e^{-\lambda} \lambda^k}{k!}$$

### The factorial simplification trick

Here's the key simplification. Notice that:

$$\frac{k}{k!} = \frac{k}{k \cdot (k-1)!} = \frac{1}{(k-1)!}$$

Why? Because $k! = k \cdot (k-1) \cdot (k-2) \cdot ... \cdot 1 = k \cdot (k-1)!$. So dividing $k$ by $k!$ cancels the $k$, leaving $1/(k-1)!$.

Applying this:

$$E[X] = \sum_{k=1}^{\infty} \frac{e^{-\lambda} \lambda^k}{(k-1)!}$$

### Pull out a factor of $\lambda$

$$E[X] = \lambda \sum_{k=1}^{\infty} \frac{e^{-\lambda} \lambda^{k-1}}{(k-1)!}$$

### Change the index

Let $j = k-1$. When $k=1$, $j=0$. When $k \to \infty$, $j \to \infty$:

$$E[X] = \lambda \sum_{j=0}^{\infty} \frac{e^{-\lambda} \lambda^{j}}{j!}$$

### Recognize the sum

What's $\sum_{j=0}^{\infty} \frac{e^{-\lambda} \lambda^{j}}{j!}$? It's the sum of all Poisson probabilities — which we proved equals 1 in Chapter 3.

$$E[X] = \lambda \cdot 1 = \lambda$$

$$\boxed{E[X] = \lambda}$$

### Understanding the formula

The mean of a Poisson is simply $\lambda$. This confirms our original setup: $np = \lambda$ was the expected count, and that expectation carries through the limit.

If $\lambda = 4$ calls per minute, the expected number of calls in a minute is 4. If $\lambda = 0.5$ defects per batch, the expected number of defects is 0.5.

**What happens when $\lambda$ is not an integer?** The mean doesn't have to be a possible outcome. For $\lambda = 2.7$, the mean is 2.7 even though $X$ can only be 0, 1, 2, 3, ... This is fine — the center of mass can sit between integer values.

---

## Chapter 6: Deriving the Variance — $\text{Var}(X) = \lambda$

### Strategy: Compute $E[X(X-1)]$ first

Instead of computing $E[X^2]$ directly, there's a clever trick: compute $E[X(X-1)]$ first. The factorial cancellation is much cleaner this way.

$$E[X(X-1)] = \sum_{k=0}^{\infty} k(k-1) \cdot \frac{e^{-\lambda} \lambda^k}{k!}$$

The $k=0$ term is $0$ (killed by $k=0$). The $k=1$ term is also $0$ (killed by $k-1=0$). So start from $k=2$:

$$E[X(X-1)] = \sum_{k=2}^{\infty} k(k-1) \cdot \frac{e^{-\lambda} \lambda^k}{k!}$$

### The factorial cancellation

$$\frac{k(k-1)}{k!} = \frac{k(k-1)}{k(k-1)(k-2)!} = \frac{1}{(k-2)!}$$

Let me verify: $k! = k \cdot (k-1) \cdot (k-2)!$. So $\frac{k(k-1)}{k(k-1)(k-2)!} = \frac{1}{(k-2)!}$. ✅

So:

$$E[X(X-1)] = \sum_{k=2}^{\infty} \frac{e^{-\lambda} \lambda^k}{(k-2)!}$$

### Factor out $\lambda^2$

$$E[X(X-1)] = \lambda^2 \sum_{k=2}^{\infty} \frac{e^{-\lambda} \lambda^{k-2}}{(k-2)!}$$

### Change the index

Let $j = k-2$. When $k=2$, $j=0$:

$$E[X(X-1)] = \lambda^2 \sum_{j=0}^{\infty} \frac{e^{-\lambda} \lambda^{j}}{j!} = \lambda^2 \cdot 1 = \lambda^2$$

### Connect back to $E[X^2]$

$$E[X(X-1)] = E[X^2 - X] = E[X^2] - E[X]$$

So:

$$E[X^2] = E[X(X-1)] + E[X] = \lambda^2 + \lambda$$

### Apply the variance shortcut

$$\text{Var}(X) = E[X^2] - (E[X])^2 = (\lambda^2 + \lambda) - \lambda^2 = \lambda$$

$$\boxed{\text{Var}(X) = \lambda}$$

### Understanding the formula

**Mean = Variance.** This is unique. No other common distribution has this property.

| Distribution | Mean | Variance | Mean ? Variance |
|---|---|---|---|
| **Poisson($\lambda$)** | $\lambda$ | $\lambda$ | **Equal** |
| Bernoulli($p$) | $p$ | $p(1-p)$ | $>$ (unless $p=0$ or $1$) |
| Binomial($n,p$) | $np$ | $np(1-p)$ | $>$ (unless $p=0$ or $1$) |
| Exponential($\lambda$) | $1/\lambda$ | $1/\lambda^2$ | $\neq$ |
| Uniform($a,b$) | $(a+b)/2$ | $(b-a)^2/12$ | $\neq$ |
| Normal($\mu,\sigma^2$) | $\mu$ | $\sigma^2$ | $\neq$ |

**What mean = variance tells us about the data:**

- If you're counting events and the mean equals the variance, Poisson is a good fit
- If the variance is larger than the mean, you have **overdispersion** (more spread than Poisson allows)
- If the variance is smaller than the mean, you have **underdispersion** (less spread than Poisson allows)

This is a useful diagnostic check in practice.

---

## Chapter 7: Understanding $\lambda$ — The Many Faces of One Number

### What $\lambda$ controls

$\lambda$ is the single parameter of the Poisson, and it controls everything:

- **Center:** $E[X] = \lambda$
- **Spread:** $\text{Var}(X) = \lambda$, $\sigma = \sqrt{\lambda}$
- **Shape:** As $\lambda$ grows, the distribution becomes more symmetric

### Mean = Standard Deviation? No — let's check

Wait — I said mean = variance, not mean = SD. Let's be precise:

- Mean = $\lambda$
- Variance = $\lambda$
- Standard deviation = $\sqrt{\lambda}$

For $\lambda = 4$: SD = $2$, mean = $4$. SD is half the mean.
For $\lambda = 16$: SD = $4$, mean = $16$. SD is one-quarter of the mean.
For $\lambda = 100$: SD = $10$, mean = $100$. SD is one-tenth of the mean.

The $SD/Mean$ ratio = $\sqrt{\lambda}/\lambda = 1/\sqrt{\lambda}$ — it shrinks as $\lambda$ grows.

### The approach to Normality

As $\lambda$ increases, the Poisson distribution starts looking like a Normal bell curve:

| $\lambda$ | Mean | SD ($\sqrt{\lambda}$) | SD/Mean | Shape |
|---|---|---|---|---|
| 1 | 1 | 1 | 100% | Very lopsided — most mass at 0 and 1 |
| 4 | 4 | 2 | 50% | Still lopsided but improving |
| 10 | 10 | 3.16 | 31.6% | Starting to look symmetric |
| 50 | 50 | 7.07 | 14.1% | Nearly bell-shaped |
| 100 | 100 | 10 | 10% | Essentially a bell curve |

The key insight: the spread ($\sqrt{\lambda}$) grows, but the center ($\lambda$) grows **faster**. So the spread becomes a smaller fraction of the center, and the distribution "smooths out."

### See it

![[assets/poisson-lambda-comparison.png]]

Look at what happens across the four panels:
- **λ = 1:** Totally lopsided. Most probability at 0 and 1, long skinny tail.
- **λ = 4:** Better. Mass centered around 4, but still slightly right-skewed.
- **λ = 10:** Almost symmetric. Forms a rough bell shape.
- **λ = 50:** Practically a bell curve. If you didn't know it was Poisson, you'd guess Normal.

### Extreme cases

- **λ = 0:** No events ever. $P(X=0) = e^0 \cdot 0^0/0! = 1$. Wait — $0^0$ is undefined. Let's handle this properly.

For $\lambda = 0$, the PMF gives: $P(X=0) = e^{-0} \cdot 0^0/0!$. The term $0^0$ is technically an indeterminate form. But we interpret it from the limit: as $\lambda \to 0^+$, $P(X=0) = e^{-\lambda} \to 1$. So $\lambda = 0$ means "certainly zero events."

- **λ = 1:** $P(X=0) = e^{-1} \approx 0.368$, $P(X=1) = e^{-1} \approx 0.368$, $P(X=2) = e^{-1}/2 \approx 0.184$
- **λ = 5:** $P(X=0) = e^{-5} \approx 0.0067$, $P(X=5) = e^{-5}5^5/120 \approx 0.175$

Notice for $\lambda = 1$, $P(X=0) = P(X=1)$ — they're equal. For $\lambda = 5$, the peak is at $k = 5$ (the mean and mode are close but not necessarily equal for discrete distributions).

---

## Chapter 8: The Poisson Process — When Does Poisson Apply?

### Three conditions

A Poisson distribution is appropriate when events satisfy three properties:

1. **Independence:** One event doesn't affect the probability of another. A horse kick doesn't make another horse kick more or less likely.

2. **Constant average rate:** $\lambda$ doesn't change over time or space. The rate of horse kicks per year is roughly constant.

3. **Rare at any instant:** At any tiny moment, the chance of an event is basically zero (even though over a long period, $\lambda$ may be large).

These three conditions define a **Poisson process** — a sequence of events arriving randomly at a constant rate.

### $\lambda$ scales with the interval

One of the most important things to remember: **$\lambda$ scales with the length of the interval.**

- If calls arrive at 4 per minute, then in 1 minute: $\lambda = 4$
- In 5 minutes: $\lambda = 4 \times 5 = 20$
- In 30 seconds (0.5 minutes): $\lambda = 4 \times 0.5 = 2$

The Poisson PMF for any interval is:

$$P(X = k \text{ events in interval of length } t) = \frac{e^{-\lambda t} (\lambda t)^k}{k!}$$

### Real-world examples

- Number of emails in an hour
- Number of car accidents at an intersection per year
- Number of radioactive decays from a sample per second
- Number of typos on a page of a book
- Number of website visits per minute
- Number of support calls per hour

### One parameter to rule them all

The Binomial needs two numbers ($n$ and $p$). The Poisson only needs one ($\lambda$). That's the whole point — when you don't know $n$ or $p$ individually but know their product, Poisson gets the job done.

---

## Chapter 9: Why Poisson Matters — Real-World Importance

### 1. The natural model for counts

Whenever you're counting rare independent events over a fixed interval, Poisson is the default model. It's the "go-to" for count data — just as Normal is the go-to for continuous data.

### 2. Queueing theory

Poisson arrivals are the standard assumption in queueing theory. Together with Exponential service times, they form the M/M/1 queue — the simplest and most fundamental model of waiting lines.

### 3. The Binomial approximation

When $n$ is large and $p$ is small, Poisson approximates Binomial with $\lambda = np$. This saves you from computing enormous binomial coefficients:

$$\binom{5000}{5} p^5 (1-p)^{4995} \approx \frac{e^{-np} (np)^5}{5!}$$

### 4. Radiative decay

Radioactive decay follows a Poisson process. The number of decays in a fixed time interval is Poisson, and the time between decays is Exponential — giving us the bridge to Session 005.

### 5. Insurance and risk modeling

Insurance companies model rare events (accidents, claims, natural disasters) using Poisson. The "rare events" condition fits perfectly.

### 6. GATE DA relevance

Poisson appears in GATE DA exams in several forms:
- Computing probabilities from the PMF
- Adjusting $\lambda$ for different time intervals
- Poisson approximation of Binomial
- Mean = Variance property
- Connection to Exponential distribution

---

## Summary of Formulas

| Property | Formula |
|---|---|
| **PMF** | $P(X = k) = \dfrac{e^{-\lambda} \lambda^k}{k!}, \quad k = 0, 1, 2, ...$ |
| **CDF** | $P(X \leq k) = \sum_{i=0}^{k} \dfrac{e^{-\lambda} \lambda^i}{i!}$ (no closed form) |
| **Mean** | $E[X] = \lambda$ |
| **Variance** | $\text{Var}(X) = \lambda$ |
| **Std Dev** | $\sigma = \sqrt{\lambda}$ |
| **Support** | Non-negative integers |
| **Mean = Variance** | Unique among common distributions |

---

## Comparison: Poisson vs Binomial

| Aspect | Binomial($n,p$) | Poisson($\lambda$) |
|---|---|---|
| **Parameters** | $n$, $p$ | $\lambda$ |
| **When to use** | Fixed $n$, independent trials | Rare events, large $n$, small $p$ |
| **Mean** | $np$ | $\lambda$ |
| **Variance** | $np(1-p)$ | $\lambda$ |
| **Support** | $0, 1, ..., n$ | $0, 1, 2, ...$ |
| **Relation** | — | Limit as $n \to \infty$, $p \to 0$, $np \to \lambda$ |

---

## Practice Problems

---

### Problem E1: Customer Service Calls

A call center receives an average of 4 calls per minute. The calls follow a Poisson process.

a) What's the probability of exactly 2 calls in a given minute?
b) What's the probability of at least 1 call in a given minute?
c) What's the probability of 3 or more calls in a 2-minute period?

> [!info]- First-principle derivation
>
> **Why Poisson here?** Calls arrive independently (one call doesn't trigger another), at a roughly constant rate (4 per minute), and at any instant the chance of a call is tiny. All three Poisson conditions are satisfied.
>
> **Adjusting $\lambda$ for the interval:**
> - 1 minute: $\lambda = 4$
> - 2 minutes: $\lambda = 4 \times 2 = 8$
>
> **The "at least 1" trick:**
> $$P(X \geq 1) = 1 - P(X = 0) = 1 - e^{-\lambda}$$
> Always compute complement rather than summing an infinite series.
>
> **The "3 or more" trick:**
> $$P(X \geq 3) = 1 - P(X \leq 2) = 1 - [P(0) + P(1) + P(2)]$$

> [!success]- Solution (with theory)
>
> a) $\lambda = 4$, $k = 2$:
>
> $$P(X=2) = \frac{e^{-4} \cdot 4^2}{2!} = \frac{e^{-4} \cdot 16}{2} = 8e^{-4}$$
> $$\approx 8 \times 0.01832 \approx 0.1465$$
>
> About 14.7% of minutes have exactly 2 calls.
>
> b) $\lambda = 4$:
>
> $$P(X \geq 1) = 1 - P(X=0) = 1 - e^{-4} \approx 1 - 0.01832 = 0.9817$$
>
> About 98.2% of minutes have at least one call. Even though the average is only 4, having zero calls is quite rare.
>
> c) $\lambda = 8$ (2 minutes):
>
> $$P(X=0) = e^{-8} \approx 0.000335$$
> $$P(X=1) = \frac{e^{-8} \cdot 8}{1!} = 8e^{-8} \approx 0.00268$$
> $$P(X=2) = \frac{e^{-8} \cdot 64}{2!} = 32e^{-8} \approx 0.01073$$
>
> $$P(X \geq 3) = 1 - (0.000335 + 0.00268 + 0.01073) = 1 - 0.01374 = 0.98626$$
>
> About 98.6% chance of 3+ calls in 2 minutes. With $\lambda = 8$, getting only 0-2 calls is very unlikely.

---

### Problem E2: Rare Disease

A rare disease affects 0.1% of the population. In a town of 5,000 people:

a) What's the expected number of cases?
b) What's the probability of exactly 5 cases?
c) What's the probability of at least 1 case?

> [!info]- First-principle derivation
>
> **Why Poisson?** $n = 5000$ is large, $p = 0.001$ is small, $np = 5$ is moderate. This is a textbook Poisson approximation of Binomial.
>
> **Why not Binomial directly?** You *could* use Binomial(5000, 0.001), but computing $\binom{5000}{5}$ is computationally intense. Poisson with $\lambda = np = 5$ gives an excellent approximation with much simpler arithmetic.
>
> **Accuracy check:** The Poisson approximation improves as $n$ grows and $p$ shrinks. A common rule of thumb: the approximation is good when $n \geq 20$ and $p \leq 0.05$. Here $n=5000$, $p=0.001$ — well within the range.

> [!success]- Solution (with theory)
>
> a) $E[X] = \lambda = np = 5000 \times 0.001 = 5$ cases expected
>
> b) $\lambda = 5$, $k = 5$:
>
> $$P(X=5) = \frac{e^{-5} \cdot 5^5}{5!} = \frac{e^{-5} \cdot 3125}{120}$$
> $$\approx \frac{0.006738 \times 3125}{120} \approx 0.1755$$
>
> c) $\lambda = 5$:
>
> $$P(X \geq 1) = 1 - P(X=0) = 1 - e^{-5} \approx 1 - 0.006738 = 0.99326$$
>
> **Key insight:** Even though the disease is rare (0.1%), in a town of 5000 there's a 99.3% chance of at least one case. That's the power of large $n$ — rare events become almost certain at scale.

---

### Problem M1: Overlapping Intervals

A website gets an average of 6 visits per minute.

a) What's the probability of exactly 3 visits in 30 seconds?
b) What's the probability of no visits in 10 seconds?
c) What's the probability that the time between two consecutive visits is more than 20 seconds? (Uses Exponential — preview of Session 005)

> [!info]- First-principle derivation
>
> **Adjusting $\lambda$ for different intervals:**
>
> Rate = 6 visits per minute.
>
> - 30 seconds = 0.5 minutes: $\lambda = 6 \times 0.5 = 3$
> - 10 seconds = $1/6$ minute: $\lambda = 6 \times 1/6 = 1$
>
> **Part (c)** connects to the Exponential distribution. If $T$ is the time between visits (in minutes), and visits follow a Poisson process with rate $\lambda = 6$ per minute, then $T \sim \text{Exponential}(6)$.
>
> The probability $T > 20$ seconds requires converting to minutes: 20 seconds = $20/60 = 1/3$ minute.
>
> $$P(T > 1/3) = e^{-6 \times (1/3)} = e^{-2}$$

> [!success]- Solution (with theory)
>
> a) $\lambda = 3$ (30 seconds):
>
> $$P(X=3) = \frac{e^{-3} \cdot 3^3}{3!} = \frac{e^{-3} \cdot 27}{6} = 4.5e^{-3}$$
> $$\approx 4.5 \times 0.04979 \approx 0.2240$$
>
> b) $\lambda = 1$ (10 seconds):
>
> $$P(X=0) = e^{-1} \approx 0.3679$$
>
> About 36.8% of 10-second intervals have zero visits.
>
> c) $\lambda = 6$ per minute, time in minutes:
>
> $$P(T > 20\text{s}) = P(T > 1/3 \text{ min}) = e^{-6 \times 1/3} = e^{-2} \approx 0.1353$$
>
> About 13.5% of inter-visit times exceed 20 seconds.

---

### Problem M2: Poisson Approximation of Binomial

A factory produces items with a 2% defect rate. A batch of 200 items is inspected.

a) What's the exact distribution of the number of defects?
b) Approximate using Poisson. What's $\lambda$?
c) Compare the Poisson and Binomial probabilities for $k = 0, 1, 2, 3$.

> [!info]- First-principle derivation
>
> **Exact distribution:** $X \sim \text{Binomial}(n=200, p=0.02)$
>
> **Poisson approximation:** $\lambda = np = 200 \times 0.02 = 4$
>
> **Comparing the two:**
>
> Binomial: $P(X=k) = \binom{200}{k} (0.02)^k (0.98)^{200-k}$
>
> Poisson: $P(X=k) = \frac{e^{-4} \cdot 4^k}{k!}$
>
> Let's compute and compare:
>
> **For $k=0$:**
> - Binomial: $P(0) = (0.98)^{200} \approx 0.0176$
> - Poisson: $P(0) = e^{-4} \approx 0.0183$
> - Difference: 0.0007 — negligible
>
> **For $k=1$:**
> - Binomial: $P(1) = \binom{200}{1}(0.02)(0.98)^{199} = 200 \times 0.02 \times (0.98)^{199}$
>   $= 4 \times (0.98)^{199} \approx 4 \times 0.0180 \approx 0.0719$
> - Poisson: $P(1) = e^{-4} \cdot 4 \approx 0.0733$
> - Difference: 0.0014 — still very small
>
> **For $k=2$:**
> - Binomial: $P(2) = \binom{200}{2}(0.02)^2(0.98)^{198} = 19900 \times 0.0004 \times (0.98)^{198}$
>   $= 7.96 \times (0.98)^{198} \approx 7.96 \times 0.0183 \approx 0.1458$
> - Poisson: $P(2) = e^{-4} \cdot 16/2 = 8e^{-4} \approx 0.1465$
> - Difference: 0.0007 — excellent
>
> The approximation is already excellent at $n=200$ because $p=0.02$ is small.

> [!success]- Solution (with theory)
>
> a) $X \sim \text{Binomial}(n=200, p=0.02)$
>
> b) $\lambda = np = 200 \times 0.02 = 4$
> $$X \approx \text{Poisson}(\lambda = 4)$$
>
> c) Comparison:
>
> | $k$ | Binomial(200, 0.02) | Poisson(4) | Difference |
> |:---:|:---:|:---:|:---:|
> | 0 | 0.0176 | 0.0183 | 0.0007 |
> | 1 | 0.0719 | 0.0733 | 0.0014 |
> | 2 | 0.1458 | 0.1465 | 0.0007 |
> | 3 | 0.1974 | 0.1954 | 0.0020 |
>
> The Poisson approximation is excellent — errors are less than 0.002 in all cases. This is why Poisson is so useful: it replaces the messy Binomial with a simple formula at negligible accuracy loss.

---

### Problem M3: Sum of Independent Poissons

A bookstore gets:
- Poetry customers: Poisson($\lambda_1 = 2$) per hour
- Fiction customers: Poisson($\lambda_2 = 5$) per hour
- The two types are independent

a) What's the distribution of total customers per hour?
b) What's the probability of exactly 7 total customers in an hour?
c) What's the probability of at least 1 poetry customer in 30 minutes?

> [!info]- First-principle derivation
>
> **Sum of independent Poissons:**
>
> If $X \sim \text{Poisson}(\lambda_1)$ and $Y \sim \text{Poisson}(\lambda_2)$ are independent, then $X+Y \sim \text{Poisson}(\lambda_1 + \lambda_2)$.
>
> **Proof sketch:** The sum of independent Poisson processes is also a Poisson process, with rate equal to the sum of the rates. Intuitively, if two types of events arrive independently at constant rates, the combined arrival process is also a constant-rate process.
>
> $$E[X+Y] = E[X] + E[Y] = \lambda_1 + \lambda_2 = 7$$
> $$\text{Var}(X+Y) = \text{Var}(X) + \text{Var}(Y) = \lambda_1 + \lambda_2 = 7$$
>
> Independence ensures no covariance terms.
>
> **For part (c):** $\lambda$ scales with the interval. Poetry customers arrive at $\lambda_1 = 2$ per hour, so in 30 minutes ($0.5$ hours): $\lambda = 2 \times 0.5 = 1$.
>
> $$P(\text{at least 1 poetry customer in 30 min}) = 1 - P(X=0) = 1 - e^{-1}$$

> [!success]- Solution (with theory)
>
> a) $X + Y \sim \text{Poisson}(\lambda_1 + \lambda_2 = 2 + 5 = 7)$
>
> b) $\lambda = 7$, $k = 7$:
>
> $$P(X+Y = 7) = \frac{e^{-7} \cdot 7^7}{7!} = \frac{e^{-7} \cdot 823543}{5040}$$
> $$\approx \frac{0.000912 \times 823543}{5040} \approx 0.1490$$
>
> c) $\lambda = 1$ (30 minutes for poetry customers):
>
> $$P(\text{at least 1}) = 1 - P(X=0) = 1 - e^{-1} \approx 1 - 0.3679 = 0.6321$$
>
> **Key property tested here:** Sum of independent Poissons is Poisson. This is a frequently tested GATE concept.

---

> Say **"done session-004"** when you've worked through these. Next: Session 006 — The Normal Distribution.

---

## Key Differences: Poisson vs Binomial vs Exponential

| Property | Binomial($n,p$) | Poisson($\lambda$) | Exponential($\lambda$) |
|---|---|---|---|
| **What it models** | Count in $n$ trials | Count in fixed interval | Time between events |
| **Domain** | $0, 1, ..., n$ (finite) | $0, 1, 2, ...$ (infinite) | $t \geq 0$ (continuous) |
| **Parameters** | $n, p$ | $\lambda$ (one number!) | $\lambda$ |
| **Mean** | $np$ | $\lambda$ | $1/\lambda$ |
| **Variance** | $np(1-p)$ | $\lambda$ | $1/\lambda^2$ |
| **Mean vs Variance** | Mean > Var | Mean = Var | Mean ≠ Var |
