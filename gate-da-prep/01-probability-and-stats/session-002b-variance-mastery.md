# Session 002b — Variance & Covariance Mastery

> **📅 Expected:** Jun 18 – Jun 20 | **Buffer:** +13 days 🟢 | **Status:** 📄 Doc ready (written ahead of schedule)
>
> **Target:** Build rock-solid intuition for variance, conditional variance, Law of Total Variance, covariance, and correlation — through **30+ problems** of progressive difficulty, each with full step-by-step derivation.
>
> **Prerequisite:** Session 002 (conditional probability, expectation, variance definitions)

---

## Quick Formula Reference

| Concept | Formula |
|---------|---------|
| Variance (definition) | $\text{Var}(X) = E[(X - \mu)^2]$ |
| Variance (shortcut) | $\text{Var}(X) = E[X^2] - (E[X])^2$ |
| Variance of linear combo | $\text{Var}(aX + b) = a^2\text{Var}(X)$ |
| Conditional Variance | $\text{Var}(X \mid B) = E[X^2 \mid B] - (E[X \mid B])^2$ |
| Law of Total Variance | $\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$ |
| Covariance (definition) | $\text{Cov}(X,Y) = E[(X - \mu_X)(Y - \mu_Y)]$ |
| Covariance (shortcut) | $\text{Cov}(X,Y) = E[XY] - E[X]E[Y]$ |
| Covariance bilinearity | $\text{Cov}(aX + bY, cZ + dW) = a c\,\text{Cov}(X,Z) + a d\,\text{Cov}(X,W) + b c\,\text{Cov}(Y,Z) + b d\,\text{Cov}(Y,W)$ |
| Variance of sum | $\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y)$ |
| Correlation | $\rho_{XY} = \dfrac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y}$ |

---

## Part 1 — Variance: Shortcut Formula

---

#### Problem V1: Variance from a Simple PMF

X has PMF:

| x | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| P(X=x) | 0.2 | 0.3 | 0.3 | 0.1 | 0.1 |

Find $\text{Var}(X)$ using the shortcut formula.

> [!success]- Solution (with theory)
>
> **Concept — Why the shortcut formula?**
>
> Variance measures **average squared distance from the mean**. The definition is:
> $$\text{Var}(X) = E[(X - \mu)^2]$$
> Expanding $(X - \mu)^2 = X^2 - 2\mu X + \mu^2$ and taking expectation gives:
> $$\text{Var}(X) = E[X^2] - 2\mu E[X] + \mu^2 = E[X^2] - 2\mu^2 + \mu^2 = E[X^2] - \mu^2$$
> So $\text{Var}(X) = E[X^2] - (E[X])^2$ — the "shortcut" isn't a separate formula, it's just algebra.
>
> **Intuition:** $E[X^2]$ is the average of squares. $(E[X])^2$ is the square of the average. Their difference tells you how spread out the distribution is.
>
> ---
>
> **Step 1 — Find $E[X]$ (the center):**
> $$E[X] = 1(0.2) + 2(0.3) + 3(0.3) + 4(0.1) + 5(0.1)$$
> $$= 0.2 + 0.6 + 0.9 + 0.4 + 0.5 = 2.6$$
>
> The distribution is centered at 2.6 — slightly above the midpoint because probabilities are heavier on the right.
>
> **Step 2 — Find $E[X^2]$ (average of squares):**
> $$E[X^2] = 1^2(0.2) + 2^2(0.3) + 3^2(0.3) + 4^2(0.1) + 5^2(0.1)$$
> $$= 0.2 + 1.2 + 2.7 + 1.6 + 2.5 = 8.2$$
>
> Note: $E[X^2] \neq (E[X])^2$ — that would be $6.76$. The difference IS the variance.
>
> **Step 3 — Apply shortcut:**
> $$\text{Var}(X) = 8.2 - (2.6)^2 = 8.2 - 6.76 = 1.44$$
> $$\sigma_X = \sqrt{1.44} = 1.2$$
>
> **Interpretation:** On average, X is about 1.2 units away from its mean of 2.6. The standard deviation (1.2) is easier to interpret than variance (1.44) because it's in the same units as X.

---

#### Problem V2: Variance of a Transformed Variable

If $E[X] = 10$, $\text{Var}(X) = 16$, find:

a) $E[Y]$ and $\text{Var}(Y)$ where $Y = 3X - 2$
b) $E[Z]$ and $\text{Var}(Z)$ where $Z = -X + 5$

> [!success]- Solution (with theory)
>
> **Concept — How does variance behave under transformations?**
>
> Two key rules:
> 1. **Adding a constant shifts the center but not the spread:** $\text{Var}(X + c) = \text{Var}(X)$ because variance measures deviation from the mean, and both X and X+c shift by the same amount.
> 2. **Multiplying by a constant scales the spread:** $\text{Var}(aX) = a^2\text{Var}(X)$. Why $a^2$? Because variance is in squared units. If X is in meters, $\text{Var}(X)$ is in meters². Multiplying X by 3 makes the spread 3× larger, so variance becomes 9× larger.
>
> Combined: $\text{Var}(aX + b) = a^2\text{Var}(X)$ — the $b$ disappears.
>
> ---
>
> a) $Y = 3X - 2$
> $E[Y] = E[3X - 2] = 3E[X] - 2$ (linearity of expectation)
> $= 3(10) - 2 = 28$
>
> $\text{Var}(Y) = \text{Var}(3X - 2) = 3^2\text{Var}(X)$ (the $-2$ doesn't matter)
> $= 9(16) = 144$
>
> b) $Z = -X + 5$
> $E[Z] = -E[X] + 5 = -10 + 5 = -5$
>
> $\text{Var}(Z) = \text{Var}(-X + 5) = (-1)^2\text{Var}(X) = 16$
>
> **Key insight:** The sign of the coefficient doesn't matter for variance — flipping X upside down doesn't change how spread out it is. Only the magnitude matters.

---

#### Problem V3: Variance Coding Challenge

A random variable X takes values $x_1, x_2, ..., x_n$ with equal probability $1/n$.

a) Show that $E[X^2] = \frac{1}{n}\sum_{i=1}^n x_i^2$
b) If $X = \{2, 4, 6, 8, 10\}$ with equal probability, find $\text{Var}(X)$
c) What happens to $\text{Var}(X)$ if you multiply every value by 3?

> [!success]- Solution (with theory)
>
> **Concept — Equally likely outcomes and the mean formula:**
> When all $n$ outcomes are equally likely, the probability of each is $1/n$.
> The mean is just the arithmetic average: $E[X] = \frac{1}{n}\sum_{i=1}^n x_i$.
> Similarly $E[X^2] = \frac{1}{n}\sum_{i=1}^n x_i^2$ — average of the squares.
>
> **Why this matters:** For equally likely outcomes, all probability calculations reduce to simple averages. This is the simplest case to build intuition.
>
> ---
>
> a) For equally likely outcomes: $E[X^2] = \frac{1}{n}\sum_{i=1}^n x_i^2$ (definition — replace probability $P(X=x_i) = 1/n$ in the formula $E[X^2] = \sum x_i^2 P(X=x_i)$)
>
> b) $X = \{2, 4, 6, 8, 10\}$, $n=5$, equally likely:
> $$\bar{x} = \frac{2+4+6+8+10}{5} = \frac{30}{5} = 6$$
> $$E[X^2] = \frac{4+16+36+64+100}{5} = \frac{220}{5} = 44$$
> $$\text{Var}(X) = 44 - 6^2 = 44 - 36 = 8$$
>
> **Interpretation:** The values range from 2 to 10 (range = 8), and $\sigma = \sqrt{8} \approx 2.83$, which is roughly 1/3 of the range — reasonable for a symmetric spread.
>
> c) If $Y = 3X$, then by the scaling rule: $\text{Var}(Y) = 9\cdot\text{Var}(X) = 72$
>
> **Direct check:** $Y = \{6, 12, 18, 24, 30\}$, $\bar{y}=18$
> $$E[Y^2] = \frac{36+144+324+576+900}{5} = \frac{1980}{5} = 396$$
> $$\text{Var}(Y) = 396 - 18^2 = 396 - 324 = 72$$ ✅
>
> Verifies that the scaling rule $\text{Var}(aX) = a^2\text{Var}(X)$ always holds.

---

#### Problem V4: Variance from Raw Moments

A random variable has moments: $E[X] = 4$, $E[X^2] = 25$, $E[X^3] = 100$, $E[X^4] = 625$.

a) Find $\text{Var}(X)$
b) Find $\text{Var}(X^2)$
c) Find $\text{Cov}(X, X^2)$

> [!success]- Solution (with theory)
>
> **Concept — Moments completely describe a distribution.**
>
> The $k$-th moment $E[X^k]$ encodes information about shape:
> - $E[X]$ = center (1st moment)
> - $E[X^2]$ gives variance when combined with $E[X]$
> - Higher moments ($E[X^3]$, $E[X^4]$) give skewness and kurtosis
>
> **Important:** The shortcut formula only needs the first two moments — you don't need the full distribution to find variance.
>
> ---
>
> a) $\text{Var}(X) = E[X^2] - (E[X])^2 = 25 - 16 = 9$
> So $\sigma_X = 3$.
>
> b) $\text{Var}(X^2) = E[X^4] - (E[X^2])^2 = 625 - 25^2 = 625 - 625 = 0$
>
> **Diagnostic:** Zero variance means $X^2$ is a constant! If $X^2$ is constant, then $X$ can only be $\pm 2$. And indeed $E[X]=4$ combined with $\text{Var}(X)=9$ means $\sigma_X = 3$, so $X$ is always 4 ± 3, i.e., either 1 or 7... Wait, that doesn't match $X^2$ being constant.
>
> Let me recheck: If $X^2 = c$ (constant), then $X$ takes values $\pm\sqrt{c}$. But $E[X] = 4$ — if $X$ is symmetric around 0, $E[X]$ would be 0. Contradiction? No — $X$ could be +2 always (then $E[X]=2$, not 4) or -2 always (then $E[X]=-2$).
>
> Actually, the numbers tell us: $E[X^2]=25$ means $X$ is always $\pm 5$, but $E[X]=4$ means it's mostly positive 5 with a small chance of -5. And indeed $\text{Var}(X)=9$ confirms the spread. So $X^2=25$ always. The $E[X^4]=625$ confirms $X^4=(X^2)^2 = 25^2 = 625$.
>
> c) $\text{Cov}(X, X^2) = E[X^3] - E[X]E[X^2] = 100 - 4(25) = 100 - 100 = 0$
>
> Interesting — $X$ and $X^2$ have zero covariance even though they're obviously dependent (quadratic relationship). This is the classic example of **covariance only capturing linear relationships**.

---

#### Problem V5: Variance — Coin Toss Game

You toss a fair coin. If heads, you win \$3. If tails, you lose \$1. Let X = your winnings.

a) Find $E[X]$ and $\text{Var}(X)$
b) If you play 3 independent rounds, let $Y = X_1 + X_2 + X_3$ be total winnings. Find $E[Y]$ and $\text{Var}(Y)$
c) If instead each round costs \$0.50 to play (so net = X - 0.50 per round), find $E[\text{net}]$ and $\text{Var}(\text{net})$ for 3 rounds

