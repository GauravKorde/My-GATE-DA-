# Poisson & Exponential — Formula Reference

> Each formula explained: when to use it, and what every piece means.

---

## POISSON

---

### Formula 1: Poisson PMF

$$P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!}$$

**When to use:** You're counting how many times something happens in a fixed window of time or space. You know the average rate $\lambda$, and you want the probability of seeing exactly $k$ events.

**What each piece does:**

| Piece | Role | Intuition |
|---|---|---|
| $P(X = k)$ | The answer | Probability that exactly $k$ events occur |
| $e^{-\lambda}$ | The "zero-event" factor | Probability that zero events happen. Appears in every term because even when you want $k$ events, all other possible events must NOT happen |
| $\lambda^k$ | The "growth" factor | Grows as $k$ grows — pushes probability toward the mean |
| $k!$ | The "brake" factor | Factorial grows faster than any power — stops probability from accumulating at huge $k$ |
| $\lambda$ | The rate | Average number of events per unit time |

---

### Formula 2: Poisson PMF with Time Scaling

$$P(X = k) = \frac{e^{-\lambda t} (\lambda t)^k}{k!}$$

**When to use:** Window isn't 1 unit. If rate is 5/hr and window is 2 hr, use $\lambda t = 10$.

**What changed:** $\lambda$ becomes $\lambda t$ everywhere. $\lambda t$ = expected count for that specific window.

---

### Formula 3: Poisson Mean = $\lambda$

**When to use:** "What's the average number of events?"

**Meaning:** $\lambda$ IS the average. Not an abstract number — the expected count.

---

### Formula 4: Poisson Variance = $\lambda$

**When to use:** "What's the spread?"

**SD:** $\sqrt{\lambda}$. Mean = variance is the fingerprint of Poisson.

---

### Formula 5: Poisson CDF

$$P(X \leq k) = \sum_{i=0}^{k} \frac{e^{-\lambda} \lambda^i}{i!}$$

**When to use:** "At most k events." No closed form — sum the terms.

---

### Formula 6: Sum of Independent Poissons

$$X + Y \sim \text{Poisson}(\lambda_1 + \lambda_2)$$

**When to use:** Two independent Poisson processes combined (students + faculty arrivals).

---

## EXPONENTIAL

---

### Formula 7: Exponential Survival

$$P(T > t) = e^{-\lambda t}$$

**When to use:** "Probability event hasn't happened by time t." This is THE most important Exponential formula.

| Piece | Role | Intuition |
|---|---|---|
| $P(T > t)$ | Survival prob | Probability you're still waiting at time $t$ |
| $e$ | Natural base | From the limit $(1 - \lambda/n)^n \to e^{-\lambda}$ |
| $-\lambda t$ | Decay exponent | $\lambda$ = rate, $t$ = time. Their product = expected events. Negative = decay. |
| $\lambda$ | Rate | Same $\lambda$ as Poisson. Higher rate = shorter waits. |
| $t$ | Wait time | Larger $t$ = smaller survival probability |

---

### Formula 8: Exponential CDF

$$F(t) = 1 - e^{-\lambda t}$$

**When to use:** "Probability event happens within t time units."

**Derivation:** Complement of survival. Either it happened or it hasn't.

---

### Formula 9: Exponential PDF

$$f(t) = \lambda e^{-\lambda t}$$

**When to use:** Need density at a specific $t$ (for integration or likelihood).

**Derivation:** Derivative of CDF.

---

### Formula 10: Mean = $1/\lambda$

**When to use:** "Average waiting time."

**Meaning:** Reciprocal of rate. $\lambda$ events per time → $1/\lambda$ time per event.

---

### Formula 11: Variance = $1/\lambda^2$, SD = $1/\lambda$

**When to use:** "What's the spread?"

**Meaning:** SD = Mean. Unique to Exponential. Huge variability.

---

### Formula 12: Median = $\ln(2)/\lambda \approx 0.693/\lambda$

**When to use:** "Time by which half of events occur."

**Derivation:** Set $F(m) = 0.5$, solve $1 - e^{-\lambda m} = 0.5$.

---

### Formula 13: Memoryless Property

$$P(T > s + t \mid T > s) = P(T > t)$$

**When to use:** "Already waited $s$ minutes, what's probability of waiting $t$ more?"

**Meaning:** Past doesn't matter. Fresh start every moment.

**Proof:** $P(T > s+t)/P(T > s) = e^{-\lambda(s+t)}/e^{-\lambda s} = e^{-\lambda t}$

---

### Formula 14: Min of Exponentials

$$\min(T_1, ..., T_n) \sim \text{Exp}(\lambda_1 + ... + \lambda_n)$$

**When to use:** First of several independent events. Which bus comes first?

**Why:** $P(\min > t) = \prod P(T_i > t) = \prod e^{-\lambda_i t} = e^{-(\sum \lambda_i)t}$

---

### Formula 15: Competing Risks

$$P(T_1 < T_2) = \frac{\lambda_1}{\lambda_1 + \lambda_2}$$

**When to use:** Probability that event 1 happens before event 2.

**Intuition:** Proportionate to rates. Rate 2 vs rate 6 → $2/(2+6) = 1/4$ chance.

---

### Formula 16: Sum of Exponentials → Gamma

$$S_n = T_1 + ... + T_n \sim \text{Gamma}(n, \lambda)$$

$$E[S_n] = n/\lambda, \quad \text{Var}(S_n) = n/\lambda^2$$

$$P(S_n > t) = \sum_{k=0}^{n-1} \frac{e^{-\lambda t} (\lambda t)^k}{k!}$$

**When to use:** Waiting for the $n$th event. Total processing time for $n$ items.

**Poisson-Gamma connection:** Probability $n$th event takes $> t$ = probability fewer than $n$ events by time $t$.

---

## THE BRIDGE

### Formula 17: Poisson ↔ Exponential

$$P(T > t) = P(N(t) = 0) = e^{-\lambda t}$$

**When to use:** Switching between "how many" and "how long."

**Meaning:** Waiting time exceeds $t$ exactly when zero events by time $t$. Same event, two languages.

---

## QUICK COMPARISON

| Property | Poisson($\lambda$) | Exponential($\lambda$) |
|---|---|---|
| Answers | "How many events?" | "How long to wait?" |
| Type | Discrete (counts) | Continuous (time) |
| Core formula | $P(X=k) = e^{-\lambda}\lambda^k/k!$ | $P(T > t) = e^{-\lambda t}$ |
| Mean | $\lambda$ | $1/\lambda$ |
| Variance | $\lambda$ | $1/\lambda^2$ |
| SD | $\sqrt{\lambda}$ | $1/\lambda$ |
| Mean vs SD | SD = $\sqrt{\text{mean}}$ | SD = mean |
| Memory | Independent increments | Memoryless |
| Sum of two | Poisson($\lambda_1 + \lambda_2$) | Gamma (not Exponential) |
| Min of two | — | Exp($\lambda_1 + \lambda_2$) |
