# Route 1 — Bounding the Partial Quotients of $\log_2 3$

*Closing the Lyapunov gap via Diophantine approximation theory.*

---

## Abstract

The Collatz Lyapunov inequality, derived in the parent synthesis, takes the form

$$m_1 \;\leq\; \frac{C^{\prime}}{C_B} \cdot K^{\kappa}$$

where $\kappa = 13.3$ is Mignotte's effective exponent in the lower bound for linear forms in two logarithms. If $\kappa$ could be replaced by $1 + \varepsilon$ for any $\varepsilon > 0$, the inequality combined with the verification floor $m_1 > 2^{68}$ would close the Collatz conjecture. This document explains *why* improving $\kappa$ is equivalent to bounding the partial quotients of the continued fraction expansion of $\log_2 3$, recapitulates the known partial results, and identifies precisely what would need to be proven.

---

## 1. Setup Recap — Where $\log_2 3$ Enters

The cycle product equation for a non-trivial Collatz cycle of length $L$:

$$\prod_{i=1}^{L} \left( 3 + \frac{1}{m_i} \right) = 2^{K}.$$

Taking logarithms and dividing by $\ln 2$:

$$K - L \log_2 3 \;=\; \frac{1}{\ln 2} \sum_{i=1}^{L} \ln\!\left( 1 + \frac{1}{3 m_i} \right).$$

**Reading this equation.** The left side is the *rational approximation gap* — how far the rational number $K/L$ is from the irrational $\log_2 3$, scaled by $L$. The right side is a positive quantity controlled by how big the cycle elements $m_i$ are. The cycle condition forces these two quantities to match exactly. So:

> *Every Collatz cycle is a coincidence: a rational $K/L$ approximating $\log_2 3$ to a precision matched exactly by the +1 corrections accumulated along an orbit.*

This is why $\log_2 3$ is the central object. It is the **exchange rate** between the two prime worlds:

$$\log_2 3 \;=\; \frac{\ln 3}{\ln 2} \;\approx\; 1.5849625\ldots$$

Every multiplicative balance between powers of 2 and powers of 3 reduces to a question about how this number sits relative to the rationals.

### Why $\log_2 3$ is irrational

If $\log_2 3 = p/q$ for integers $p, q > 0$, then $2^{p/q} = 3$, hence $2^p = 3^q$. By unique factorization of integers, this requires $p = q = 0$. Contradiction. So $\log_2 3 \notin \mathbb{Q}$.

### Why $\log_2 3$ is transcendental

By the **Gelfond–Schneider theorem** (1934): if $\alpha, \beta$ are algebraic with $\alpha \neq 0, 1$ and $\beta$ irrational, then $\alpha^{\beta}$ is transcendental. Take $\alpha = 2$, $\beta = \log_2 3$: if $\log_2 3$ were algebraic, then $2^{\log_2 3} = 3$ would be transcendental — contradiction. Hence $\log_2 3$ is transcendental.

So we are stuck working with a transcendental number whose rational approximations control the conjecture.

---

## 2. Continued Fractions — The Right Coordinate System

Every real number $x$ has a unique continued fraction expansion

$$x \;=\; a_0 + \cfrac{1}{a_1 + \cfrac{1}{a_2 + \cfrac{1}{a_3 + \cdots}}}$$

where $a_0 \in \mathbb{Z}$ and $a_i \in \mathbb{Z}_{>0}$ for $i \geq 1$. The integers $a_i$ are the **partial quotients**. We write $x = [a_0; a_1, a_2, \ldots]$.

For $\log_2 3$:

$$\log_2 3 \;=\; [1; \,1, 1, 2, 2, 3, 1, 5, 2, 23, 2, 2, 1, 1, 55, \ldots].$$

The **convergents** are the rational truncations $p_n / q_n = [a_0; a_1, \ldots, a_n]$. For $\log_2 3$:

| $n$ | $p_n / q_n$ | decimal |
|---|---|---|
| 0 | $1/1$ | $1.000$ |
| 1 | $2/1$ | $2.000$ |
| 2 | $3/2$ | $1.500$ |
| 3 | $8/5$ | $1.600$ |
| 4 | $19/12$ | $1.5833$ |
| 5 | $65/41$ | $1.58537$ |
| 9 | $485/306$ | $1.5849673$ |

The convergents are the **best rational approximations**: no fraction $p/q$ with $q \leq q_n$ approximates $\log_2 3$ better than $p_n / q_n$.

### The key fact about partial quotients

A large partial quotient $a_{n+1}$ produces an exceptionally good convergent. The general bound:

$$\left| x - \frac{p_n}{q_n} \right| \;\approx\; \frac{1}{a_{n+1} \cdot q_n^{\,2}}.$$

When $a_{n+1}$ is huge, the rational $p_n / q_n$ approximates $x$ much better than the generic rate $1/q_n^{\,2}$. For $\log_2 3$, the partial quotient $a_9 = 23$ makes the convergent $485 / 306$ "exceptionally close" — and $L = 306$ would be the most algebraically dangerous cycle length below the verification bound.

### Intuition for Collatz