> [!success]- Solution (with theory)
>
> **Concept — Independent vs dependent sums:**
>
> When you add independent random variables:
> - $E[X_1 + X_2 + X_3] = E[X_1] + E[X_2] + E[X_3]$ (always true, even without independence)
> - $\text{Var}(X_1 + X_2 + X_3) = \text{Var}(X_1) + \text{Var}(X_2) + \text{Var}(X_3)$ (only true if independent! If dependent, you'd also have covariance terms)
>
> This is why diversification works in finance — adding independent assets doesn't change the total mean (just averages them), but the total variance grows slower than the individual variances would suggest.
>
> ---
>
> a) **Single round:**
> $P(X=3) = 0.5$, $P(X=-1) = 0.5$
> $E[X] = 3(0.5) + (-1)(0.5) = 1.5 - 0.5 = \$1$
> $E[X^2] = 9(0.5) + 1(0.5) = 4.5 + 0.5 = 5$
> $\text{Var}(X) = 5 - 1^2 = \$4$
> $\sigma_X = \$2$
>
> **Interpretation:** Expected profit per round is \$1, but the standard deviation is \$2 — meaning in any single round, you could easily lose money (\$1 ± \$2 covers -1 to +3).
>
> b) **3 independent rounds:**
> $Y = X_1 + X_2 + X_3$
> $E[Y] = 3E[X] = \$3$
>
> Since rounds are **independent**: $\text{Var}(Y) = 3\text{Var}(X) = 3(4) = \$12$
> $\sigma_Y = \sqrt{12} \approx \$3.46$
>
> **Key observation:** The mean triples (1→3) but $\sigma$ only grows by $\sqrt{3}$ (2→3.46). The ratio $\sigma/\mu$ shrinks — this is the "law of large numbers" in action.
>
> c) **With entry fee:**
> Net per round: $W = X - 0.50$
> $E[W] = \$1 - 0.50 = \$0.50$
> $\text{Var}(W) = \text{Var}(X) = 4$ (shift doesn't change spread)
>
> For 3 rounds: $E[Y_{\text{net}}] = 3(\$0.50) = \$1.50$, $\text{Var}(Y_{\text{net}}) = 3(4) = \$12$
>
> **Bottom line:** The fee cuts expected profit in half but doesn't reduce risk at all.

---

#### Problem V6: Variance of a Function

Let $X \sim \text{Uniform}\{1, 2, ..., 10\}$ (equally likely integers 1-10).

a) Find $E[X]$, $E[X^2]$, $\text{Var}(X)$
b) Find $E[\sqrt{X}]$ — does $\text{Var}(\sqrt{X}) = \sqrt{\text{Var}(X)}$? Check by direct computation.

> [!success]- Solution (with theory)
>
> **Concept — Variance does NOT commute with non-linear functions.**
>
> This is a common GATE trap. Students often think $\text{Var}(f(X)) = f(\text{Var}(X))$ — but this is **completely false**.
>
> ✅ $\text{Var}(aX + b) = a^2\text{Var}(X)$ works because $aX + b$ is **linear**.
> ❌ $\text{Var}(\sqrt{X}) \neq \sqrt{\text{Var}(X)}$ because $\sqrt{X}$ is **non-linear**.
>
> For non-linear functions, you MUST:
> 1. Find the distribution of $f(X)$ (or at least its moments)
> 2. Compute $E[f(X)]$ and $E[(f(X))^2]$ directly
> 3. Then apply the shortcut formula
>
> ---
>
> a) $X \sim \text{Uniform}\{1, 2, ..., 10\}$, equally likely:
>
> $E[X] = \frac{1+2+...+10}{10} = \frac{55}{10} = 5.5$
>
> $E[X^2] = \frac{1^2+2^2+...+10^2}{10} = \frac{385}{10} = 38.5$
>
> $\text{Var}(X) = 38.5 - (5.5)^2 = 38.5 - 30.25 = 8.25$
> $\sigma_X \approx 2.872$
>
> b) **Direct computation for $\sqrt{X}$:**
>
> $E[\sqrt{X}] = \frac{\sqrt{1}+\sqrt{2}+...+\sqrt{10}}{10}$
> $\approx \frac{1 + 1.414 + 1.732 + 2 + 2.236 + 2.449 + 2.646 + 2.828 + 3 + 3.162}{10}$
> $= \frac{22.467}{10} \approx 2.247$
>
> $E[(\sqrt{X})^2] = E[X] = 5.5$ (because $(\sqrt{X})^2 = X$)
>
> $\text{Var}(\sqrt{X}) = 5.5 - (2.247)^2 = 5.5 - 5.047 = 0.453$
>
> **Now compare:** $\sqrt{\text{Var}(X)} = \sqrt{8.25} \approx 2.872$
>
> Clearly $0.453 \neq 2.872$. The "intuitive" guess is off by a factor of 6!
>
> **Moral:** Never assume variance passes through non-linear functions. Always compute from scratch.

---

## Part 2 — Conditional Variance

---

#### Problem CV1: Conditional Variance from Table

| X\Y | 0 | 1 |
|---|---|---|
| 0 | 0.2 | 0.3 |
| 1 | 0.1 | 0.4 |

Find $\text{Var}(X \mid Y=0)$ and $\text{Var}(X \mid Y=1)$.

> [!success]- Solution (with theory)
>
> **Concept — Conditional variance = variance within a subgroup.**
>
> When we condition on $Y = y$, we're restricting to a specific row of the table. The unconditional variance measures spread of X across all Y values. Conditional variance measures spread within just that one group.
>
> The formula is exactly the same as regular variance, just using conditional probabilities:
> $$\text{Var}(X \mid Y=y) = E[X^2 \mid Y=y] - (E[X \mid Y=y])^2$$
>
> This is NOT a new formula — it's the old formula applied to a subset of the data.
>
> ---
>
> **Step 1 — Find the marginal probabilities of $Y$:**
> $P(Y=0) = 0.2 + 0.1 = 0.3$ (first column)
> $P(Y=1) = 0.3 + 0.4 = 0.7$ (second column)
>
> **Step 2 — Conditional distribution of $X$ given $Y=0$:**
> We restrict to the first column. Total weight in this column is 0.3.
> $P(X=0 \mid Y=0) = 0.2/0.3 = 2/3$
> $P(X=1 \mid Y=0) = 0.1/0.3 = 1/3$
>
> **Var(X | Y=0):**
> $E[X \mid Y=0] = 0(2/3) + 1(1/3) = 1/3$
> $E[X^2 \mid Y=0] = 0^2(2/3) + 1^2(1/3) = 1/3$
> $\text{Var}(X \mid Y=0) = 1/3 - (1/3)^2 = 1/3 - 1/9 = 2/9$
>
> **Step 3 — Conditional distribution of $X$ given $Y=1$:**
> Restrict to second column. Total = 0.7.
> $P(X=0 \mid Y=1) = 0.3/0.7 = 3/7$
> $P(X=1 \mid Y=1) = 0.4/0.7 = 4/7$
>
> **Var(X | Y=1):**
> $E[X \mid Y=1] = 0(3/7) + 1(4/7) = 4/7$
> $E[X^2 \mid Y=1] = 0^2(3/7) + 1^2(4/7) = 4/7$
> $\text{Var}(X \mid Y=1) = 4/7 - (4/7)^2 = 4/7 - 16/49 = 28/49 - 16/49 = 12/49$
>
> **Interpretation:** Both conditional variances are positive, meaning X varies even within each Y group. But $\text{Var}(X \mid Y=0) = 2/9 \approx 0.222$ while $\text{Var}(X \mid Y=1) = 12/49 \approx 0.245$ — slightly more spread when Y=1.

---

#### Problem CV2: Conditional Variance — Dice

Roll a fair die. Let X = the outcome. Let Y = 1 if X is even, Y = 0 if X is odd.

Find $\text{Var}(X \mid Y=1)$ and $\text{Var}(X \mid Y=0)$.

> [!success]- Solution (with theory)
>
> **Concept — Symmetry in conditional distributions:**
>
> A fair die has a symmetric distribution about 3.5. When you split by parity, you get two groups of three numbers each. The conditional distributions within each group are also uniform (each element equally likely within its group).
>
> **Key insight:** Even though the centers differ ($E[X \mid \text{even}] = 4$, $E[X \mid \text{odd}] = 3$), the spreads might be the same — or different. Let's check.
>
> ---
>
> **Y=1 (even):** $X \in \{2, 4, 6\}$, each with conditional prob $1/3$
> $E[X \mid Y=1] = (2+4+6)/3 = 12/3 = 4$
> $E[X^2 \mid Y=1] = (4+16+36)/3 = 56/3$
> $\text{Var}(X \mid Y=1) = 56/3 - 4^2 = 56/3 - 48/3 = 8/3 \approx 2.667$
>
> **Y=0 (odd):** $X \in \{1, 3, 5\}$, each with conditional prob $1/3$
> $E[X \mid Y=0] = (1+3+5)/3 = 9/3 = 3$
> $E[X^2 \mid Y=0] = (1+9+25)/3 = 35/3$
> $\text{Var}(X \mid Y=0) = 35/3 - 3^2 = 35/3 - 27/3 = 8/3 \approx 2.667$
>
> **Interesting result:** Both conditional variances equal $8/3$.
>
> **Why?** The even set {2,4,6} and odd set {1,3,5} are just shifted by 1. A shift doesn't change variance. The spacing is the same (every other number), so the spread is identical.
>
> **Compare with unconditional:**
> $E[X] = 3.5$, $E[X^2] = (1+4+9+16+25+36)/6 = 91/6$
> $\text{Var}(X) = 91/6 - (3.5)^2 = 91/6 - 12.25 = 91/6 - 73.5/6 = 17.5/6 \approx 2.917$
>
> The unconditional variance (2.917) is slightly larger than each conditional variance (2.667). Why? Because the difference between group means (3 vs 4) adds extra variability. This is exactly the Law of Total Variance in action: total = within + between.

---

#### Problem CV3: Conditional Variance from Given Info

A call center's call duration T depends on call type:
- Simple calls (60%): $E[T \mid S] = 2$, $\text{Var}(T \mid S) = 1$
- Complex calls (40%): $E[T \mid C] = 8$, $\text{Var}(T \mid C) = 4$

What is $\text{Var}(T)$? (Use Law of Total Variance)

