# Foundational Practice: Poisson & Exponential Distributions

This practice sheet is designed to build your core mechanics. Work through these step-by-step. All solutions are hidden inside dropdowns; try solving each question on paper before expanding the solution.

---

## 📋 The 6 Foundational Formulas

1. **Poisson PMF**: 
   $$P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!} \quad \text{for } k = 0, 1, 2, \dots$$
2. **Poisson Time-Interval Scaling**: 
   $$P(X = k \text{ in window } t) = \frac{e^{-\lambda t} (\lambda t)^k}{k!}$$
3. **Poisson Mean & Variance**: 
   $$E[X] = \lambda \quad \text{and} \quad \text{Var}(X) = \lambda$$
4. **Exponential Survival Function**: 
   $$P(T > t) = e^{-\lambda t}$$
5. **Exponential CDF**: 
   $$F(t) = P(T \le t) = 1 - e^{-\lambda t}$$
6. **Exponential PDF**: 
   $$f(t) = \lambda e^{-\lambda t} \quad \text{for } t \ge 0$$

---

## 📝 Warm-up & Foundational Questions

### Question 1: Direct Poisson PMF
A random variable $X$ follows a Poisson distribution with parameter $\lambda = 2$. Find the exact probability that $X = 3$.

> [!success]- Click to view Solution
> **Step 1: Identify the formula.**
> We use the standard Poisson PMF (Formula 1):
> $$P(X = k) = \frac{e^{-\lambda} \lambda^k}{k!}$$
> 
> **Step 2: Plug in the values.**
> We are given $\lambda = 2$ and we want to find the probability for $k = 3$:
> $$P(X = 3) = \frac{e^{-2} \cdot 2^3}{3!}$$
> 
> **Step 3: Simplify.**
> * $2^3 = 8$
> * $3! = 3 \times 2 \times 1 = 6$
> 
> $$P(X = 3) = \frac{8 e^{-2}}{6} = \frac{4}{3} e^{-2}$$
> 
> Using $e^{-2} \approx 0.1353$:
> $$P(X = 3) \approx 1.333 \times 0.1353 \approx 0.1804 \text{ (or } 18.04\%)$$
> 
> **Answer:** $\frac{4}{3} e^{-2} \approx 0.1804$

---

### Question 2: Poisson Mean and Variance
For a Poisson random variable $X$, we know that $\text{Var}(X) = 5$. Find:
1. The mean $E[X]$.
2. The probability that $X = 0$.

> [!success]- Click to view Solution
> **Step 1: Relate Variance to the parameter $\lambda$.**
> According to Formula 3, for any Poisson random variable:
> $$\text{Var}(X) = \lambda$$
> Since we are given $\text{Var}(X) = 5$, we have:
> $$\lambda = 5$$
> 
> **Step 2: Find the mean.**
> Also by Formula 3, the mean is equal to $\lambda$:
> $$E[X] = \lambda = 5$$
> 
> **Step 3: Find $P(X = 0)$.**
> Using Formula 1 with $\lambda = 5$ and $k = 0$:
> $$P(X = 0) = \frac{e^{-5} \cdot 5^0}{0!} = \frac{e^{-5} \cdot 1}{1} = e^{-5}$$
> 
> Using $e^{-5} \approx 0.0067$:
> $$P(X = 0) \approx 0.0067 \text{ (or } 0.67\%)$$
> 
> **Answer:** $E[X] = 5$ and $P(X = 0) = e^{-5} \approx 0.0067$

---

### Question 3: Time-Interval Scaling
A customer service hotline receives on average 12 calls per hour. Assuming the calls arrive according to a Poisson process, what is the probability of receiving exactly 2 calls in a given 10-minute window?