A cycle of length $L$ forces $K / L$ to be an accurate rational approximation of $\log_2 3$. The Baker gap

$$\Delta_{\text{Baker}} \;=\; K \ln 2 - L \ln 3$$

shrinks when $K / L$ is a "lucky" approximation. The luckiest approximations are at convergent denominators. So *cycles, if they exist, want to live at $L = q_n$ for some $n$, with the danger scaling with $a_{n+1}$.*

---

## 3. The Irrationality Measure

The **irrationality measure** (or irrationality exponent) of a real $x$ is

$$\mu(x) \;:=\; \inf \left\{ \,\mu \,:\, \left| x - \frac{p}{q} \right| > \frac{1}{q^{\mu}} \text{ for all but finitely many } p/q \in \mathbb{Q}\, \right\}.$$

**Intuition.** $\mu(x)$ measures how badly $x$ *resists* rational approximation. Larger $\mu$ means $x$ has unusually good rational approximations — it gets "approached" by rationals faster than the generic rate.

**Standard values:**

- For *almost every* real number, $\mu(x) = 2$ (Khinchin's theorem, 1924).
- For rationals, $\mu(x) = 1$.
- For algebraic irrationals, $\mu(x) = 2$ (Roth's theorem, 1955 — Fields Medal work).
- For Liouville numbers (specifically constructed), $\mu(x) = \infty$.
- For "most" naturally arising transcendentals (including $\pi$, $e$, $\log 2$), $\mu = 2$ is *conjectured but not proven*.

### Connection to partial quotients

$\mu(x) = 2$ if and only if the partial quotients $a_n$ grow no faster than $q_n^{\,\varepsilon}$ for every $\varepsilon > 0$. Bounded partial quotients (i.e., $a_n \leq A$ for some constant $A$) is a *strictly stronger* statement than $\mu(x) = 2$.

### For Collatz

Mignotte's effective bound

$$|K \ln 2 - L \ln 3| \;>\; C_B \cdot \max(K, L)^{-\kappa}, \quad \kappa = 13.3$$

is equivalent to the irrationality measure bound

$$\mu(\log_2 3) \;\leq\; \kappa + 1 \;=\; 14.3.$$

The current unconditional best is $\mu(\log_2 3) \leq 5.117$ (Wu, 2003, sharpening Rukhadze 1987 and Hata 1990). The conjecture $\mu(\log_2 3) = 2$ would give $\kappa = 1 + \varepsilon$.

---

## 4. Lang's Conjecture and What It Buys

**Lang's conjecture** (Serge Lang, 1971), specialized to two logarithms:

> *For every algebraic number $\alpha \neq 0, 1$ and every irrational algebraic $\beta$, the irrationality measure of $\log \alpha / \log \beta$ equals 2.*

More generally, Lang conjectured that "almost all" naturally occurring transcendentals (logarithms, exponentials, periods of algebraic varieties) behave like generic transcendentals with respect to Diophantine approximation: $\mu = 2$.

**For $\log_2 3$.** This is exactly the case $\alpha = 3$, $\beta = 2$. Lang predicts:

$$\mu(\log_2 3) \;=\; 2.$$

### Plugging Lang into Collatz

Under Lang's conjecture, the Baker gap becomes

$$|K \ln 2 - L \ln 3| \;>\; C(\varepsilon) \cdot L^{-1-\varepsilon}$$

for any $\varepsilon > 0$. Substituting into the Lyapunov inequality $m_1 \leq (\text{const}) \cdot K^{\kappa}$:

$$m_1 \;\leq\; C^{\prime}(\varepsilon) \cdot K^{1+\varepsilon}.$$

Since $K \leq 2L$ for cycle candidates (in fact $K \approx 1.585 \, L$):

$$m_1 \;\leq\; C^{\prime\prime}(\varepsilon) \cdot L^{1+\varepsilon}.$$

Combined with the verification floor $m_1 > 2^{68}$:

$$L \;\geq\; C^{\prime\prime\prime}(\varepsilon) \cdot 2^{68/(1+\varepsilon)}.$$

For $\varepsilon < 1$, this gives $L \geq 2^{34}$ at least — far exceeding any plausible cycle length and any reasonable computational bound. **Effectively, Lang implies no non-trivial Collatz cycles.**

(There remains a separate question about *divergent orbits* — trajectories that escape to infinity — which neither Baker nor Lang addresses directly. For the cycle part of Collatz, Lang closes it.)

---

## 5. Why Bounding $\mu(\log_2 3)$ Is Hard

Transcendence of $\log_2 3$ was established in 1934. The irrationality measure has been bounded by ~13.3 since 1987 and sharpened to ~5.1 by 2003. The conjecture $\mu = 2$ has remained out of reach for ninety years. Why?

### The toolkit problem

All known bounds on irrationality measures of logarithms use **Padé approximations**: explicit polynomials $P_n, Q_n \in \mathbb{Z}[x]$ constructed so that

$$P_n(x) - Q_n(x) \log_2 3$$

is unusually small at $x = 3/2$ (or similar). The quality of the resulting bound depends on growth rates of $|P_n|, |Q_n|$ and arithmetic structure (common denominators, divisibility patterns). Current Padé constructions for $\log 3 / \log 2$ are essentially saturated — improving them requires fundamentally new approximation schemes.

### The structural problem

No one has identified what makes $\log_2 3$ special among transcendentals. Lang's conjecture predicts $\mu = 2$ but provides no algorithm. For algebraic numbers, Roth's theorem gives $\mu = 2$ via *ineffective* methods (proof by contradiction; no constructive bound on the implied constant). An analogous "Roth for logarithms" would close this and a vast family of related problems.

### The same wall, three costumes

The Collatz Lyapunov wall is identical to the Diophantine wall:

$$\text{(Lyapunov closes Collatz)} \iff \mu(\log_2 3) = 2 \iff \text{(bounded } a_n\text{)} \iff \text{(Lang for this pair)}.$$

This is genuinely a single problem, not three independent ones. Solving any one solves all.

---

## 6. Sub-Routes Within Route 1

If a direct proof of $\mu(\log_2 3) = 2$ remains out of reach, are there weaker statements that suffice for Collatz?

### Sub-route 1a — Marginal improvement of $\mu$

Prove $\mu(\log_2 3) \leq 2 + \delta$ for some specific small $\delta$. The smallest $\delta$ that suffices depends on $M_v$. With $M_v = 2^{68}$, roughly $\delta < 0.05$ would work. The current unconditional best is $\delta \approx 3.1$ (from $\mu \leq 5.117$). This sub-route is the most "classical" — chip away at $\mu$ until it crosses the Collatz threshold.

### Sub-route 1b — Bounded partial quotients at specific indices

If $a_n \leq f(n)$ can be proven for all $n$ with $f$ polynomially bounded, that suffices for Collatz (it is *strictly weaker* than $\mu = 2$). No known method targets specific partial quotients of a transcendental — but the question is well-defined and might admit a different toolkit.

### Sub-route 1c — One-sided positivity-constrained bound

Recall the cycle equation forces $\Delta_{\text{Baker}} = K \ln 2 - L \ln 3 > 0$ (so that the denominator $D = 2^K - 3^L$ is positive). The standard $\mu$ bound is two-sided. A *one-sided* lower bound — applying only to positive values of $K \ln 2 - L \ln 3$ — might be more tractable than the full two-sided $\mu$. The intuition: the integer lattice $(K, L)$ is asymmetric around $K / L = \log_2 3$, with "good" approximations clustering above and below the line. A bound on the positive side alone exploits only half of the approximation structure.

To my knowledge, no one has attempted this restricted form. It is a clean target.

---

## 7. Status and Best Entry Point

Route 1 is the most **classical** of the three routes. It connects Collatz directly to a 90-year-old open problem in Diophantine approximation.

**Advantage.** Any progress is independently significant. A bound $\mu(\log_2 3) < 5$ is publishable in number theory journals on its own merits.

**Disadvantage.** The problem has resisted attack for as long as it has been posed. Current tools appear saturated. Major new ideas — possibly from modular forms, motivic cohomology, or the theory of periods — would likely be required.

**Best entry point:** Sub-route 1c. A one-sided positivity-constrained lower bound is structurally different from the standard two-sided $\mu$ bound and might admit a different toolkit. It is also Collatz-specific in a way that the general $\mu$ problem is not — the cycle equation already specifies the sign of the quantity to be bounded.

---

## 8. Notation Summary

| Symbol | Meaning |
|---|---|
| $L$ | Number of odd steps in a hypothetical cycle |
| $K$ | Total halvings: $K = \sum k_i$ |
| $k_i$ | Halving count at step $i$: $k_i = v_2(3 m_i + 1)$ |
| $m_i$ | Odd element at position $i$ in the cycle |
| $\log_2 3$ | The exchange rate between primes 2 and 3 |
| $a_n$ | $n$-th partial quotient of $\log_2 3$ |
| $p_n / q_n$ | $n$-th convergent of $\log_2 3$ |
| $\mu(x)$ | Irrationality measure of $x$ |
| $C_B$ | Mignotte's effective Baker constant |
| $\kappa$ | Mignotte exponent, currently 13.3 |
| $M_v$ | Computational verification bound, $2^{68}$ (Barina 2020) |

## 9. References

- Mignotte, M. (1999). "A corollary to a theorem of Laurent–Mignotte–Nesterenko." *Acta Arithmetica* 86.
- Rukhadze, E. A. (1987). "A lower bound for the rational approximation of $\ln 2$ by rational numbers." *Vestnik Moskov. Univ.*
- Hata, M. (1990). "Legendre type polynomials and irrationality measures." *J. Reine Angew. Math.*
- Wu, Q. (2003). "On the linear independence measure of logarithms of rational numbers." *Math. Comp.*
- Lang, S. (1971). *Transcendental Numbers*. Springer.
- Roth, K. F. (1955). "Rational approximations to algebraic numbers." *Mathematika* 2.
- Tao, T. (2019). "Almost all orbits of the Collatz map attain almost bounded values." arXiv:1909.03562.
- Barina, D. (2020). "Convergence verification of the Collatz problem." *J. Supercomputing* 77.