> [!success]- Solution (with full theory)
>
> **Concept 1 — Why does variance have two components?**
>
> When data comes from different groups (here: call types), total variability comes from two sources:
> - **Within-group variability:** Even within simple calls, durations vary. That's $\text{Var}(T \mid S) = 1$.
> - **Between-group variability:** Simple calls average 2 min, complex average 8 min. The gap between groups adds variability.
>
> The Law of Total Variance formalizes this:
> $$\text{Var}(T) = \underbrace{E[\text{Var}(T \mid \text{type})]}_{\text{average within-group}} + \underbrace{\text{Var}(E[T \mid \text{type}])}_{\text{between-group}}$$
>
> **Concept 2 — It's like ANOVA:**
> If you've studied ANOVA, this is exactly the same decomposition:
> - $SS_{\text{total}} = SS_{\text{within}} + SS_{\text{between}}$
> - LTV is the same idea in expectation terms.
>
> ---
>
> **Step 1 — Compute the within-group term ($E[\text{Var}(T \mid \text{type})]$)**
>
> This is just a weighted average of the conditional variances:
> $$E[\text{Var}(T \mid \text{type})] = \text{Var}(T \mid S) \cdot P(S) + \text{Var}(T \mid C) \cdot P(C)$$
> $$= 1(0.6) + 4(0.4) = 0.6 + 1.6 = 2.2$$
>
> **Interpretation:** Even within the same call type, durations vary by 2.2 on average. This is the "unavoidable" randomness.
>
> **Step 2 — Compute $E[T]$ (needed for the between-group term)**
>
> By Law of Total Expectation: $E[T] = E[E[T \mid \text{type}]]$
> $$E[T] = E[T \mid S] \cdot P(S) + E[T \mid C] \cdot P(C)$$
> $$= 2(0.6) + 8(0.4) = 1.2 + 3.2 = 4.4 \text{ min}$$
>
> **Step 3 — Compute the between-group term ($\text{Var}(E[T \mid \text{type}])$)**
>
> $E[T \mid \text{type}]$ is itself a random variable — it takes value 2 with prob 0.6, and 8 with prob 0.4. It measures "what the group averages look like."
>
> Its variance tells us how much the groups differ from each other:
> $$\text{Var}(E[T \mid \text{type}]) = E[(E[T \mid \text{type}])^2] - (E[E[T \mid \text{type}]])^2$$
>
> First compute $E[(E[T \mid \text{type}])^2]$:
> $$= 2^2(0.6) + 8^2(0.4) = 4(0.6) + 64(0.4) = 2.4 + 25.6 = 28$$
>
> We already know $E[E[T \mid \text{type}]] = E[T] = 4.4$, so:
> $$\text{Var}(E[T \mid \text{type}]) = 28 - (4.4)^2 = 28 - 19.36 = 8.64$$
>
> **Interpretation:** The group means differ substantially (2 vs 8), contributing 8.64 to total variance.
>
> **Step 4 — Add them up:**
> $$\text{Var}(T) = 2.2 + 8.64 = 10.84 \text{ min}^2$$
>
> **Final insight:** Which component is bigger?
> - Within: $2.2/10.84 \approx 20.3\%$
> - Between: $8.64/10.84 \approx 79.7\%$
>
> **~80% of call duration variability comes from the type difference, not random fluctuations within a type.** This means: if you want to predict call duration, knowing the call type is far more valuable than knowing anything else.

---

#### Problem CV4: Conditional Variance — 3×3 Table

| X\Y | 1 | 2 | 3 |
|---|---|---|---|
| 1 | 0.1 | 0.05 | 0.05 |
| 2 | 0.1 | 0.2 | 0.1 |
| 3 | 0.05 | 0.05 | 0.3 |

Find $\text{Var}(X \mid Y=2)$ and $\text{Var}(X \mid Y=3)$.

> [!success]- Solution (with theory)
>
> **Concept — Conditional variance from a joint table:**
>
> To find $\text{Var}(X \mid Y=y)$, you:
> 1. Take the column where $Y=y$
> 2. Renormalize the probabilities so they sum to 1 (divide each cell by the column total)
> 3. This gives you the conditional distribution $P(X = x \mid Y = y)$
> 4. Apply the variance shortcut formula using these conditional probabilities
>
> ---
>
> **Step 1 — Column totals (marginals of Y):**
> $P(Y=1) = 0.1 + 0.1 + 0.05 = 0.25$
> $P(Y=2) = 0.05 + 0.2 + 0.05 = 0.30$
> $P(Y=3) = 0.05 + 0.1 + 0.3 = 0.45$
>
> **Step 2 — $\text{Var}(X \mid Y=2)$:**
>
> *Conditional distribution (column Y=2, total = 0.30):*
> $P(X=1 \mid Y=2) = 0.05/0.30 = 1/6$
> $P(X=2 \mid Y=2) = 0.2/0.30 = 2/3$
> $P(X=3 \mid Y=2) = 0.05/0.30 = 1/6$
>
> *Notice the symmetry: 1/6, 2/3, 1/6 — this is a symmetric distribution centered at 2.*
>
> $E[X \mid Y=2] = 1(1/6) + 2(4/6) + 3(1/6) = (1+8+3)/6 = 12/6 = 2$
> $E[X^2 \mid Y=2] = 1(1/6) + 4(4/6) + 9(1/6) = (1+16+9)/6 = 26/6 = 13/3$
> $\text{Var}(X \mid Y=2) = 13/3 - 2^2 = 13/3 - 12/3 = 1/3$
>
> **Step 3 — $\text{Var}(X \mid Y=3)$:**
>
> *Conditional distribution (column Y=3, total = 0.45):*
> $P(X=1 \mid Y=3) = 0.05/0.45 = 1/9$
> $P(X=2 \mid Y=3) = 0.1/0.45 = 2/9$
> $P(X=3 \mid Y=3) = 0.3/0.45 = 2/3$
>
> *This is skewed right — most mass is at X=3.*
>
> $E[X \mid Y=3] = 1(1/9) + 2(2/9) + 3(6/9) = (1+4+18)/9 = 23/9 \approx 2.556$
> $E[X^2 \mid Y=3] = 1(1/9) + 4(2/9) + 9(6/9) = (1+8+54)/9 = 63/9 = 7$
> $\text{Var}(X \mid Y=3) = 7 - (23/9)^2 = 7 - 529/81 = 567/81 - 529/81 = 38/81 \approx 0.469$
>
> **Comparison:** $\text{Var}(X \mid Y=2) \approx 0.333$, $\text{Var}(X \mid Y=3) \approx 0.469$, $\text{Var}(X \mid Y=1) \approx 0.249$. The condition Y=3 has the highest conditional spread.

---

#### Problem CV5: Conditional Variance with Continuous Thinking

A student's exam score S depends on preparation hours H. Given H = h hours:
$$E[S \mid H = h] = 40 + 5h$$
$$\text{Var}(S \mid H = h) = 20 + h$$

If H takes values {1, 2, 3} with equal probability:

a) Find $E[S]$ and $\text{Var}(S)$
b) What fraction of total variance is explained by study hours (between-group)?

> [!success]- Solution (with theory)
>
> **Concept — Law of Total Variance as an ANOVA decomposition:**
>
> The Law of Total Variance $\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$ partitions total variance into:
> - **Within-group variance** $E[\text{Var}(X \mid Y)]$: variability that remains after knowing group membership — this is "noise" you can't explain
> - **Between-group variance** $\text{Var}(E[X \mid Y])$: variability due to differences in group means — this is "signal" explained by Y
>
> The ratio $\text{Var}(E[X \mid Y]) / \text{Var}(X)$ is $R^2$ — the fraction of total variance explained by Y.
>
> a) $E[S \mid H=1] = 45$, $E[S \mid H=2] = 50$, $E[S \mid H=3] = 55$
> $E[S] = (45+50+55)/3 = 150/3 = 50$
>
> **Within-group:**
> $\text{Var}(S \mid H=1) = 21$, $\text{Var}(S \mid H=2) = 22$, $\text{Var}(S \mid H=3) = 23$
> $E[\text{Var}(S \mid H)] = (21+22+23)/3 = 66/3 = 22$
>
> **Between-group:**
> $E[S \mid H]$ = {45, 50, 55}, each prob 1/3
> $\text{Var}(E[S \mid H]) = E[(E[S \mid H])^2] - (E[S])^2$
> $= (45^2+50^2+55^2)/3 - 50^2$
> $= (2025+2500+3025)/3 - 2500$
> $= 7550/3 - 2500 = 2516.67 - 2500 = 16.67$
>
> $\text{Var}(S) = 22 + 16.67 = 38.67$
>
> b) Fraction explained = $16.67/38.67 \approx 0.431$ (43.1%)
>
> **Interpretation:** About 43% of score variability comes from differences in study hours. The remaining 57% is due to other factors (ability, luck, etc.) even within the same study hour group.

---

## Part 3 — Law of Total Variance (LTV)

---

#### Problem LTV1: LTV — Two-Group Decomposition

A company has two divisions:
- Division A (65% of employees): avg salary = \$50K, variance = 100
- Division B (35% of employees): avg salary = \$70K, variance = 144

Find overall salary variance and decomose into within/between.

> [!success]- Solution (with theory)
>
> **Concept — The Law of Total Variance has two interpretations:**
>
> 1. **Formula:** $\text{Var}(S) = E[\text{Var}(S \mid \text{div})] + \text{Var}(E[S \mid \text{div}])$
> 2. **Intuition:** Total variability in salary = average variability within each division + variability due to division differences
>
> If all divisions had the same average salary, the between-group term would be zero. If every employee in a division earned exactly the same, the within-group term would be zero. Real data has both.
>
> ---
>
> **Step 1 — $E[S]$:**
> $E[S] = 50(0.65) + 70(0.35) = 32.5 + 24.5 = 57$
>
> **Step 2 — Within-division variance:**
> $E[\text{Var}(S \mid \text{div})] = 100(0.65) + 144(0.35) = 65 + 50.4 = 115.4$
>
> **Step 3 — Between-division variance:**
> $E[(E[S \mid \text{div}])^2] = 50^2(0.65) + 70^2(0.35) = 1625 + 1715 = 3340$
> $\text{Var}(E[S \mid \text{div}]) = 3340 - 57^2 = 3340 - 3249 = 91$
>
> **Step 4 — Total:**
> $\text{Var}(S) = 115.4 + 91 = 206.4$
>
> Within: $115.4/206.4 \approx 55.9\%$ | Between: $91/206.4 \approx 44.1\%$
>
> **Interpretation:** Even within the same division, salaries vary substantially (55.9% of total). But knowing which division someone works in reduces uncertainty by 44.1% — a meaningful but not dominant effect.

---

#### Problem LTV2: LTV — Three-Group (Restaurant)

A restaurant chain has 3 locations:
| Location | % of sales | Avg profit (\$K) | Variance |
|----------|-----------|-----------------|----------|
| Downtown | 40% | 120 | 400 |
| Suburb | 35% | 80 | 225 |
| Mall | 25% | 150 | 625 |

Find total profit variance. Which component (within or between) is larger?

> [!success]- Solution (with theory)
>
> **Concept — When between-group variance dominates:**
>
> The three locations have very different average profits (80, 120, 150), so we expect a large between-group contribution. The two components tell us:
> - **Within** = how much individual restaurants vary within the same location type
> - **Between** = how much the locations differ from each other
>
> When between > within, location is a strong predictor.
>
> ---
>
> $E[P] = 120(0.4) + 80(0.35) + 150(0.25) = 48 + 28 + 37.5 = 113.5$
>
> **Within:**
> $E[\text{Var}(P \mid \text{loc})] = 400(0.4) + 225(0.35) + 625(0.25) = 160 + 78.75 + 156.25 = 395$
>
> **Between:**
> $E[(E[P \mid \text{loc}])^2] = 120^2(0.4) + 80^2(0.35) + 150^2(0.25)$
> $= 5760 + 2240 + 5625 = 13625$
> $\text{Var}(E[P \mid \text{loc}]) = 13625 - (113.5)^2 = 13625 - 12882.25 = 742.75$
>
> $\text{Var}(P) = 395 + 742.75 = 1137.75$
>
> Within: $395/1137.75 \approx 34.7\%$ | Between: $742.75/1137.75 \approx 65.3\%$
>
> **Between-location variance dominates** (65.3% vs 34.7%) — location significantly affects profit. If you want to understand why some restaurants perform better, start by looking at the location type.

---

#### Problem LTV3: LTV — Proof Practice

Prove the Law of Total Variance:
$$\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$$