> [!success]- Click to view Solution
> **Step 1: Identify the base rate and the time window.**
> * Base rate: $\lambda_{\text{base}} = 12 \text{ calls/hour}$
> * Time window: $t = 10 \text{ minutes} = \frac{10}{60} \text{ hours} = \frac{1}{6} \text{ hours}$
> 
> **Step 2: Scale the rate parameter to the window.**
> Using Formula 2, the scaled parameter for our window is:
> $$\lambda_{\text{scaled}} = \lambda_{\text{base}} \times t = 12 \times \frac{1}{6} = 2 \text{ calls per 10 minutes}$$
> 
> **Step 3: Calculate the probability.**
> Now we find $P(X = 2)$ using the scaled rate $\lambda = 2$:
> $$P(X = 2) = \frac{e^{-2} \cdot 2^2}{2!} = \frac{e^{-2} \cdot 4}{2} = 2 e^{-2}$$
> 
> Using $e^{-2} \approx 0.1353$:
> $$P(X = 2) \approx 2 \times 0.1353 = 0.2706 \text{ (or } 27.06\%)$$
> 
> **Answer:** $2 e^{-2} \approx 0.2706$

---

### Question 4: Exponential Survival Function
The lifetime $T$ (in hours) of a LED lightbulb is exponentially distributed with a mean lifetime of 1000 hours. What is the probability that a randomly selected bulb lasts for more than 1500 hours?

> [!success]- Click to view Solution
> **Step 1: Find the rate parameter $\lambda$.**
> For an Exponential distribution, the mean is related to the rate parameter by:
> $$E[T] = \frac{1}{\lambda}$$
> We are given $E[T] = 1000$ hours. Therefore:
> $$\lambda = \frac{1}{1000} = 0.001 \text{ failures per hour}$$
> 
> **Step 2: Identify the correct formula.**
> We want the probability of surviving past $t = 1500$ hours, i.e., $P(T > 1500)$. We use the Survival Function (Formula 4):
> $$P(T > t) = e^{-\lambda t}$$
> 
> **Step 3: Plug in the values.**
> $$P(T > 1500) = e^{-0.001 \times 1500} = e^{-1.5}$$
> 
> Using $e^{-1.5} \approx 0.2231$:
> $$P(T > 1500) \approx 0.2231 \text{ (or } 22.31\%)$$
> 
> **Answer:** $e^{-1.5} \approx 0.2231$

---

### Question 5: Exponential CDF
A bank teller is free, and the waiting time $T$ (in minutes) for the next customer to arrive is exponentially distributed with a rate parameter of $\lambda = 0.4$ arrivals per minute. What is the probability that a customer arrives within the next 5 minutes?

> [!success]- Click to view Solution
> **Step 1: Identify the question.**
> "Within the next 5 minutes" means the waiting time $T$ is less than or equal to 5 ($T \le 5$). 
> 
> **Step 2: Select the correct formula.**
> We use the Exponential CDF (Formula 5):
> $$F(t) = P(T \le t) = 1 - e^{-\lambda t}$$
> 
> **Step 3: Plug in the values.**
> Here, $\lambda = 0.4$ and $t = 5$:
> $$P(T \le 5) = 1 - e^{-0.4 \times 5} = 1 - e^{-2}$$
> 
> Using $e^{-2} \approx 0.1353$:
> $$P(T \le 5) \approx 1 - 0.1353 = 0.8647 \text{ (or } 86.47\%)$$
> 
> **Answer:** $1 - e^{-2} \approx 0.8647$

---

### Question 6: Identifying Parameters from PDF
The probability density function (PDF) of a continuous random variable $T$ is given by:
$$f(t) = 0.5 e^{-0.5 t} \quad \text{for } t \ge 0$$
Find:
1. The rate parameter $\lambda$.
2. The mean $E[T]$.
3. The variance $\text{Var}(T)$.

> [!success]- Click to view Solution
> **Step 1: Match the PDF to the standard formula.**
> The standard Exponential PDF (Formula 6) is:
> $$f(t) = \lambda e^{-\lambda t}$$
> By directly matching the given $f(t) = 0.5 e^{-0.5 t}$, we see that:
> $$\lambda = 0.5$$
> 
> **Step 2: Calculate the mean.**
> The mean of an Exponential distribution is:
> $$E[T] = \frac{1}{\lambda} = \frac{1}{0.5} = 2$$
> 
> **Step 3: Calculate the variance.**
> The variance of an Exponential distribution is:
> $$\text{Var}(T) = \frac{1}{\lambda^2} = \frac{1}{(0.5)^2} = \frac{1}{0.25} = 4$$
> 
> **Answer:** $\lambda = 0.5$, $E[T] = 2$, and $\text{Var}(T) = 4$

