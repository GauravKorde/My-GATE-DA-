# Formula Sheet — Session 004 (Poisson) & 005 (Exponential)

---

## POISSON DISTRIBUTION

### The Formula

$$P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!}$$

This gives the probability of seeing exactly $k$ events in a fixed window, when events happen at rate $\lambda$. The window is unit time (1 hour, 1 minute, etc.).

If the window is $t$ units instead of 1:

$$P(X = k) = \frac{e^{-\lambda t} (\lambda t)^k}{k!}$$

### Mean & Variance

$$E[X] = \lambda, \quad \text{Var}(X) = \lambda$$

Mean equals variance. That's the fingerprint of Poisson. If mean = 9, then SD = 3. The CV = $1/\sqrt{\lambda}$ shrinks as $\lambda$ grows — Poisson becomes more predictable and starts looking Normal.

### Where It Comes From

Poisson is the limit of Binomial when $n \to \infty$, $p \to 0$, and $np = \lambda$ stays fixed.

The limit works in three steps:
1. $\binom{n}{k} \to \frac{n^k}{k!}$ (for large $n$, the choose formula simplifies)
2. $p^k = (\lambda/n)^k$ (substitute $p = \lambda/n$)
3. $(1 - \lambda/n)^n \to e^{-\lambda}$ (the famous exponential limit)

Multiply all three: $\frac{n^k}{k!} \times \frac{\lambda^k}{n^k} \times e^{-\lambda} = \frac{e^{-\lambda} \lambda^k}{k!}$

### The Poisson Process

Three rules define it:
1. **One at a time** — no simultaneous events
2. **Independent** — past doesn't affect future
3. **Constant rate** — $\lambda$ doesn't change

These three rules force the count in any interval to be Poisson. Nothing else works.

### When to Use Poisson

- Counting events in a fixed time/space window
- Events are rare (relative to opportunity)
- Events happen independently at constant average rate
- Examples: website visits per hour, calls per minute, mutations per DNA segment, photons hitting a detector per second

---

## EXPONENTIAL DISTRIBUTION

### The Formulas

**PDF (density at time $t$):**
$$f(t) = \lambda e^{-\lambda t}, \quad t \geq 0$$

**CDF (probability event has happened by time $t$):**
$$F(t) = P(T \leq t) = 1 - e^{-\lambda t}$$

**Survival (probability still waiting at time $t$):**
$$S(t) = P(T > t) = e^{-\lambda t}$$

### Mean & Variance

$$E[T] = \frac{1}{\lambda}, \quad \text{Var}(T) = \frac{1}{\lambda^2}, \quad \sigma_T = \frac{1}{\lambda}$$

Mean = SD. CV = 1. The spread is 100% of the average. This means Exponential is wildly unpredictable — if the average wait is 5 minutes, a 10-minute wait happens 14% of the time, and a 15-minute wait happens 5% of the time.

### Where It Comes From

The time $T$ until the next event is more than $t$ when **zero events** happened in $[0, t]$.

$$P(T > t) = P(\text{0 events}) = e^{-\lambda t}$$

That's Poisson with $k = 0$. Then:
- The CDF is the complement: $F(t) = 1 - e^{-\lambda t}$
- The PDF is the derivative: $f(t) = \lambda e^{-\lambda t}$

### The Memoryless Property

$$P(T > s + t \mid T > s) = P(T > t)$$

The bus doesn't care how long you've waited. The probability of waiting another $t$ minutes, given you've already waited $s$ minutes, is the same as the probability of waiting $t$ minutes from the start.

Proof: $\frac{P(T > s + t)}{P(T > s)} = \frac{e^{-\lambda(s+t)}}{e^{-\lambda s}} = e^{-\lambda t} = P(T > t)$

Only the Exponential (and its discrete cousin Geometric) has this property.

### Minimum of Exponentials

If you have $n$ independent Exponential clocks with rates $\lambda_1, \lambda_2, ..., \lambda_n$, the time until the **first** one rings is:

$$\min(X_1, X_2, ..., X_n) \sim \text{Exponential}(\lambda_1 + \lambda_2 + ... + \lambda_n)$$

Why: $P(\min > t) = P(X_1 > t) \times ... \times P(X_n > t) = e^{-\lambda_1 t} \times ... \times e^{-\lambda_n t} = e^{-(\lambda_1 + ... + \lambda_n)t}$

Rates add. More clocks = faster first ring.

### Sum of Exponentials → Gamma

If you wait for $n$ events to happen, the total time is:

$$T_1 + T_2 + ... + T_n \sim \text{Gamma}(n, \lambda)$$

Mean = $\frac{n}{\lambda}$, Variance = $\frac{n}{\lambda^2}$

The Poisson-Gamma connection: $P(S_n > t) = \sum_{k=0}^{n-1} \frac{e^{-\lambda t} (\lambda t)^k}{k!}$

This says: "the probability that the $n$th event takes more than $t$ time equals the probability that fewer than $n$ events have occurred by time $t$."

### When to Use Exponential

- "How long until the next event?"
- Modeling waiting times, service times, lifetimes
- Situations with constant failure rate (no aging, no wear)
- Examples: time until next customer arrives, battery lifetime in random failure phase, time between radioactive decays

---

## THE BRIDGE — Poisson & Exponential Together

Poisson and Exponential describe the **same process** from different angles.

| | Poisson | Exponential |
|---|---|---|
| **Perspective** | Count events in a window | Measure time between events |
| **Type** | Discrete | Continuous |
| **Question** | "How many?" | "How long?" |
| **Parameter** | $\lambda t$ (rate × window) | $\lambda$ (rate) |
| **Mean** | $\lambda t$ | $1/\lambda$ |
| **Variance** | $\lambda t$ | $1/\lambda^2$ |
| **CV** | $1/\sqrt{\lambda t}$ | $1$ (always) |
| **Memory** | Independent increments | Memoryless |

If events occur at rate $\lambda$ per unit time:
- The **count** in $[0, t]$ is Poisson($\lambda t$)
- The **gap** between events is Exponential($\lambda$)

Same $\lambda$. Same process. Two questions.