> [!success]- Solution
> **Step 1:** Start with shortcut formula
> $$\text{Var}(X) = E[X^2] - (E[X])^2$$
>
> **Step 2:** Apply LTE to $E[X^2]$ and $E[X]$
> $$E[X^2] = E[E[X^2 \mid Y]], \qquad E[X] = E[E[X \mid Y]]$$
>
> **Step 3:** Substitute
> $$\text{Var}(X) = E[E[X^2 \mid Y]] - (E[E[X \mid Y]])^2$$
>
> **Step 4:** Rewrite $E[X^2 \mid Y] = \text{Var}(X \mid Y) + (E[X \mid Y])^2$
> $$\text{Var}(X) = E[\text{Var}(X \mid Y) + (E[X \mid Y])^2] - (E[E[X \mid Y]])^2$$
>
> **Step 5:** Split
> $$\text{Var}(X) = E[\text{Var}(X \mid Y)] + \underbrace{E[(E[X \mid Y])^2] - (E[E[X \mid Y]])^2}_{\text{Var}(E[X \mid Y])}$$
>
> **Step 6:** Conclude
> $$\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$$
>
> **Intuition:** Total variance = average within-group variance + variance of group means.

---

#### Problem LTV4: LTV — Insurance Claims

Insurance claims vary by policy type:
- Basic (50%): $E[C] = \$200$, $\text{Var}(C) = 10,000$
- Standard (30%): $E[C] = \$500$, $\text{Var}(C) = 40,000$
- Premium (20%): $E[C] = \$1,000$, $\text{Var}(C) = 160,000$

a) Find expected claim $E[C]$
b) Find $\text{Var}(C)$
c) What fraction is due to policy type differences? What does this imply?

> [!success]- Solution (with theory)
>
> **Concept — Why decompose variance?**
>
> The LTV decomposition tells us where risk comes from. For insurance:
> - If most variance is **within** policy types → pricing should focus on refining within-type risk assessment
> - If most variance is **between** policy types → pricing should strongly differentiate by type
>
> The fraction $\text{Var}(E[C \mid \text{type}]) / \text{Var}(C)$ tells you how much claim variability is "explained" by policy type alone.
>
> ---
>
> a) $E[C] = 200(0.5) + 500(0.3) + 1000(0.2) = 100 + 150 + 200 = \$450$
>
> b) **Within:**
> $E[\text{Var}(C \mid \text{type})] = 10000(0.5) + 40000(0.3) + 160000(0.2)$
> $= 5000 + 12000 + 32000 = 49,000$
>
> **Between:**
> $E[(E[C \mid \text{type}])^2] = 200^2(0.5) + 500^2(0.3) + 1000^2(0.2)$
> $= 40000(0.5) + 250000(0.3) + 1000000(0.2)$
> $= 20000 + 75000 + 200000 = 295,000$
> $\text{Var}(E[C \mid \text{type}]) = 295000 - 450^2 = 295000 - 202500 = 92,500$
>
> $\text{Var}(C) = 49000 + 92500 = 141,500$
>
> c) Between fraction: $92500/141500 \approx 0.654$ (65.4%)
>
> **Implication:** Most claim variability (65.4%) comes from policy type differences, not randomness within a type. Pricing should differentiate strongly by type. However, even within a single policy type, there's still substantial variance ($\sigma \approx \sqrt{49000/0.5} \approx \$313$ for Basic).

---

#### Problem LTV5: LTV — Manufacturing

Three suppliers provide components:
| Supplier | % of parts | Mean strength (MPa) | Variance |
|----------|-----------|-------------------|----------|
| X | 45% | 120 | 25 |
| Y | 30% | 110 | 36 |
| Z | 25% | 130 | 49 |

Find overall variance. If you could reduce variance in only one supplier by 50%, which would most reduce total variance?