---

### Question 7: Poisson Complement Rule
A small bakery bakes on average 4 cakes per hour. Assuming a Poisson process, what is the probability that they sell **at least 1** cake in a 30-minute window?

> [!success]- Click to view Solution
> **Step 1: Identify the rate and time.**
> * $\lambda_{\text{base}} = 4 \text{ cakes/hour}$
> * $t = 30 \text{ minutes} = 0.5 \text{ hours}$
> 
> **Step 2: Scale the rate.**
> $$\lambda_{\text{scaled}} = 4 \times 0.5 = 2 \text{ cakes per 30 minutes}$$
> 
> **Step 3: Apply the complement rule.**
> "At least 1" means $X \ge 1$. The complement of "at least 1" is "exactly 0" ($X = 0$).
> $$P(X \ge 1) = 1 - P(X = 0)$$
> 
> **Step 4: Calculate.**
> $$P(X = 0) = \frac{e^{-2} \cdot 2^0}{0!} = e^{-2}$$
> $$P(X \ge 1) = 1 - e^{-2} \approx 1 - 0.1353 = 0.8647$$
> 
> **Answer:** $1 - e^{-2} \approx 0.8647$

---

### Question 8: Probability in an Interval
A laptop battery's lifetime $T$ (in hours) is exponentially distributed with a mean of 8 hours. What is the probability that the battery fails between 6 and 10 hours of use?

> [!success]- Click to view Solution
> **Step 1: Find the rate parameter $\lambda$.**
> $$E[T] = \frac{1}{\lambda} = 8 \implies \lambda = \frac{1}{8} = 0.125 \text{ failures per hour}$$
> 
> **Step 2: Set up the interval probability.**
> We want to find $P(6 \le T \le 10)$. Using the CDF:
> $$P(6 \le T \le 10) = F(10) - F(6)$$
> 
> **Step 3: Substitute the CDF formula.**
> $$F(10) = 1 - e^{-10 \lambda} = 1 - e^{-10/8} = 1 - e^{-1.25}$$
> $$F(6) = 1 - e^{-6 \lambda} = 1 - e^{-6/8} = 1 - e^{-0.75}$$
> 
> Subtracting the two:
> $$P(6 \le T \le 10) = (1 - e^{-1.25}) - (1 - e^{-0.75}) = e^{-0.75} - e^{-1.25}$$
> 
> **Step 4: Calculate numerical values.**
> * $e^{-0.75} \approx 0.4724$
> * $e^{-1.25} \approx 0.2865$
> 
> $$P(6 \le T \le 10) \approx 0.4724 - 0.2865 = 0.1859 \text{ (or } 18.59\%)$$
> 
> **Answer:** $e^{-0.75} - e^{-1.25} \approx 0.1859$

---

### Question 9: Algebraic Equation of PMF
For a Poisson random variable $X$, it is known that $P(X = 1) = P(X = 2)$. Find the expected value $E[X]$.

> [!success]- Click to view Solution
> **Step 1: Write down the equations for both probabilities.**
> Using Formula 1:
> $$P(X = 1) = \frac{e^{-\lambda} \lambda^1}{1!} = \lambda e^{-\lambda}$$
> $$P(X = 2) = \frac{e^{-\lambda} \lambda^2}{2!} = \frac{\lambda^2 e^{-\lambda}}{2}$$
> 
> **Step 2: Set them equal to each other.**
> $$\lambda e^{-\lambda} = \frac{\lambda^2 e^{-\lambda}}{2}$$
> 
> **Step 3: Solve for $\lambda$.**
> Since $e^{-\lambda} > 0$, we can divide both sides by $e^{-\lambda}$:
> $$\lambda = \frac{\lambda^2}{2}$$
> 
> Since $\lambda > 0$ for a non-trivial Poisson distribution, divide both sides by $\lambda$:
> $$1 = \frac{\lambda}{2} \implies \lambda = 2$$
> 
> **Step 4: Find the expected value.**
> For a Poisson distribution, the expected value is $\lambda$:
> $$E[X] = \lambda = 2$$
> 
> **Answer:** $E[X] = 2$