> [!success]- Solution (with theory)
>
> **Concept — Where to invest quality improvement?**
>
> The LTV decomposition helps identify the biggest leverage point. Each supplier's contribution to within-group variance is ($\text{Var}_i \times p_i$). Halving supplier $i$'s variance reduces total variance by $\frac{\text{Var}_i}{2} \times p_i$.
>
> The decision isn't about which supplier has the largest variance in absolute terms — it's about the product of variance and share. Supplier Z has high variance (49) despite low share (25%), while Supplier X has moderate variance (25) but high share (45%).
>
> ---
>
> $E[S] = 120(0.45) + 110(0.3) + 130(0.25) = 54 + 33 + 32.5 = 119.5$
>
> **Within:**
> $E[\text{Var}(S \mid \text{supp})] = 25(0.45) + 36(0.3) + 49(0.25) = 11.25 + 10.8 + 12.25 = 34.3$
>
> **Between:**
> $E[(E[S \mid \text{supp}])^2] = 120^2(0.45) + 110^2(0.3) + 130^2(0.25)$
> $= 14400(0.45) + 12100(0.3) + 16900(0.25)$
> $= 6480 + 3630 + 4225 = 14335$
> $\text{Var}(E[S \mid \text{supp}]) = 14335 - (119.5)^2 = 14335 - 14280.25 = 54.75$
>
> $\text{Var}(S) = 34.3 + 54.75 = 89.05$
>
> **Reduction analysis (halving one supplier's within-variance):**
> - Supplier X: reduction = $(25/2)(0.45) = 5.625$
> - Supplier Y: reduction = $(36/2)(0.3) = 5.4$
> - Supplier Z: reduction = $(49/2)(0.25) = 6.125$
>
> **Supplier Z** gives the biggest reduction (6.125), despite being the smallest share (25%), because its within-variance (49) is largest.

---

## Part 4 — Covariance: First-Principles Deep Dive

---

### Foundations — What covariance actually measures

#### Step 1: The core question

We have two random variables, $X$ and $Y$. We know how to measure the variability of each one individually ($\text{Var}(X)$, $\text{Var}(Y)$). But we want to know: **do $X$ and $Y$ move together?**

- When $X$ goes **up** (above its mean), does $Y$ also tend to go **up**?
- Or when $X$ goes up, does $Y$ tend to go **down**?
- Or is there **no relationship** — knowing $X$ tells us nothing about $Y$?

Covariance is the answer to this question.

#### Step 2: The intuition — products of deviations

Let $\mu_X = E[X]$ and $\mu_Y = E[Y]$ be the center points.

For a single observation $(x, y)$:
- $x - \mu_X$ = "how far is this X from its average?" (positive = above avg, negative = below)
- $y - \mu_Y$ = "how far is this Y from its average?"

Now multiply them: $(x - \mu_X)(y - \mu_Y)$

| Scenario | $x-\mu_X$ | $y-\mu_Y$ | Product | Interpretation |
|----------|-----------|-----------|---------|---------------|
| Both above avg | + | + | **+** | They move together |
| Both below avg | - | - | **+** | They move together |
| X above, Y below | + | - | **-** | They move opposite |
| X below, Y above | - | + | **-** | They move opposite |

**The product is positive when they're on the same side of their means, negative when they're on opposite sides.**

#### Step 3: From one observation to the average

One observation doesn't tell us much. We need the **average** product over all possibilities, weighted by probability:

$$\text{Cov}(X,Y) = E[(X - \mu_X)(Y - \mu_Y)]$$

This is the **definition**. Everything else is derived from this.

Think of it as:
$$\text{Cov}(X,Y) = \sum_{\text{all }x}\sum_{\text{all }y} (x - \mu_X)(y - \mu_Y) \cdot P(X=x, Y=y)$$

#### Step 4: Deriving the shortcut formula

Start with the definition:

$$\text{Cov}(X,Y) = E[(X - \mu_X)(Y - \mu_Y)]$$

Expand the product:

$$= E[XY - \mu_X Y - \mu_Y X + \mu_X\mu_Y]$$

Linearity of expectation lets us split:

$$= E[XY] - \mu_X E[Y] - \mu_Y E[X] + \mu_X\mu_Y$$

But $E[X] = \mu_X$ and $E[Y] = \mu_Y$:

$$= E[XY] - \mu_X\mu_Y - \mu_Y\mu_X + \mu_X\mu_Y$$

$$= E[XY] - \mu_X\mu_Y$$

So:

$$\boxed{\text{Cov}(X,Y) = E[XY] - E[X]E[Y]}$$

**This is NOT a new formula — it's just the definition expanded algebraically.** Use whichever is easier to compute.

#### Step 5: Connection to variance

Notice: $\text{Var}(X) = E[X^2] - (E[X])^2 = E[X \cdot X] - E[X]E[X] = \text{Cov}(X, X)$

**Variance is just covariance of X with itself.** This is why the formulas look identical — variance IS covariance (with yourself).

---

### How to read a joint probability table

This is the most important practical skill. Let's take a simple 2×2 table:

**Table structure:**

```
         Y=0    Y=1    ← These are the values Y can take
         ---    ---
X=0  |  p_00   p_01   |  P(X=0)
X=1  |  p_10   p_11   |  P(X=1)
      -------  -------
      P(Y=0)  P(Y=1)
```

**What each cell means:**

- $p_{00} = P(X=0, Y=0)$ = probability that **simultaneously** X=0 AND Y=0
- $p_{01} = P(X=0, Y=1)$ = probability that X=0 AND Y=1
- $p_{10} = P(X=1, Y=0)$ = probability that X=1 AND Y=0
- $p_{11} = P(X=1, Y=1)$ = probability that X=1 AND Y=1

All four cells sum to 1 (total probability).

**Row sums (marginal of X):**
- $P(X=0) = p_{00} + p_{01}$ (sum across row 0)
- $P(X=1) = p_{10} + p_{11}$ (sum across row 1)

**Column sums (marginal of Y):**
- $P(Y=0) = p_{00} + p_{10}$ (sum down column 0)
- $P(Y=1) = p_{01} + p_{11}$ (sum down column 1)

---

### How to compute each expectation from the table

**$E[X]$ uses the marginal of X:**
$$E[X] = \sum_x x \cdot P(X=x) = 0 \cdot P(X=0) + 1 \cdot P(X=1)$$
Just take each X value, multiply by its row total, sum them up.

**$E[Y]$ uses the marginal of Y:**
$$E[Y] = \sum_y y \cdot P(Y=y) = 0 \cdot P(Y=0) + 1 \cdot P(Y=1)$$
Same idea — each Y value times its column total.

**$E[XY]$ uses every cell:**
$$E[XY] = \sum_x \sum_y x \cdot y \cdot P(X=x, Y=y)$$
For each cell, multiply **(row value) × (column value) × (cell probability)**.

This is the critical difference:
- $E[X]$ only needs row totals (summing across columns first)
- $E[Y]$ only needs column totals (summing across rows first)
- $E[XY]$ needs every individual cell — because $x \cdot y$ changes for each cell

#### Worked example — 2×2 table walkthrough

```
        Y=0    Y=1
        ---    ---
X=0  |  0.2    0.3   |  0.5
X=1  |  0.1    0.4   |  0.5
       ----   ----
       0.3    0.7
```

**Step-by-step:**

1. $E[X] = 0(0.5) + 1(0.5) = 0.5$ — half the time X=0, half the time X=1
   - Row 0 total = 0.2+0.3 = 0.5, Row 1 total = 0.1+0.4 = 0.5

2. $E[Y] = 0(0.3) + 1(0.7) = 0.7$ — Y is more often 1 than 0
   - Col 0 total = 0.2+0.1 = 0.3, Col 1 total = 0.3+0.4 = 0.7

3. $E[XY]$:
   - Cell (X=0, Y=0): $0 \times 0 \times 0.2 = 0$ (zero because X=0 makes the product 0)
   - Cell (X=0, Y=1): $0 \times 1 \times 0.3 = 0$ (zero because X=0)
   - Cell (X=1, Y=0): $1 \times 0 \times 0.1 = 0$ (zero because Y=0)
   - Cell (X=1, Y=1): $1 \times 1 \times 0.4 = 0.4$ (nonzero only when BOTH are 1)
   - **Total: $E[XY] = 0 + 0 + 0 + 0.4 = 0.4$**

4. $\text{Cov}(X,Y) = 0.4 - (0.5)(0.7) = 0.4 - 0.35 = 0.05$

**Interpretation:** Positive, but weak. When both are 1 (probability 0.4), it's slightly more than what independence would predict (0.5×0.7=0.35), giving a slight positive co-movement.

---

### The quadrant diagram (visual intuition)

```
                 Y  
                 ↑
                 |    Quadrant II          Quadrant I
                 |   (X low, Y high)      (X high, Y high)
                 |   product negative      product positive
                 |    
                 +---------μ_Y--------→
                 |    
                 |   Quadrant III         Quadrant IV
                 |   (X low, Y low)       (X high, Y low)
                 |   product positive     product negative
                 |
                 +------------------------→ X
                 μ_X
```

Covariance checks: which quadrants have the most probability mass?
- If mass is concentrated in QI and QIII (same-sign deviations) → **positive covariance**
- If mass is concentrated in QII and QIV (opposite-sign deviations) → **negative covariance**
- If mass is evenly spread across all four → **covariance near zero**

---

### Properties of covariance

1. **Symmetry:** $\text{Cov}(X,Y) = \text{Cov}(Y,X)$ — swapping doesn't change it

2. **Variance is Cov(X,X):** $\text{Var}(X) = \text{Cov}(X,X)$

3. **Bilinearity:** $\text{Cov}(aX + bY, cZ + dW) = ac\,\text{Cov}(X,Z) + ad\,\text{Cov}(X,W) + bc\,\text{Cov}(Y,Z) + bd\,\text{Cov}(Y,W)$
   - This means covariance behaves like multiplication when you have linear combinations

4. **Adding constants doesn't change it:** $\text{Cov}(X + c, Y + d) = \text{Cov}(X,Y)$
   - Because shifting doesn't affect deviations from the mean

5. **Scaling multiplies:** $\text{Cov}(aX, bY) = ab\,\text{Cov}(X,Y)$
   - If you change units, covariance changes accordingly

6. **Not bounded:** Covariance can be any real number (unlike correlation which is [-1,1])

7. **Zero doesn't mean independent:** $\text{Cov}(X,Y) = 0$ does NOT imply $X$ and $Y$ are independent
   - Example: $Y = X^2$ with symmetric $X$ gives $\text{Cov}(X, X^2) = 0$ even though they're deterministically related
   - Covariance only captures **linear** relationships

---

#### Problem COV1: Covariance from a 3×3 Table — Full Cell-by-Cell Walkthrough

| X\Y | -1 | 0 | 1 |
|---|---|---|---|
| -1 | 0.1 | 0.05 | 0.05 |
| 0 | 0.05 | 0.3 | 0.05 |
| 1 | 0.05 | 0.05 | 0.3 |

Find $\text{Cov}(X, Y)$ and interpret.

> [!success]- Solution (with theory) — Cell-by-Cell Walkthrough
>
> This solution walks through **every single number** in the table and explains where it comes from and what it contributes.
>
> ---
>
> ### Step 1: Understanding the table structure
>
> The table has:
> - **3 rows** = X can be -1, 0, or 1
> - **3 columns** = Y can be -1, 0, or 1
> - **9 cells** = each combination of (X, Y)
>
> Each cell $P(X=x, Y=y)$ is the probability that **both** events happen simultaneously.
>
> For example, the top-left cell = 0.1 means:
> - There is a **10% chance** that X = -1 AND Y = -1 at the same time
> - This is ONE joint outcome, not two separate events
>
> **Read the table like a grid:** pick a row (X value), pick a column (Y value), read the cell where they meet.
>
> ---
>
> ### Step 2: Row sums = marginal probabilities of X
>
> To find $P(X=-1)$, look at row X=-1 and add ALL columns:
> $$P(X=-1) = 0.1 + 0.05 + 0.05 = 0.2$$
> This means: "regardless of what Y is, X is -1 with 20% probability."
>
> $$P(X=0) = 0.05 + 0.3 + 0.05 = 0.4$$
> $$P(X=1) = 0.05 + 0.05 + 0.3 = 0.4$$
>
> **Check:** $0.2 + 0.4 + 0.4 = 1.0$ ✅
>
> ---
>
> ### Step 3: Column sums = marginal probabilities of Y
>
> To find $P(Y=-1)$, look at column Y=-1 and add ALL rows:
> $$P(Y=-1) = 0.1 + 0.05 + 0.05 = 0.2$$
>
> $$P(Y=0) = 0.05 + 0.3 + 0.05 = 0.4$$
> $$P(Y=1) = 0.05 + 0.05 + 0.3 = 0.4$$
>
> **Check:** $0.2 + 0.4 + 0.4 = 1.0$ ✅
>
> ---
>
> ### Step 4: Computing $E[X]$ — the center of X
>
> $E[X] = \sum_x x \cdot P(X=x)$
>
> This uses ONLY the row totals (marginals of X). Each X value times its probability:
>
> $$E[X] = (-1)(0.2) + (0)(0.4) + (1)(0.4)$$
> $$= -0.2 + 0 + 0.4 = 0.2$$
>
> **What this means:** The average of X is slightly positive (0.2) because X=1 has higher probability (0.4) than X=-1 (0.2).
>
> ---
>
> ### Step 5: Computing $E[Y]$ — the center of Y
>
> $E[Y] = \sum_y y \cdot P(Y=y)$
>
> This uses ONLY the column totals:
>
> $$E[Y] = (-1)(0.2) + (0)(0.4) + (1)(0.4)$$
> $$= -0.2 + 0 + 0.4 = 0.2$$
>
> **Same** as $E[X]$ — both are centered slightly above 0.
>
> ---
>
> ### Step 6: Computing $E[XY]$ — THIS is where covariance lives
>
> $E[XY] = \sum_x \sum_y x \cdot y \cdot P(X=x, Y=y)$
>
> **For each of the 9 cells:**
> - Take the row's X value
> - Take the column's Y value
> - Multiply them together: $x \cdot y$
> - Multiply by the cell probability $P(x,y)$
> - Add all 9 results
>
> **Why $x \cdot y$?** Because $(X-\mu_X)(Y-\mu_Y)$ expands to include $XY$ as the main term. The product $x \cdot y$ is large and positive when both are big with the same sign, large and negative when they have opposite signs.
>
> **Cell-by-cell breakdown:**
>
> | Cell (X, Y) | $x$ | $y$ | $x \cdot y$ | $P(x,y)$ | Contribution = $x\cdot y \cdot P(x,y)$ |
> |-------------|-----|-----|-------------|----------|--------------------------------------|
> | (-1, -1) | -1 | -1 | **+1** | 0.1 | $+1 \times 0.1 = \mathbf{+0.1}$ |
> | (-1, 0) | -1 | 0 | **0** | 0.05 | $0 \times 0.05 = \mathbf{0}$ |
> | (-1, 1) | -1 | 1 | **-1** | 0.05 | $-1 \times 0.05 = \mathbf{-0.05}$ |
> | (0, -1) | 0 | -1 | **0** | 0.05 | $0 \times 0.05 = \mathbf{0}$ |
> | (0, 0) | 0 | 0 | **0** | 0.3 | $0 \times 0.3 = \mathbf{0}$ |
> | (0, 1) | 0 | 1 | **0** | 0.05 | $0 \times 0.05 = \mathbf{0}$ |
> | (1, -1) | 1 | -1 | **-1** | 0.05 | $-1 \times 0.05 = \mathbf{-0.05}$ |
> | (1, 0) | 1 | 0 | **0** | 0.05 | $0 \times 0.05 = \mathbf{0}$ |
> | (1, 1) | 1 | 1 | **+1** | 0.3 | $+1 \times 0.3 = \mathbf{+0.3}$ |
>
> **Key observations:**
> - Any cell where either $X=0$ or $Y=0$ contributes **zero** (because the product $x\cdot y = 0$)
> - Only cells where BOTH are non-zero contribute
> - The diagonal cells (-1,-1) and (1,1) contribute **positive** (same sign = co-movement)
> - The off-diagonal cells (-1,1) and (1,-1) contribute **negative** (opposite sign = opposite movement)
>
> **Sum:**
> $$E[XY] = 0.1 + 0 - 0.05 + 0 + 0 + 0 - 0.05 + 0 + 0.3 = 0.3$$
>
> ---
>
> ### Step 7: Computing Covariance
>
> $$\text{Cov}(X,Y) = E[XY] - E[X]E[Y]$$
>
> $$= 0.3 - (0.2)(0.2) = 0.3 - 0.04 = 0.26$$
>
> **Step-by-step meaning of this subtraction:**
>
> $E[XY] = 0.3$ is the actual average product.
>
> $E[X]E[Y] = 0.04$ is what $E[XY]$ WOULD BE if X and Y were independent (because if independent, $E[XY] = E[X]E[Y]$).
>
> The difference $0.3 - 0.04 = 0.26 > 0$ means: **X and Y occur together with the same sign more often than they would if independent.**
>
> **How big is 0.26?** Hard to say without standardization — that's why we have correlation. For now, the SIGN tells the story: positive.
>
> ---
>
> ### Step 8: Intuition check with the table
>
> Look at the diagonal cells:
> - $P(X=-1, Y=-1) = 0.1$ — both negative
> - $P(X=1, Y=1) = 0.3$ — both positive
> **Total probability on diagonal = 0.1 + 0.3 = 0.4**
>
> Look at the off-diagonal cells (opposite signs):
> - $P(X=-1, Y=1) = 0.05$
> - $P(X=1, Y=-1) = 0.05$
> **Total probability off-diagonal = 0.05 + 0.05 = 0.1**
>
> The diagonal has 4× more probability mass than the off-diagonal! This tells us X and Y tend to have the same sign, which means **positive covariance**.

---

#### Problem COV2: Covariance Bilinearity — Proof Practice

Expand $\text{Cov}(aX + bY, cZ + dW)$ in terms of covariances between X,Y,Z,W.

> [!success]- Solution (with theory)
>
> **Concept — Covariance behaves like multiplication:**
>
> Bilinearity means covariance is "linear in each argument." This is the single most useful algebraic property because it lets us break complex expressions into simple covariance terms.
>
> **Proof outline:**
> 1. Write the definition: $\text{Cov}(U,V) = E[UV] - E[U]E[V]$
> 2. Expand $UV$ and $E[U]E[V]$ using algebra
> 3. Group terms to recognize $\text{Cov}$ expressions
>
> **Step 1 — Start with definition:**
> $$\text{Cov}(U,V) = E[UV] - E[U]E[V]$$
> where $U = aX + bY$, $V = cZ + dW$.
>
> **Step 2 — $E[UV]$ (expand product, then use linearity):**
> $E[UV] = E[(aX + bY)(cZ + dW)]$
> $= E[acXZ + adXW + bcYZ + bdYW]$
> $= ac\,E[XZ] + ad\,E[XW] + bc\,E[YZ] + bd\,E[YW]$
>
> **Step 3 — $E[U]E[V]$ (linearity, then multiply):**
> $E[U]E[V] = (aE[X] + bE[Y])(cE[Z] + dE[W])$
> $= ac\,E[X]E[Z] + ad\,E[X]E[W] + bc\,E[Y]E[Z] + bd\,E[Y]E[W]$
>
> **Step 4 — Subtract (pair up matching terms):**
> $\text{Cov}(U,V) = [ac\,E[XZ] - ac\,E[X]E[Z]]$
> $\qquad\qquad + [ad\,E[XW] - ad\,E[X]E[W]]$
> $\qquad\qquad + [bc\,E[YZ] - bc\,E[Y]E[Z]]$
> $\qquad\qquad + [bd\,E[YW] - bd\,E[Y]E[W]]$
>
> $= ac(E[XZ] - E[X]E[Z]) + ad(E[XW] - E[X]E[W])$
> $\qquad + bc(E[YZ] - E[Y]E[Z]) + bd(E[YW] - E[Y]E[W])$
>
> **Step 5 — Recognize covariance in each bracket:**
> $$\text{Cov}(aX + bY, cZ + dW) = ac\,\text{Cov}(X,Z) + ad\,\text{Cov}(X,W) + bc\,\text{Cov}(Y,Z) + bd\,\text{Cov}(Y,W)$$
>
> **Why this matters:** This formula is the engine behind every variance-of-a-sum calculation. For example, $\text{Var}(X+Y) = \text{Cov}(X+Y, X+Y)$ — apply bilinearity and you get $\text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y)$ immediately.