---

### Question 10: Conceptual Check
A machine component's lifetime $T$ (in hours) is exponentially distributed with a PDF of $f(t) = 0.05 e^{-0.05 t}$. What is the probability that the component fails at **exactly** $T = 10$ hours?

> [!success]- Click to view Solution
> **The Answer is 0.**
> 
> **Why?**
> $T$ is a **continuous** random variable. For any continuous random variable, the probability of the variable taking on any single exact value is always zero:
> $$P(T = c) = 0 \quad \text{for any constant } c$$
> 
> A PDF (Probability Density Function) does not represent probability directly; it represents *density*. Probability is represented by the area under the PDF curve. The area under a single point (which has width $= 0$) is always zero:
> $$P(T = 10) = \int_{10}^{10} f(t) \, dt = 0$$
> 
> **Answer:** $0$

---

## 📈 Slightly More Advanced Questions

### Question 11: Exponential CDF Interval Probability
Let the continuous random variable $T$ represent the lifetime of a device, where $T \sim \text{Exp}(\lambda)$ with a mean lifetime of 4 years. What is the probability that the device fails between year 2 and year 6?

> [!success]- Click to view Solution
> **Step 1: Find the rate parameter $\lambda$.**
> We know the mean of an Exponential distribution is:
> $$E[T] = \frac{1}{\lambda} = 4 \implies \lambda = \frac{1}{4} = 0.25 \text{ failures per year}$$
> 
> **Step 2: Set up the interval probability.**
> We want to find $P(2 \le T \le 6)$. Using the CDF $F(t) = 1 - e^{-\lambda t}$:
> $$P(2 \le T \le 6) = F(6) - F(2)$$
> 
> **Step 3: Calculate using the CDF.**
> $$F(6) = 1 - e^{-6 \lambda} = 1 - e^{-6 \times 0.25} = 1 - e^{-1.5}$$
> $$F(2) = 1 - e^{-2 \lambda} = 1 - e^{-2 \times 0.25} = 1 - e^{-0.5}$$
> 
> Subtracting the two:
> $$P(2 \le T \le 6) = (1 - e^{-1.5}) - (1 - e^{-0.5}) = e^{-0.5} - e^{-1.5}$$
> 
> **Step 4: Calculate numerical values.**
> * $e^{-0.5} \approx 0.6065$
> * $e^{-1.5} \approx 0.2231$
> 
> $$P(2 \le T \le 6) \approx 0.6065 - 0.2231 = 0.3834 \text{ (or } 38.34\%)$$
> 
> **Answer:** $e^{-0.5} - e^{-1.5} \approx 0.3834$

---

### Question 12: Poisson Scaling with Fractional Rates
A web server receives on average 1.5 hits per minute. Assuming a Poisson process, what is the probability of receiving exactly 3 hits in a 4-minute window?

> [!success]- Click to view Solution
> **Step 1: Identify the base rate and the time window.**
> * Base rate: $\lambda_{\text{base}} = 1.5 \text{ hits/minute}$
> * Time window: $t = 4 \text{ minutes}$
> 
> **Step 2: Scale the rate parameter to the window.**
> Using Formula 2:
> $$\lambda_{\text{scaled}} = \lambda_{\text{base}} \times t = 1.5 \times 4 = 6 \text{ hits per 4 minutes}$$
> 
> **Step 3: Calculate the probability using the PMF.**
> Now find $P(X = 3)$ using the scaled rate $\lambda = 6$:
> $$P(X = 3) = \frac{e^{-6} \cdot 6^3}{3!}$$
> 
> **Step 4: Simplify.**
> * $6^3 = 216$
> * $3! = 6$
> 
> $$P(X = 3) = \frac{216 e^{-6}}{6} = 36 e^{-6}$$
> 
> Using $e^{-6} \approx 0.00248$:
> $$P(X = 3) \approx 36 \times 0.00248 \approx 0.0893 \text{ (or } 8.93\%)$$
> 
> **Answer:** $36 e^{-6} \approx 0.0893$

---

### Question 13: Direct Application of the Memoryless Property
A vacuum pump has an exponentially distributed lifetime with a mean of 5 years. If the pump has already survived for 3 years without failing, what is the conditional probability that it will survive for at least another 2 years?

> [!success]- Click to view Solution
> **Step 1: Define the random variable and parameters.**
> Let $T$ be the lifetime of the pump. $T \sim \text{Exp}(\lambda)$ with mean $E[T] = 5 \implies \lambda = \frac{1}{5} = 0.2$ per year.
> 
> **Step 2: Identify the conditional probability.**
> We are given that it survived 3 years ($T > 3$). We want to find the probability that it survives for at least another 2 years, meaning total lifetime $T > 3 + 2 = 5$.
> $$P(T > 5 \mid T > 3)$$
> 
> **Step 3: Apply the Memoryless Property.**
> For any Exponential random variable:
> $$P(T > s + t \mid T > s) = P(T > t)$$
> Here, $s = 3$ and $t = 2$:
> $$P(T > 3 + 2 \mid T > 3) = P(T > 2)$$
> 
> **Step 4: Calculate the survival probability.**
> Using Formula 4:
> $$P(T > 2) = e^{-2 \lambda} = e^{-2 \times 0.2} = e^{-0.4}$$
> 
> Using $e^{-0.4} \approx 0.6703$:
> $$P(T > 5 \mid T > 3) \approx 0.6703 \text{ (or } 67.03\%)$$
> 
> **Answer:** $e^{-0.4} \approx 0.6703$

---

### Question 14: Poisson Variance and Moments
For a Poisson random variable $X$, the second moment is $E[X^2] = 12$. Find:
1. The mean $E[X]$.
2. The probability $P(X = 1)$.

> [!success]- Click to view Solution
> **Step 1: Relate the second moment to the parameter $\lambda$.**
> We know that:
> $$\text{Var}(X) = E[X^2] - (E[X])^2$$
> For a Poisson distribution, $E[X] = \lambda$ and $\text{Var}(X) = \lambda$. Substituting these:
> $$\lambda = E[X^2] - \lambda^2$$
> 
> **Step 2: Solve the quadratic equation.**
> Given $E[X^2] = 12$:
> $$\lambda = 12 - \lambda^2 \implies \lambda^2 + \lambda - 12 = 0$$
> Factor the quadratic equation:
> $$(\lambda + 4)(\lambda - 3) = 0$$
> Since the rate parameter must be positive ($\lambda > 0$), we choose:
> $$\lambda = 3$$
> 
> **Step 3: Find the mean.**
> $$E[X] = \lambda = 3$$
> 
> **Step 4: Find $P(X = 1)$.**
> Using Formula 1 with $\lambda = 3$ and $k = 1$:
> $$P(X = 1) = \frac{e^{-3} \cdot 3^1}{1!} = 3 e^{-3}$$
> 
> Using $e^{-3} \approx 0.0498$:
> $$P(X = 1) \approx 3 \times 0.0498 \approx 0.1494 \text{ (or } 14.94\%)$$
> 
> **Answer:** $E[X] = 3$ and $P(X = 1) = 3 e^{-3} \approx 0.1494$

---

### Question 15: Exponential PDF Integration
Let $T$ be an Exponential random variable with rate parameter $\lambda = 0.2$. Write down the definite integral representing the CDF at $t = 4$, $F(4) = P(T \le 4)$, and evaluate it to find the exact probability.

> [!success]- Click to view Solution
> **Step 1: Set up the integral using the PDF.**
> The PDF of $T$ is $f(t) = \lambda e^{-\lambda t} = 0.2 e^{-0.2 t}$ for $t \ge 0$.
> The probability $P(T \le 4)$ is the area under the PDF from $0$ to $4$:
> $$P(T \le 4) = \int_{0}^{4} 0.2 e^{-0.2 t} \, dt$$
> 
> **Step 2: Integrate.**
> Recall that the antiderivative of $e^{cx}$ is $\frac{1}{c} e^{cx}$:
> $$\int 0.2 e^{-0.2 t} \, dt = 0.2 \left( \frac{e^{-0.2 t}}{-0.2} \right) = -e^{-0.2 t}$$
> 
> **Step 3: Evaluate at the boundaries.**
> $$P(T \le 4) = \left[ -e^{-0.2 t} \right]_{0}^{4} = -e^{-0.2 \times 4} - (-e^{-0.2 \times 0})$$
> $$P(T \le 4) = -e^{-0.8} + e^0 = 1 - e^{-0.8}$$
> 
> Using $e^{-0.8} \approx 0.4493$:
> $$P(T \le 4) \approx 1 - 0.4493 = 0.5507 \text{ (or } 55.07\%)$$
> 
> **Answer:** $\int_{0}^{4} 0.2 e^{-0.2 t} \, dt = 1 - e^{-0.8} \approx 0.5507$