---

#### Problem COV3: Variance of a Sum — The Bilinearity Connection

Given:
$$\text{Var}(X) = 10,\; \text{Var}(Y) = 20,\; \text{Cov}(X,Y) = 5$$

Find:
a) $\text{Var}(X + Y)$
b) $\text{Var}(X - Y)$
c) $\text{Var}(2X - 3Y)$

> [!success]- Solution (with theory)
>
> **Concept — Variance IS covariance with itself:**
>
> $\text{Var}(X + Y) = \text{Cov}(X+Y, X+Y)$
>
> Apply bilinearity (from COV2) with $a=1, b=1, c=1, d=1$:
> $\text{Cov}(X+Y, X+Y) = 1\cdot1\cdot\text{Cov}(X,X) + 1\cdot1\cdot\text{Cov}(X,Y) + 1\cdot1\cdot\text{Cov}(Y,X) + 1\cdot1\cdot\text{Cov}(Y,Y)$
> $= \text{Var}(X) + \text{Cov}(X,Y) + \text{Cov}(X,Y) + \text{Var}(Y)$
> $= \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y)$
>
> **The 2 comes from symmetry:** $\text{Cov}(X,Y) = \text{Cov}(Y,X)$, so the cross terms appear twice.
>
> **For $X - Y$:** Same idea but the cross term flips sign:
> $\text{Var}(X - Y) = \text{Cov}(X-Y, X-Y)$
> $= \text{Var}(X) + (-1)(-1)\text{Var}(Y) + 2(1)(-1)\text{Cov}(X,Y)$
> $= \text{Var}(X) + \text{Var}(Y) - 2\text{Cov}(X,Y)$
>
> **Intuitive meaning:**
> - If $\text{Cov}(X,Y) > 0$ (they move together): adding them amplifies the variance, subtracting reduces it
> - If $\text{Cov}(X,Y) < 0$ (they move opposite): adding them reduces variance, subtracting amplifies it
>
> This is the mathematical basis of **diversification** — combining negatively correlated assets reduces portfolio variance.
>
> ---
>
> a) $\text{Var}(X + Y) = 10 + 20 + 2(5) = 10 + 20 + 10 = 40$
>
> b) $\text{Var}(X - Y) = 10 + 20 - 2(5) = 30 - 10 = 20$
>
> c) $\text{Var}(2X - 3Y)$: Use bilinearity with $a=2, b=-3, c=2, d=-3$:
> $= 2^2\text{Var}(X) + (-3)^2\text{Var}(Y) + 2(2)(-3)\text{Cov}(X,Y)$
> $= 4(10) + 9(20) - 12(5)$
> $= 40 + 180 - 60 = 160$
>
> **Check the signs:** $\text{Cov}=5>0$ means X and Y go up together. Adding them ($X+Y$) gives a +10 boost from covariance. Subtracting ($X-Y$) gives a -10 effect. Scaling $2X-3Y$ with the large negative coefficient (-3) makes the covariance contribution negative (-60), subtracting from total variance.

---

#### Problem COV4: Covariance of Sum and Difference

Let X and Y have: $\mu_X = 10$, $\mu_Y = 20$, $\sigma_X^2 = 25$, $\sigma_Y^2 = 36$, $\rho = 0.5$.

Define $U = X + Y$ and $V = X - Y$.

a) Find $\text{Cov}(U, V)$ and $\rho_{UV}$
b) Are U and V independent? Why or why not?

> [!success]- Solution (with theory)
>
> **Concept — What happens when you form sum and difference?**
>
> Using bilinearity: $\text{Cov}(X+Y, X-Y) = \text{Var}(X) - \text{Var}(Y)$
>
> **Derivation:**
> $\text{Cov}(X+Y, X-Y) = \text{Cov}(X,X) - \text{Cov}(X,Y) + \text{Cov}(Y,X) - \text{Cov}(Y,Y)$
> $= \text{Var}(X) - \text{Cov}(X,Y) + \text{Cov}(X,Y) - \text{Var}(Y)$
> $= \text{Var}(X) - \text{Var}(Y)$
>
> **Key insight:** When $\text{Var}(X) = \text{Var}(Y)$, the sum and difference are always uncorrelated, regardless of $\rho_{XY}$! Here $\text{Var}(X) \neq \text{Var}(Y)$, so we get a non-zero result.
>
> ---
>
> a) First find $\text{Cov}(X,Y)$ from correlation:
> $\text{Cov}(X,Y) = \rho\sigma_X\sigma_Y = 0.5(5)(6) = 15$
>
> $\text{Cov}(U,V) = \text{Cov}(X+Y, X-Y)$
> $= \text{Var}(X) - \text{Var}(Y)$
> $= 25 - 36 = -11$
>
> **Interpretation:** $U$ (sum) and $V$ (difference) have negative covariance. When the sum goes up, the difference tends to go down. This makes sense: if X increases more than Y, the sum goes up but the difference (X-Y) also goes up... except here $\text{Var}(Y) > \text{Var}(X)$, so Y's movements dominate.
>
> $\text{Var}(U) = \text{Var}(X+Y) = 25 + 36 + 2(15) = 91$, $\sigma_U = \sqrt{91} \approx 9.539$
> $\text{Var}(V) = \text{Var}(X-Y) = 25 + 36 - 2(15) = 31$, $\sigma_V = \sqrt{31} \approx 5.568$
>
> $\rho_{UV} = \frac{-11}{\sqrt{91}\sqrt{31}} \approx \frac{-11}{53.12} \approx -0.207$
>
> **Correlation is weak** despite $\rho_{XY}=0.5$, because the variances are close in magnitude.
>
> b) No, U and V are not independent. $\text{Cov}(U,V) \neq 0$ directly implies they are dependent. **The contrapositive holds: if independent, Cov=0. But Cov=0 doesn't imply independence.** Here we have Cov ≠ 0, so they're definitely dependent.

---

#### Problem COV5: Covariance with a Constant

Prove: $\text{Cov}(X, c) = 0$ for any constant $c$. What does this mean intuitively?

> [!success]- Solution (with theory)
>
> **Proof (definition):**
> $\text{Cov}(X, c) = E[(X - \mu_X)(c - E[c])]$
>
> But $c$ is constant, so $E[c] = c$, which means $c - E[c] = 0$:
> $\text{Cov}(X, c) = E[(X - \mu_X)(0)] = E[0] = 0$
>
> **Proof (shortcut):**
> $\text{Cov}(X, c) = E[X \cdot c] - E[X]E[c]$
> $= cE[X] - E[X] \cdot c$
> $= cE[X] - cE[X] = 0$
>
> **Intuition at three levels:**
>
> 1. **Algebraic:** $c$ is constant so $E[c] = c$ and the terms cancel perfectly.
>
> 2. **Geometric:** A constant has no variation (its variance is 0). It can't "co-vary" with anything because it doesn't vary at all. Covariance measures joint movement — a constant is a flat line.
>
> 3. **Practical:** This is why adding constants doesn't affect covariance. $\text{Cov}(X+c, Y+d) = \text{Cov}(X,Y)$ because constants have zero covariance with everything.
>
> **General lesson:** Any deterministic quantity (one with zero variance) has zero covariance with any random variable. This is why $\text{Cov}(X, f(X)) \neq 0$ in general — $f(X)$ IS random because it depends on X.

---

## Part 5 — Correlation

---

#### Problem R1: Correlation from Covariance

Given: $\text{Var}(X) = 25$, $\text{Var}(Y) = 49$, $\text{Cov}(X,Y) = 14$

a) Find $\rho_{XY}$
b) If you transform $U = 2X$ and $V = 3Y$, what is $\rho_{UV}$?
c) What does the sign and magnitude tell you?

> [!success]- Solution (with theory)
>
> **Concept — Correlation is scale-invariant:**
>
> $\rho_{XY} = \frac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y}$ is **unitless** and bounded by $[-1, 1]$.
>
> Key property: $\rho_{aX+b, cY+d} = \text{sign}(ac) \cdot \rho_{XY}$
> - Adding constants doesn't change ρ (shift doesn't affect co-movement)
> - Multiplying by positive constants doesn't change ρ (scaling cancels in numerator and denominator)
> - Multiplying by a negative constant flips the sign only
>
> This is why correlation is preferred over covariance for interpretation — it's a standardized measure.
>
> ---
>
> a) $\sigma_X = 5$, $\sigma_Y = 7$
> $\rho_{XY} = 14 / (5 \times 7) = 14/35 = 0.4$
>
> b) $U = 2X$, $V = 3Y$ — both positive scaling, so:
> $\text{Cov}(U,V) = 6\text{Cov}(X,Y) = 6(14) = 84$
> $\sigma_U = 2(5) = 10$, $\sigma_V = 3(7) = 21$
> $\rho_{UV} = 84 / (10 \times 21) = 84/210 = 0.4$
>
> **Same ρ!** Scaling cancels out.
>
> c) $\rho = 0.4$: moderate positive linear relationship. A "medium" effect size in Cohen's convention. X explains $0.4^2 = 16\%$ of the variance in Y through a linear relationship.

---

#### Problem R2: Correlation Bounds Proof

Use Cauchy-Schwarz to prove $-1 \leq \rho_{XY} \leq 1$.

> [!success]- Solution
> **Step 1 — Start with a non-negative variance:**
> For any real t:
> $$\text{Var}(tX + Y) = t^2\text{Var}(X) + 2t\text{Cov}(X,Y) + \text{Var}(Y) \geq 0$$
>
> **Step 2 — This is a quadratic in t:** $at^2 + bt + c \geq 0$ where
> $a = \text{Var}(X)$, $b = 2\text{Cov}(X,Y)$, $c = \text{Var}(Y)$
>
> **Step 3 — For a quadratic to be $\geq 0$ for all t, its discriminant must be $\leq 0$:**
> $$b^2 - 4ac \leq 0$$
> $$(2\text{Cov})^2 - 4\text{Var}(X)\text{Var}(Y) \leq 0$$
> $$4\text{Cov}^2 \leq 4\text{Var}(X)\text{Var}(Y)$$
>
> **Step 4 — Divide by 4 and take square root:**
> $$|\text{Cov}(X,Y)| \leq \sqrt{\text{Var}(X)}\sqrt{\text{Var}(Y)} = \sigma_X\sigma_Y$$
>
> **Step 5 — Divide both sides by $\sigma_X\sigma_Y$:**
> $$\frac{|\text{Cov}(X,Y)|}{\sigma_X\sigma_Y} \leq 1$$
> $$|\rho_{XY}| \leq 1$$
> $$\boxed{-1 \leq \rho_{XY} \leq 1}$$
>
> **Equality when?** $\rho = \pm 1$ iff $Y = aX + b$ (perfect linear relationship).