---

### Question 16: Poisson Scaling and Complement
A busy intersection averages 3 traffic incidents every 10 minutes. Under a Poisson process model:
1. What is the expected number of incidents in a 20-minute window?
2. What is the probability of having **at least 2** traffic incidents in a 20-minute window?

> [!success]- Click to view Solution
> **Step 1: Scale the rate parameter.**
> * Base window: 10 minutes, with average count $= 3$.
> * New window: 20 minutes ($t = 2$ times the base window).
> * Scaled parameter: $\lambda = 3 \times 2 = 6$ incidents per 20 minutes.
> 
> **Step 2: Set up the complement rule.**
> We want the probability of "at least 2" incidents, which is $P(X \ge 2)$.
> The complement of $X \ge 2$ is $X < 2$, which means $X = 0$ or $X = 1$:
> $$P(X \ge 2) = 1 - P(X < 2) = 1 - [P(X = 0) + P(X = 1)]$$
> 
> **Step 3: Calculate individual probabilities.**
> Using $\lambda = 6$:
> $$P(X = 0) = \frac{e^{-6} \cdot 6^0}{0!} = e^{-6}$$
> $$P(X = 1) = \frac{e^{-6} \cdot 6^1}{1!} = 6e^{-6}$$
> 
> Adding them:
> $$P(X < 2) = e^{-6} + 6e^{-6} = 7e^{-6}$$
> 
> **Step 4: Subtract from 1.**
> $$P(X \ge 2) = 1 - 7e^{-6}$$
> 
> Using $e^{-6} \approx 0.00248$:
> $$P(X \ge 2) \approx 1 - 7(0.00248) = 1 - 0.01736 = 0.98264 \text{ (or } 98.26\%)$$
> 
> **Answer:** $1 - 7e^{-6} \approx 0.9826$

---

### Question 17: Poisson Independent Windows (Joint Probability)
A customer service desk receives an average of 4 queries per hour. Assuming a Poisson process:
1. What is the probability of receiving exactly 1 query in the first 30 minutes?
2. What is the probability of receiving exactly 1 query in the first 30 minutes **and** exactly 2 queries in the next 30 minutes?

> [!success]- Click to view Solution
> **Step 1: Understand the independent increments property of a Poisson process.**
> A key property of a Poisson process is that the number of events occurring in non-overlapping (disjoint) time intervals are independent of each other. 
> * The first interval is $I_1 = [0, 30 \text{ minutes}]$.
> * The second interval is $I_2 = [30 \text{ minutes}, 60 \text{ minutes}]$.
> These two intervals do not overlap. Therefore, the counts of queries in these two intervals are independent.
> 
> **Step 2: Scale the rate parameter for a 30-minute window.**
> * Base rate: $\lambda_{\text{base}} = 4 \text{ queries/hour}$
> * Time window: $t = 30 \text{ minutes} = 0.5 \text{ hours}$
> * Scaled parameter: $\lambda = 4 \times 0.5 = 2 \text{ queries per 30 minutes}$
> 
> **Step 3: Solve part 1.**
> Find $P(X_1 = 1)$ for the first 30-minute window:
> $$P(X_1 = 1) = \frac{e^{-2} \cdot 2^1}{1!} = 2e^{-2} \approx 2 \times 0.1353 = 0.2706$$
> 
> **Step 4: Solve part 2.**
> Let $X_1$ be the number of queries in the first 30 minutes, and $X_2$ be the number of queries in the next 30 minutes. We want the joint probability:
> $$P(X_1 = 1 \cap X_2 = 2)$$
> Since $X_1$ and $X_2$ are independent:
> $$P(X_1 = 1 \cap X_2 = 2) = P(X_1 = 1) \cdot P(X_2 = 2)$$
> 
> We already calculated $P(X_1 = 1) = 2e^{-2}$. Let's calculate $P(X_2 = 2)$ (since the second interval is also 30 minutes, it has the same scaled rate $\lambda = 2$):
> $$P(X_2 = 2) = \frac{e^{-2} \cdot 2^2}{2!} = 2e^{-2}$$
> 
> Now multiply them:
> $$P(X_1 = 1 \cap X_2 = 2) = (2e^{-2}) \cdot (2e^{-2}) = 4e^{-4}$$
> 
> Using $e^{-4} \approx 0.0183$:
> $$P(X_1 = 1 \cap X_2 = 2) \approx 4 \times 0.0183 \approx 0.0732 \text{ (or } 7.32\%)$$
> 
> **Answer:** 1) $2e^{-2} \approx 0.2706$, 2) $4e^{-4} \approx 0.0732$

---

### Question 18: Finding the Median of an Exponential
For an Exponential random variable $T \sim \text{Exp}(\lambda)$:
1. Prove that the median lifetime $m$ (the point where $P(T \le m) = 0.5$) is given by $m = \frac{\ln(2)}{\lambda}$.
2. If the mean of $T$ is 10 hours, calculate its median.

> [!success]- Click to view Solution
> **Step 1: Set up the equation for the median.**
> The median $m$ is the value where the CDF equals $0.5$:
> $$F(m) = P(T \le m) = 0.5$$
> 
> **Step 2: Solve the proof.**
> Using Formula 5:
> $$1 - e^{-\lambda m} = 0.5$$
> $$e^{-\lambda m} = 0.5 = \frac{1}{2}$$
> Take the natural logarithm of both sides:
> $$-\lambda m = \ln\left(\frac{1}{2}\right) = -\ln(2)$$
> Divide both sides by $-\lambda$:
> $$m = \frac{\ln(2)}{\lambda} \quad \text{(Q.E.D.)}$$
> 
> **Step 3: Calculate the median when the mean is 10 hours.**
> The mean is $E[T] = \frac{1}{\lambda} = 10 \implies \lambda = 0.1$.
> Substitute $\lambda = 0.1$ into our proven formula:
> $$m = \frac{\ln(2)}{0.1} = 10 \ln(2)$$
> 
> Using $\ln(2) \approx 0.6931$:
> $$m \approx 10 \times 0.6931 = 6.931 \text{ hours}$$
> 
> **Answer:** 1) Proof completed, 2) $10\ln(2) \approx 6.931$ hours

---

### Question 19: Ratio of Poisson Probabilities
For a Poisson random variable $X$, the ratio of the probability of observing 4 events to the probability of observing 3 events is 2.
$$\frac{P(X = 4)}{P(X = 3)} = 2$$
Find the variance of $X$.

> [!success]- Click to view Solution
> **Step 1: Write out the formulas for the ratio.**
> Using Formula 1:
> $$P(X = 4) = \frac{e^{-\lambda} \lambda^4}{4!}$$
> $$P(X = 3) = \frac{e^{-\lambda} \lambda^3}{3!}$$
> 
> **Step 2: Divide the two expressions.**
> $$\frac{P(X = 4)}{P(X = 3)} = \frac{\frac{e^{-\lambda} \lambda^4}{4!}}{\frac{e^{-\lambda} \lambda^3}{3!}} = \frac{\lambda^4}{\lambda^3} \cdot \frac{3!}{4!}$$
> 
> Simplify the fraction:
> * $\frac{\lambda^4}{\lambda^3} = \lambda$
> * $\frac{3!}{4!} = \frac{3 \times 2 \times 1}{4 \times 3 \times 2 \times 1} = \frac{1}{4}$
> 
> $$\frac{P(X = 4)}{P(X = 3)} = \frac{\lambda}{4}$$
> 
> **Step 3: Solve for $\lambda$.**
> We are given that this ratio is equal to 2:
> $$\frac{\lambda}{4} = 2 \implies \lambda = 8$$
> 
> **Step 4: Find the variance.**
> For a Poisson distribution, the variance is $\lambda$ (Formula 3):
> $$\text{Var}(X) = \lambda = 8$$
> 
> **Answer:** $\text{Var}(X) = 8$