---

#### Problem R3: Correlation After Transformation

$X$ and $Y$ have $\rho_{XY} = 0.8$. Find $\rho$ between:

a) $U = X + 5$ and $V = Y - 2$
b) $U = -X$ and $V = 2Y + 3$
c) $U = X$ and $V = -X + Y$

> [!success]- Solution (with theory)
>
> **Concept — How transformations affect correlation:**
>
> Correlation is invariant to:
> - Adding constants ($X \to X+c$, $Y \to Y+d$): shift doesn't affect co-movement
> - Scaling by positive constants: $\rho_{aX, bY} = \rho_{XY}$ because scale cancels
> - Negative scaling flips sign: $\rho_{-X, Y} = -\rho_{XY}$
>
> However, when you take **linear combinations** of X and Y (like $V = -X+Y$), the new variable mixes both, and the correlation depends on the relative variances of X and Y.
>
> ---
>
> a) $\rho_{UV} = \rho_{XY} = 0.8$ — adding constants doesn't affect correlation
>
> b) $\text{Cov}(-X, 2Y+3) = \text{Cov}(-X, 2Y) = -2\text{Cov}(X,Y)$
> $\text{Var}(-X) = \text{Var}(X)$, $\text{Var}(2Y+3) = 4\text{Var}(Y)$
> $\rho_{UV} = \frac{-2\text{Cov}(X,Y)}{\sigma_X \cdot 2\sigma_Y} = -\frac{\text{Cov}(X,Y)}{\sigma_X\sigma_Y} = -\rho_{XY} = -0.8$
>
> **Only sign flips** — magnitude unchanged.
>
> c) $\text{Cov}(X, -X+Y) = \text{Cov}(X,-X) + \text{Cov}(X,Y) = -\text{Var}(X) + \text{Cov}(X,Y)$
> Need $\sigma_X$ and $\sigma_Y$ to compute numerically. This illustrates that forming linear combos fundamentally changes correlation in ways that depend on the relative variances.

---

#### Problem R4: Correlation vs Causation

A study finds correlation of 0.9 between ice cream sales and drowning incidents.

a) Does this mean eating ice cream causes drowning?
b) What's a likely confounding variable?
c) If you control for temperature, what might happen to the correlation?

> [!success]- Solution
> a) **No!** Correlation ≠ Causation. This is a classic spurious correlation.
>
> b) **Confounder:** Temperature (summer). Hot weather → more people buy ice cream AND more people go swimming → more drowning incidents.
>
> c) If you control for temperature (look at data within each temperature band), the partial correlation would likely drop to near 0.
>
> **Key GATE insight:** $\rho_{XY} \neq 0$ doesn't imply X causes Y. There could be:
> - Reverse causation (Y → X)
> - Confounding variable Z (X ← Z → Y)
> - Coincidence

---

## Part 6 — Mixed & Challenge Problems

---

#### Problem MIX1: All Formulas at Once

Given:
$$P(A) = 0.3,\; P(B) = 0.6,\; P(A \cap B) = 0.15$$

Define indicator variables: $X = I_A$ (1 if A occurs, 0 otherwise), $Y = I_B$.

a) Find $E[X]$, $E[Y]$, $\text{Var}(X)$, $\text{Var}(Y)$
b) Find $\text{Cov}(X, Y)$ and $\rho_{XY}$
c) What is $\text{Var}(X + Y)$? Verify by direct computation.

> [!success]- Solution (with theory)
>
> **Concept — Indicator variables simplify probability:**
>
> For an indicator $I_A$ (1 if A occurs, 0 otherwise):
> - $E[I_A] = P(A)$ — because expectation of 0/1 variable is just the probability of 1
> - $I_A^2 = I_A$ — squaring doesn't change 0 or 1
> - $E[I_A I_B] = P(A \cap B)$ — product is 1 only when both occur
>
> These properties make indicator variables a powerful bridge between probability and expectation.
>
> ---
>
> a) $E[X] = P(A) = 0.3$, $E[Y] = P(B) = 0.6$
> $E[X^2] = E[X] = 0.3$ (since $X^2 = X$ for 0/1)
> $\text{Var}(X) = 0.3 - (0.3)^2 = 0.3 - 0.09 = 0.21$
> $\text{Var}(Y) = 0.6 - (0.6)^2 = 0.6 - 0.36 = 0.24$
>
> b) $E[XY] = P(A \cap B) = 0.15$ (product of indicators = 1 only when both occur)
> $\text{Cov}(X,Y) = 0.15 - (0.3)(0.6) = 0.15 - 0.18 = -0.03$
> $\rho_{XY} = -0.03 / (\sqrt{0.21}\sqrt{0.24}) \approx -0.03 / (0.458 \times 0.490) \approx -0.03/0.224 \approx -0.134$
>
> **Interpretation:** Despite $P(A \cap B) = 0.15$, the covariance is slightly negative. Why? Because $0.15 < 0.3 \times 0.6 = 0.18$ — the events occur together less often than independence would predict.
>
> c) $\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y)$
> $= 0.21 + 0.24 + 2(-0.03) = 0.45 - 0.06 = 0.39$
>
> **Direct verification:**
> $X+Y$ can be 0, 1, or 2.
> $P(X+Y=0) = P(A' \cap B') = 1 - P(A \cup B)$
> $P(A \cup B) = 0.3 + 0.6 - 0.15 = 0.75$
> $P(X+Y=0) = 1 - 0.75 = 0.25$
> $P(X+Y=1) = P(A \cap B') + P(A' \cap B) = (0.3-0.15) + (0.6-0.15) = 0.15 + 0.45 = 0.60$
> $P(X+Y=2) = P(A \cap B) = 0.15$
> $E[X+Y] = 0(0.25) + 1(0.60) + 2(0.15) = 0.9 = E[X]+E[Y]$ ✅
> $E[(X+Y)^2] = 0^2(0.25) + 1^2(0.60) + 2^2(0.15) = 0.6 + 0.6 = 1.2$
> $\text{Var}(X+Y) = 1.2 - (0.9)^2 = 1.2 - 0.81 = 0.39$ ✅

---

#### Problem MIX2: From Covariance to Conditional Expectation

Given joint distribution:
| X\Y | 0 | 2 |
|---|---|---|
| 1 | 0.1 | 0.3 |
| 2 | 0.2 | 0.4 |

a) Find $E[X \mid Y=0]$, $E[X \mid Y=2]$, and verify LTE
b) Find $\text{Var}(X \mid Y=0)$, $\text{Var}(X \mid Y=2)$
c) Find $\text{Cov}(X,Y)$ and verify LTV

> [!success]- Solution (with theory)
>
> **Concept — Connecting covariance and conditional expectation:**
>
> The Law of Total Expectation (LTE) and Law of Total Variance (LTV) are linked:
> - $E[X] = E[E[X \mid Y]]$ — unconditional mean = weighted average of conditional means
> - $\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$ — total = within + between
>
> Covariance tells us whether knowing Y helps predict X. If $\text{Cov}(X,Y) \neq 0$, then $E[X \mid Y=y]$ depends on y.
>
> ---
>
> a) $P(Y=0) = 0.1+0.2 = 0.3$, $P(Y=2) = 0.3+0.4 = 0.7$
> $E[X \mid Y=0] = 1(0.1/0.3) + 2(0.2/0.3) = 1(1/3) + 2(2/3) = 5/3$
> $E[X \mid Y=2] = 1(0.3/0.7) + 2(0.4/0.7) = 1(3/7) + 2(4/7) = 11/7$
> **LTE:** $E[X] = E[E[X \mid Y]] = (5/3)(0.3) + (11/7)(0.7) = 0.5 + 1.1 = 1.6$
> Direct: $E[X] = 1(0.4) + 2(0.6) = 1.6$ ✅
>
> b) $E[X^2 \mid Y=0] = 1(1/3) + 4(2/3) = 9/3 = 3$
> $\text{Var}(X \mid Y=0) = 3 - (5/3)^2 = 3 - 25/9 = 27/9 - 25/9 = 2/9$
> $E[X^2 \mid Y=2] = 1(3/7) + 4(4/7) = (3+16)/7 = 19/7$
> $\text{Var}(X \mid Y=2) = 19/7 - (11/7)^2 = 19/7 - 121/49 = 133/49 - 121/49 = 12/49$
>
> c) $E[X] = 1.6$, $E[Y] = 0(0.3) + 2(0.7) = 1.4$
> $E[XY] = 1(0)(0.1) + 1(2)(0.3) + 2(0)(0.2) + 2(2)(0.4) = 0 + 0.6 + 0 + 1.6 = 2.2$
> $\text{Cov}(X,Y) = 2.2 - (1.6)(1.4) = 2.2 - 2.24 = -0.04$
>
> **LTV verification:**
> $E[\text{Var}(X \mid Y)] = (2/9)(0.3) + (12/49)(0.7) = 0.0667 + 0.1714 = 0.2381$
> $E[X \mid Y]$ = {5/3, 11/7} with probs {0.3, 0.7}
> $\text{Var}(E[X \mid Y]) = E[(E[X \mid Y])^2] - (E[X])^2$
> $= (25/9)(0.3) + (121/49)(0.7) - (1.6)^2$
> $= 0.8333 + 1.7286 - 2.56 = 0.0019$
> $\text{Var}(X)$ direct: $E[X^2] = 1(0.4) + 4(0.6) = 2.8$
> $\text{Var}(X) = 2.8 - (1.6)^2 = 2.8 - 2.56 = 0.24$
> LTV: $0.2381 + 0.0019 = 0.24$ ✅
>
> **Note:** The between-group variance is tiny (0.0019/0.24 ≈ 0.8%) — knowing Y barely helps explain X. This matches $\text{Cov}(X,Y) \approx -0.04$, a very weak relationship.

---

#### Problem MIX3: Covariance of Independent Variables

Prove: If X and Y are independent, $\text{Cov}(X, Y) = 0$. Is the converse true? Provide a counterexample.

> [!success]- Solution
> **Forward direction ($\Rightarrow$):**
> If X and Y are independent: $E[XY] = E[X]E[Y]$
> Therefore: $\text{Cov}(X,Y) = E[XY] - E[X]E[Y] = E[X]E[Y] - E[X]E[Y] = 0$
>
> **Converse ($\Leftarrow$) is FALSE:**
> Cov = 0 does NOT imply independence.
>
> **Counterexample:**
> Let $X \in \{-1, 0, 1\}$ with equal prob $1/3$. Let $Y = X^2$.
> $E[X] = (-1 + 0 + 1)/3 = 0$
> $E[Y] = (1 + 0 + 1)/3 = 2/3$
> $E[XY] = E[X \cdot X^2] = E[X^3] = (-1 + 0 + 1)/3 = 0$
> $\text{Cov}(X,Y) = 0 - 0(2/3) = 0$
>
> Yet $Y = X^2$ — they are deterministically related, clearly not independent.
>
> **Why?** Covariance only captures **linear** relationships. Non-linear relationships (like quadratic) can have zero covariance.

---

#### Problem MIX4: All of Variance in One Problem

Let X have PMF: $P(X = -2) = 0.1$, $P(X = -1) = 0.2$, $P(X = 0) = 0.3$, $P(X = 1) = 0.3$, $P(X = 2) = 0.1$

a) Find $E[X]$, $E[X^2]$, $\text{Var}(X)$
b) Let $Y = X^2$. Find $\text{Cov}(X, Y)$
c) Find $\text{Var}(X + Y)$
d) Find $E[Y \mid X \geq 0]$ and $\text{Var}(Y \mid X \geq 0)$

> [!success]- Solution (with theory)
>
> **Concept — Integrating all concepts: variance, covariance of non-linear transforms, conditional variance.**
>
> Key observations:
> - $Y = X^2$ creates a U-shaped relationship with X — symmetric X values map to the same Y
> - $\text{Cov}(X, X^2)$ can be zero even with strong dependence (symmetric distribution → $E[X^3] = 0$)
> - Conditional variance still uses the shortcut formula, just applied to the restricted subset
>
> ---
>
> a) $E[X] = -2(0.1) - 1(0.2) + 0(0.3) + 1(0.3) + 2(0.1) = -0.2 - 0.2 + 0 + 0.3 + 0.2 = 0.1$
> $E[X^2] = 4(0.1) + 1(0.2) + 0(0.3) + 1(0.3) + 4(0.1) = 0.4 + 0.2 + 0 + 0.3 + 0.4 = 1.3$
> $\text{Var}(X) = 1.3 - (0.1)^2 = 1.3 - 0.01 = 1.29$
>
> b) $Y = X^2$ takes values {4, 1, 0, 1, 4}
> $E[Y] = E[X^2] = 1.3$
> $E[XY] = E[X \cdot X^2] = E[X^3] = (-8)(0.1) + (-1)(0.2) + 0(0.3) + 1(0.3) + 8(0.1)$
> $= -0.8 - 0.2 + 0 + 0.3 + 0.8 = 0.1$
> $\text{Cov}(X,Y) = 0.1 - (0.1)(1.3) = 0.1 - 0.13 = -0.03$
>
> **Note:** $\text{Cov}(X, X^2)$ is near zero because the distribution is nearly symmetric. This illustrates how covariance misses non-linear relationships.
>
> c) $\text{Var}(X+Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y)$
> $E[Y^2] = E[X^4] = 16(0.1) + 1(0.2) + 0(0.3) + 1(0.3) + 16(0.1) = 1.6 + 0.2 + 0 + 0.3 + 1.6 = 3.7$
> $\text{Var}(Y) = 3.7 - (1.3)^2 = 3.7 - 1.69 = 2.01$
> $\text{Var}(X+Y) = 1.29 + 2.01 + 2(-0.03) = 3.30 - 0.06 = 3.24$
>
> d) $P(X \geq 0) = 0.3 + 0.3 + 0.1 = 0.7$
> Conditional: $X \in \{0, 1, 2\}$, $Y = X^2 \in \{0, 1, 4\}$
> $P(Y=0 \mid X \geq 0) = 0.3/0.7 = 3/7$
> $P(Y=1 \mid X \geq 0) = 0.3/0.7 = 3/7$
> $P(Y=4 \mid X \geq 0) = 0.1/0.7 = 1/7$
> $E[Y \mid X \geq 0] = 0(3/7) + 1(3/7) + 4(1/7) = 7/7 = 1$
> $E[Y^2 \mid X \geq 0] = 0(3/7) + 1(3/7) + 16(1/7) = 19/7$
> $\text{Var}(Y \mid X \geq 0) = 19/7 - 1^2 = 19/7 - 7/7 = 12/7 \approx 1.714$
>
> **Note:** The conditional variance (1.714) is slightly less than unconditional (2.01) — restricting to non-negative values removes some spread.

---

#### Problem MIX5: GATE-Style Multi-Concept

Two random variables have joint distribution:
$$P(X = x, Y = y) = \frac{x + y}{30}, \quad x = 1, 2, 3,\; y = 1, 2$$

a) Find the joint table and marginal distributions
b) Find $E[X]$, $E[Y]$, $\text{Var}(X)$, $\text{Var}(Y)$
c) Find $\text{Cov}(X,Y)$ and $\rho_{XY}$
d) Find $E[X \mid Y = 1]$ and $\text{Var}(X \mid Y = 1)$
e) Verify LTV for $\text{Var}(X)$

> [!success]- Solution (with theory)
>
> **Concept — GATE-style problems test all concepts at once:**
>
> This problem integrates: joint tables, marginalization, expectation, variance, covariance, conditional expectation, conditional variance, and the Law of Total Variance. Each part builds on the previous.
>
> The key insight for LTV verification: the within + between decomposition must exactly equal the directly computed Var(X). This is a powerful consistency check.
>
> ---
>
> a) **Joint table** ($P = (x+y)/30$):
> | X\Y | 1 | 2 | P(X=x) |
> |---|---|---|--------|
> | 1 | 2/30 | 3/30 | 5/30 |
> | 2 | 3/30 | 4/30 | 7/30 |
> | 3 | 4/30 | 5/30 | 9/30 |
> | P(Y=y) | 9/30 | 12/30 | 1 |
>
> Simplifying: $P(X=1)=1/6$, $P(X=2)=7/30$, $P(X=3)=3/10$
> $P(Y=1)=3/10$, $P(Y=2)=2/5$
>
> b) $E[X] = 1(1/6) + 2(7/30) + 3(3/10) = 1/6 + 14/30 + 9/10$
> $= 5/30 + 14/30 + 27/30 = 46/30 = 23/15$
> $E[X^2] = 1(1/6) + 4(7/30) + 9(3/10) = 1/6 + 28/30 + 27/10$
> $= 5/30 + 28/30 + 81/30 = 114/30 = 19/5$
> $\text{Var}(X) = 19/5 - (23/15)^2 = 19/5 - 529/225 = 855/225 - 529/225 = 326/225$
>
> $E[Y] = 1(3/10) + 2(2/5) = 3/10 + 4/5 = 3/10 + 8/10 = 11/10$
> $E[Y^2] = 1(3/10) + 4(2/5) = 3/10 + 8/5 = 3/10 + 16/10 = 19/10$
> $\text{Var}(Y) = 19/10 - (11/10)^2 = 19/10 - 121/100 = 190/100 - 121/100 = 69/100$
>
> c) $E[XY] = \sum\sum xy \cdot P(x,y)$
> $= 1(1)(2/30) + 1(2)(3/30) + 2(1)(3/30) + 2(2)(4/30) + 3(1)(4/30) + 3(2)(5/30)$
> $= (2 + 6 + 6 + 16 + 12 + 30)/30 = 72/30 = 12/5$
>
> $\text{Cov}(X,Y) = 12/5 - (23/15)(11/10) = 12/5 - 253/150 = 360/150 - 253/150 = 107/150$
> $\sigma_X = \sqrt{326/225} \approx 1.203$, $\sigma_Y = \sqrt{69/100} \approx 0.831$
> $\rho_{XY} = (107/150) / (\sqrt{326/225}\sqrt{69/100}) \approx 0.713$
>
> **Interpretation:** $\rho \approx 0.713$ is a strong positive correlation. X and Y are jointly determined by $(x+y)/30$ — larger X values tend to pair with larger Y values.
>
> d) $P(Y=1) = 9/30 = 3/10$
> $P(X=1 \mid Y=1) = (2/30)/(9/30) = 2/9$
> $P(X=2 \mid Y=1) = (3/30)/(9/30) = 3/9 = 1/3$
> $P(X=3 \mid Y=1) = (4/30)/(9/30) = 4/9$
> $E[X \mid Y=1] = 1(2/9) + 2(3/9) + 3(4/9) = (2+6+12)/9 = 20/9$
> $E[X^2 \mid Y=1] = 1(2/9) + 4(3/9) + 9(4/9) = (2+12+36)/9 = 50/9$
> $\text{Var}(X \mid Y=1) = 50/9 - (20/9)^2 = 50/9 - 400/81 = 450/81 - 400/81 = 50/81$
>
> e) **LTV for Var(X):**
> $P(Y=2) = 12/30 = 2/5$
> $P(X=1 \mid Y=2) = (3/30)/(12/30) = 1/4$
> $P(X=2 \mid Y=2) = (4/30)/(12/30) = 1/3$
> $P(X=3 \mid Y=2) = (5/30)/(12/30) = 5/12$
> $E[X \mid Y=2] = 1(1/4) + 2(1/3) + 3(5/12) = 3/12 + 8/12 + 15/12 = 26/12 = 13/6$
> $E[X^2 \mid Y=2] = 1(1/4) + 4(1/3) + 9(5/12) = 3/12 + 16/12 + 45/12 = 64/12 = 16/3$
> $\text{Var}(X \mid Y=2) = 16/3 - (13/6)^2 = 16/3 - 169/36 = 192/36 - 169/36 = 23/36$
>
> $E[\text{Var}(X \mid Y)] = (50/81)(3/10) + (23/36)(2/5) = 150/810 + 46/180 = 5/27 + 23/90$
> $= (50 + 69)/270 = 119/270$
>
> $E[X \mid Y]$ = {20/9, 13/6} with probs {3/10, 2/5}
> $E[(E[X \mid Y])^2] = (20/9)^2(3/10) + (13/6)^2(2/5)$
> $= (400/81)(3/10) + (169/36)(2/5)$
> $= 1200/810 + 338/180 = 40/27 + 169/90$
> $= (400 + 507)/270 = 907/270$
> $\text{Var}(E[X \mid Y]) = 907/270 - (23/15)^2 = 907/270 - 529/225$
> $= 907/270 - 1058/450 = (4535 - 3174)/1350 = 1361/1350$
>
> LTV: $119/270 + 1361/1350 = (595 + 1361)/1350 = 1956/1350 = 326/225$ ✅
> Matches $\text{Var}(X) = 326/225$ from part (b). LTV verified — the decomposition is exact.

---

## Quick Reference

| Formula | When to Use |
|---------|------------|
| $\text{Var}(X) = E[X^2] - (E[X])^2$ | Always (shortcut) |
| $\text{Var}(aX + b) = a^2\text{Var}(X)$ | Linear transformations |
| $\text{Var}(X \mid B) = E[X^2 \mid B] - (E[X \mid B])^2$ | Conditional variance |
| $\text{Var}(X) = E[\text{Var}(X \mid Y)] + \text{Var}(E[X \mid Y])$ | Decomposing variance |
| $\text{Cov}(X,Y) = E[XY] - E[X]E[Y]$ | Shortcut for covariance |
| $\text{Cov}(aX+bY, cZ+dW) = ac\,\text{Cov}(X,Z) + ...$ | Bilinearity |
| $\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X,Y)$ | Variance of sum |
| $\rho = \frac{\text{Cov}(X,Y)}{\sigma_X\sigma_Y}$ | Unitless correlation |
| $-1 \leq \rho \leq 1$ | Cauchy-Schwarz bound |

---

Say **"done session-002b"** when you've worked through these. Next up: **Session 003 — Random Variables & Probability Distributions**.