---

### Question 20: Conditional Survival (Word Problem)
A high-performance server backup drive has a lifetime $T$ (in years) that is exponentially distributed with a rate parameter of $\lambda = 0.1$ failures per year. If the drive is currently 10 years old and still working perfectly, what is the probability that it survives to at least 15 years?

> [!success]- Click to view Solution
> **Step 1: Set up the conditional probability.**
> We are given that the drive is 10 years old ($T > 10$). We want to find the probability that it survives to at least 15 years ($T > 15$).
> $$P(T > 15 \mid T > 10)$$
> 
> **Step 2: Apply the Memoryless Property.**
> Let $s = 10$ and the additional time be $t = 5$, making the total time $s + t = 15$.
> $$P(T > 10 + 5 \mid T > 10) = P(T > 5)$$
> 
> **Step 3: Calculate the survival probability for 5 years.**
> Using Formula 4 with $\lambda = 0.1$ and $t = 5$:
> $$P(T > 5) = e^{-0.1 \times 5} = e^{-0.5}$$
> 
> Using $e^{-0.5} \approx 0.6065$:
> $$P(T > 15 \mid T > 10) \approx 0.6065 \text{ (or } 60.65\%)$$
> 
> **Answer:** $e^{-0.5} \approx 0.6065$

---

### Question 21: Poisson Probability of Even Events (Algebraic Derivation)
Let $X \sim \text{Poisson}(\lambda)$. Write down the sum representing the probability that $X$ takes an even value, $P(X \text{ is even}) = P(X = 0) + P(X = 2) + P(X = 4) + \dots$. 
Show that:
$$P(X \text{ is even}) = \frac{1 + e^{-2\lambda}}{2}$$

*Hint: Use the Taylor series expansions for $e^\lambda$ and $e^{-\lambda}$.*

> [!success]- Click to view Solution
> **Step 1: Write the sum of even terms.**
> $$P(X \text{ is even}) = \sum_{k=0, 2, 4, \dots}^{\infty} \frac{e^{-\lambda} \lambda^k}{k!} = e^{-\lambda} \sum_{n=0}^{\infty} \frac{\lambda^{2n}}{(2n)!}$$
> 
> **Step 2: Use Taylor series expansions.**
> Recall the series expansions for $e^x$ and $e^{-x}$ evaluated at $x = \lambda$:
> 1) $e^\lambda = 1 + \lambda + \frac{\lambda^2}{2!} + \frac{\lambda^3}{3!} + \frac{\lambda^4}{4!} + \dots$
> 2) $e^{-\lambda} = 1 - \lambda + \frac{\lambda^2}{2!} - \frac{\lambda^3}{3!} + \frac{\lambda^4}{4!} - \dots$
> 
> **Step 3: Add the two series.**
> When you add $e^\lambda$ and $e^{-\lambda}$, the odd-powered terms cancel out, and the even-powered terms double:
> $$e^\lambda + e^{-\lambda} = 2 \left( 1 + \frac{\lambda^2}{2!} + \frac{\lambda^4}{4!} + \dots \right)$$
> $$e^\lambda + e^{-\lambda} = 2 \sum_{n=0}^{\infty} \frac{\lambda^{2n}}{(2n)!}$$
> 
> Divide both sides by 2:
> $$\sum_{n=0}^{\infty} \frac{\lambda^{2n}}{(2n)!} = \frac{e^\lambda + e^{-\lambda}}{2}$$
> 
> **Step 4: Substitute this back into our probability equation.**
> $$P(X \text{ is even}) = e^{-\lambda} \left( \frac{e^\lambda + e^{-\lambda}}{2} \right)$$
> Multiply the $e^{-\lambda}$ through:
> $$P(X \text{ is even}) = \frac{e^{-\lambda} \cdot e^\lambda + e^{-\lambda} \cdot e^{-\lambda}}{2} = \frac{e^0 + e^{-2\lambda}}{2} = \frac{1 + e^{-2\lambda}}{2}$$
> 
> **Answer:** Proof completed.
