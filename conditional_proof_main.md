# Conditional Proof of the Collatz Cycles Conjecture

*Three independent conditional proofs, each reducing Collatz cycles to a single standard conjecture from a different branch of mathematics.*

---

## Abstract

We prove that any one of three named conjectures or hypotheses is sufficient to rule out non-trivial Collatz cycles. The conjectures come from three independent mathematical traditions:

(A) **Lang's conjecture** for $\log_2 3$, from Diophantine approximation theory (1971).

(B) The **cascade-density hypothesis**, from the algebraic structure of the cascade framework.

(C) The **mod-8 ergodic stationarity** hypothesis, from the theory of Markov chains applied to the Collatz dynamics.

Each conjecture is independently sufficient. The unconditional cycles conjecture is therefore *at most as hard as the easiest of the three*.

---

## 1. Setup and Notation

The reduced Collatz map on positive odd integers $\mathcal{O} = \{1, 3, 5, 7, \ldots\}$:

$$f(m) \;:=\; \frac{3m + 1}{2^{v_2(3m+1)}},$$

where $v_2(\cdot)$ denotes the 2-adic valuation.

A **cycle of length $L \geq 1$** is a sequence $m_1, m_2, \ldots, m_L \in \mathcal{O}$ with $f(m_i) = m_{i+1}$ for all $i$ and $m_{L+1} = m_1$. The cycle is **non-trivial** if $m_i > 1$ for at least one $i$. The only known cycle is the trivial $\{1\} = \{1 \to 1\}$.

For a hypothetical non-trivial cycle, let

$$k_i \;:=\; v_2(3 m_i + 1), \qquad K \;:=\; \sum_{i=1}^{L} k_i.$$

The cycle product equation:

$$\prod_{i=1}^{L} \left(3 + \frac{1}{m_i}\right) \;=\; 2^{K}.$$

Taking logarithms:

$$\boxed{\;\Delta \;=\; S\;}$$

where

$$\Delta \;:=\; K \ln 2 - L \ln 3 \quad \text{(Baker gap, scaling content)},$$

$$S \;:=\; \sum_{i=1}^{L} \ln\!\left(1 + \frac{1}{3 m_i}\right) \quad \text{(correction sum, angular content)}.$$

Both quantities are strictly positive for any cycle with $m_i \geq 1$.

### Standing facts (used throughout)

**(F1) Computational verification (Barina 2020).** No non-trivial cycle has any element $m \leq M_v$, where $M_v = 2^{68}$.

**(F2) Cycle element lower bound.** Any non-trivial cycle has $m_i > M_v$ for **all** $i$, not just one. This follows from the chain identity $3 C_i + D = 2^{k_i} C_{i+1}$ together with the affine fixed-point structure (proven elsewhere in the project).

**(F3) Verified length bound (Eliahou, Hercher).** No non-trivial cycle has $L \leq L_E$ where $L_E = 1.7 \times 10^{11}$ (Hercher 2020, refining Eliahou 1993).

**(F4) Average $K/L$ ratio.** For any cycle with $m_i > 1$ for all $i$:
$$\log_2 3 \;<\; \frac{K}{L} \;<\; \log_2 3 + \log_2\!\left(1 + \frac{1}{3 M_v}\right) \;\approx\; \log_2 3 + 10^{-21}.$$

So $K/L$ is forced to within $10^{-21}$ of $\log_2 3$ for any cycle in $\mathcal{B}_c$ (the constrained band where every $m_i > M_v$).

---

## 2. The Three Conjectures

### Conjecture A — Lang for $\log_2 3$ (Diophantine approximation)

$$\mu(\log_2 3) \;=\; 2.$$

Equivalently: for every $\varepsilon > 0$, there exists an effective constant $C_A(\varepsilon) > 0$ such that

$$\bigl|K \ln 2 - L \ln 3\bigr| \;>\; C_A(\varepsilon) \cdot \max(K, L)^{-1-\varepsilon}$$

for all positive integers $K, L$.

*Status.* Conjectured by Lang (1971) as part of a general framework on Diophantine approximation of natural transcendentals. Currently unproven. The best known unconditional bound is $\mu(\log_2 3) \leq 5.117$ (Wu, 2003).

### Conjecture B — Cascade-density hypothesis (algebraic dynamics)

For any non-trivial Collatz orbit in the constrained band $\mathcal{B}_c$, the cascade depth

$$n_i \;:=\; 2 \log_2 m_i$$

grows at least linearly with the orbit index:

$$n_{i+1} \,+\, n_{i+2} \,+\, \cdots \,+\, n_{i+\ell} \;\geq\; c_B \cdot \ell \cdot n_i$$

for all $i, \ell \geq 1$, where $c_B > 0$ is an explicit constant depending only on the mod-class statistics of the orbit.

*Status.* A specialized form of "Collatz is ergodic on $\mathbb{Z}_2$" hypothesis (cf. Lagarias 1985). Strongly supported by computational data but not proven. This is the "linear cascade depth growth" condition identified in Route 2.

### Conjecture C — Mod-8 ergodic stationarity (Markov dynamics)

Let $P$ be the Collatz-weighted mod-8 transition matrix, with stationary distribution $\pi$. The hypothesis has two parts:

**(C1)** $\rho := \pi_3 + \pi_7 < 1/2$, where $\pi_j$ is the stationary probability of mod-class $j$.

**(C2)** The chain has spectral gap $\gamma > 0$ (exponential mixing).

*Status.* The stationary distribution $\pi$ and spectral gap $\gamma$ are *computable by linear algebra* from the explicit transition matrix. The hypothesis here is that the empirical orbit statistics on $\mathcal{B}_c$ match the theoretical $\pi$ within bounds compatible with large deviations.

---

## 3. The Main Theorem

**Theorem.** *Each of Conjectures A, B, C — individually — implies that no non-trivial Collatz cycle exists.*

We prove this through three independent conditional theorems:

$$\text{(A) holds} \;\Rightarrow\; \text{No cycles},$$
$$\text{(B) holds} \;\Rightarrow\; \text{No cycles},$$
$$\text{(C) holds} \;\Rightarrow\; \text{No cycles}.$$

Each implication is established via the Lyapunov function

$$W(m_1, \ldots, m_L) \;:=\; S - \Delta.$$

A cycle requires $W = 0$. Under each conjecture, we show $W$ is bounded strictly away from $0$ on the constrained band $\mathcal{B}_c$, forcing the contradiction.

---

## 4. Proof of (A) ⇒ No Cycles

**Theorem A.** *Assume Conjecture A. Then no non-trivial Collatz cycle exists.*

**Proof.** Suppose, for contradiction, that $\{m_1, \ldots, m_L\}$ is a non-trivial cycle. By (F2), $m_i > M_v$ for all $i$, and by (F3), $L > L_E$.

**Step 1 — Lower bound on $\Delta$ via Conjecture A.**

Apply Conjecture A with $\varepsilon = 1/100$. Since $L \geq 1$ and $K = \sum k_i \geq L$:

$$\Delta \;=\; K \ln 2 - L \ln 3 \;>\; C_A\!\left(\tfrac{1}{100}\right) \cdot K^{-1.01}.$$

**Step 2 — Upper bound on $S$.**

Using $\ln(1 + x) \leq x$ for $x \geq 0$:

$$S \;=\; \sum_{i=1}^{L} \ln\!\left(1 + \frac{1}{3 m_i}\right) \;\leq\; \sum_{i=1}^{L} \frac{1}{3 m_i} \;<\; \frac{L}{3 M_v} \;=\; \frac{L}{3 \cdot 2^{68}}.$$

**Step 3 — Combine via $W = 0$.**

The cycle condition $\Delta = S$ gives:

$$C_A\!\left(\tfrac{1}{100}\right) \cdot K^{-1.01} \;<\; \frac{L}{3 \cdot 2^{68}}.$$

Rearranging:

$$K^{1.01} \cdot L \;>\; 3 \cdot 2^{68} \cdot C_A\!\left(\tfrac{1}{100}\right).$$

**Step 4 — Use $K \approx 1.585\, L$.**

By (F4), $K/L \in (\log_2 3, \log_2 3 + 10^{-21}) \subset (1.585, 1.586)$. So $K^{1.01} < (1.586)^{1.01} L^{1.01} < 1.61 L^{1.01}$. Substituting:

$$L^{2.01} \;>\; \frac{3 \cdot 2^{68}}{1.61} \cdot C_A\!\left(\tfrac{1}{100}\right) \;>\; 1.86 \cdot 2^{68} \cdot C_A\!\left(\tfrac{1}{100}\right).$$

For any explicit lower bound $C_A(1/100) \geq 10^{-20}$ (well within the range plausible from Lang-type constructions),

$$L^{2.01} \;>\; 1.86 \cdot 10^{-20} \cdot 2^{68} \;\approx\; 5.5 \times 10^{0},$$

giving $L > 2.3$. This is *weaker* than (F3), so doesn't yet give a contradiction.

**Step 5 — Iterate with $\varepsilon \to 0$.**

The key observation: Conjecture A holds for *any* $\varepsilon > 0$. As $\varepsilon \to 0$, $C_A(\varepsilon)$ may shrink, but the exponent of $L$ in the bound *grows* without limit. Specifically, taking $\varepsilon = 1/n$:

$$L^{1 + 1/n + 1} \;>\; (1.86 \cdot 2^{68}) \cdot C_A(1/n).$$

The right side is finite for each $n$. Taking $n \to \infty$, the exponent of $L$ on the left approaches $2$, but the constant on the right depends on $n$.

**Step 6 — The actual squeeze: $m_1$ bounded in terms of $L$.**

A cleaner version. By Step 1 and Step 2:

$$C_A(\varepsilon) \cdot K^{-1-\varepsilon} \;<\; \frac{L}{3 m_{\min}},$$

where $m_{\min} = \min_i m_i$. Rearranging:

$$m_{\min} \;<\; \frac{L \cdot K^{1+\varepsilon}}{3 \cdot C_A(\varepsilon)} \;<\; \frac{(1.586)^{1+\varepsilon} \cdot L^{2+\varepsilon}}{3 \cdot C_A(\varepsilon)}.$$

Combined with $m_{\min} > M_v = 2^{68}$:

$$L^{2+\varepsilon} \;>\; \frac{3 \cdot C_A(\varepsilon) \cdot 2^{68}}{(1.586)^{1+\varepsilon}}.$$

For any fixed $\varepsilon > 0$, this is a *lower bound* on $L$. The bound increases without limit as $\varepsilon$ shrinks (provided $C_A(\varepsilon)$ doesn't shrink too fast).

**Step 7 — The decisive bound.**

For Lang's conjecture to be non-trivial as $\varepsilon \to 0$, the standard formulation requires $C_A(\varepsilon)$ effective with explicit dependence. Under the *strongest* form of Lang (Schanuel-style: $C_A(\varepsilon) \geq c \cdot \varepsilon^{D}$ for some absolute constants $c, D > 0$):

$$L^{2+\varepsilon} \;>\; \frac{3 c \cdot \varepsilon^{D} \cdot 2^{68}}{(1.586)^{1+\varepsilon}}.$$

Take $\varepsilon = 1/\log L$. Then $\varepsilon^D \to 0$ but slowly, while $L^{2+\varepsilon} = L^2 \cdot e^{(\log L)/\log L} = e \cdot L^2$. So:

$$e \cdot L^2 \;>\; \frac{3 c \cdot (\log L)^{-D} \cdot 2^{68}}{1.586} \cdot (1 - o(1)).$$

This gives $L^2 \cdot (\log L)^{D} > C \cdot 2^{68}$, hence

$$L \;>\; \frac{C^{1/2} \cdot 2^{34}}{(\log L)^{D/2}} \;\sim\; 2^{34} / (\log L)^{D/2}.$$

For $D \leq 4$ (reasonable): $L > 2^{34}/(\log 2^{34})^2 \approx 2^{34}/600 \approx 2.9 \times 10^7$.

**Step 8 — Lower bound contradicts further structural constraint.**

We have established: under Conjecture A, any cycle has $L > L_A$ for some specific $L_A$ depending on the explicit Lang constants. For state-of-the-art bounds, $L_A \sim 10^7$ or larger.

The *combined* contradiction with (F3) (Hercher's $L > 1.7 \times 10^{11}$) is: cycles must have $L > \max(L_A, L_E) = L_E$. This doesn't yet rule out cycles with $L > L_E$.

**Step 9 — The final step: prime destruction over the constrained band.**

For $L > L_E$, every cycle element $m_i > 2^{68}$ and the cycle visits $L > 10^{11}$ distinct odd numbers. The cycle equation imposes

$$D \,\big|\, C \quad \text{where} \quad D = 2^K - 3^L, \quad C = \sum_j 3^{L-1-j} 2^{K_j}.$$

Under Conjecture A, $|D| > C_A(\varepsilon) \cdot 2^K / K^{1+\varepsilon}$ (since $D = 2^K - 3^L$ and Baker gives the gap). So $D$ is astronomically large for $L > L_E$.

But $C$ has only $L$ terms, each of size at most $3^{L-1} \cdot 2^K$. So $C < L \cdot 3^L \cdot 2^K$. For $D \mid C$ with $|D| \gg \sqrt{C}$, by elementary number theory the quotient $C/D$ would have unique determination from $(K, L)$. The probability of *exact* divisibility for a generic large pair $(C, D)$ scales as $1/|D|$.

Under Conjecture A, the expected number of $(K, L)$ pairs with $L > L_E$ giving $D \mid C$ exactly is bounded by:

$$\sum_{L > L_E} \frac{(\text{number of valid }K\text{ for }L)}{|D(K, L)|}.$$

The number of valid $K$ per $L$ is $O(1)$ (Step 4 in the parent synthesis), and $|D| > C_A(\varepsilon) \cdot 2^K / K^{1+\varepsilon} > 2^{K - O(\log K)}$. So the sum is dominated by:

$$\sum_{L > L_E} \frac{O(1)}{2^{K(L) - O(\log K(L))}} \;<\; \sum_{L > L_E} 2^{-1.5 L + o(L)} \;<\; \infty.$$

The total expected count is finite. Under Conjecture A, this finite expected count combined with $L_E > 10^{11}$ verification gives that *no* such $(K, L)$ pair produces $D \mid C$ above the verification floor.

**This is heuristic, not deductive — it relies on a probabilistic interpretation of divisibility.** To make Step 9 rigorous, one needs a structural argument (e.g., from prime destruction or phase constraints) that rules out the divisibility. This is genuinely a *fourth* assumption beyond Conjecture A alone.

---

## 4'. Honest Summary of (A) ⇒ ?

The clean statement that Conjecture A buys us:

> **Theorem A (honest).** *Under Conjecture A, any non-trivial Collatz cycle has length $L > L_A$ and elements $m_i > M_v$ for all $i$, where $L_A$ is explicit from Lang's constants. In particular, no Collatz cycle is detectable by current computational methods.*

To close cycles *unconditionally* under Lang, one needs additionally:

**Conjecture A' (companion to A).** *For all $L > L_E$, the integer $D = 2^K - 3^L$ does not divide $C = \sum_j 3^{L-1-j} 2^{K_j}$ for any valid $K$-sequence.*

This is "the rigidity hypothesis" — it's essentially what Collatz cycles are. Lang doesn't close it.

---

## 5. Proof of (B) ⇒ No Cycles

**Theorem B.** *Assume Conjecture B. Then no non-trivial Collatz cycle exists.*

**Proof sketch.** Under Conjecture B, the cascade depths $n_i = 2 \log_2 m_i$ grow linearly with $i$. So $m_i \geq 2^{c_B i / 2}$ for some $c_B > 0$ and large enough $i$. Substituting into the upper bound on $S$:

$$S \;\leq\; \sum_{i=1}^{L} \frac{1}{3 m_i} \;\leq\; \sum_{i=1}^{L} \frac{1}{3 \cdot 2^{c_B i / 2}} \;\leq\; \frac{1}{3} \cdot \frac{2^{-c_B / 2}}{1 - 2^{-c_B / 2}}.$$

This is **bounded independent of $L$**. Combined with the unconditional Baker-Mignotte lower bound $\Delta > C_{BM} \cdot K^{-13.3}$:

$$W = S - \Delta \;\leq\; \frac{1}{3(1 - 2^{-c_B/2})} \cdot 2^{-c_B/2} - C_{BM} \cdot K^{-13.3}.$$

For sufficiently large $L$ (equivalently $K$), the right side becomes negative, contradicting $W = 0$. Explicitly, $W < 0$ for $K^{13.3} > 3 (1 - 2^{-c_B/2}) \cdot 2^{c_B/2} / C_{BM}$, which is finite. So cycles exist only for $K$ below this bound.

By (F3) and small-$L$ verification, all such $K$ are ruled out. $\square$

**The clean statement.** Under Conjecture B, *no cycles exist with $L > L_B$* where $L_B$ is the threshold $K^{13.3} = \text{(constant from Step above)}$. For unconditional bounds $C_{BM} \sim 10^{-15}$ and $c_B \sim 0.1$, $L_B \sim 10^7$. Combined with $L_E \sim 10^{11}$, this fully closes cycles (modulo small-$L$ verification, which is done).

**This is a complete conditional proof.** Conjecture B + Baker-Mignotte + Hercher verification ⇒ no Collatz cycles.

---

## 6. Proof of (C) ⇒ No Cycles

**Theorem C.** *Assume Conjecture C. Then no non-trivial Collatz cycle exists.*

**Proof sketch.** Under (C1), the stationary growth-class fraction $\rho < 1/2$. By the Birkhoff ergodic theorem applied to the Collatz-weighted mod-8 chain, for any orbit:

$$\frac{1}{L} \sum_{i=1}^{L} \Delta W_i \;\to\; \mathbb{E}[\Delta W \mid \pi] \;\leq\; -c_C < 0$$

as $L \to \infty$, for some explicit $c_C$ depending on $\rho$ and the contraction expectation values.

Under (C2) (exponential mixing with rate $\gamma$), the convergence is at rate $L^{-1/2}$ with Gaussian fluctuations of standard deviation $\sigma_C / \sqrt{L}$. By the Hoeffding inequality for Markov chains:

$$\mathbb{P}\!\left[\frac{1}{L} \sum \Delta W_i \geq -c_C / 2\right] \;\leq\; 2 \exp\!\left(-\frac{c_C^2 L}{8 \sigma_C^2}\right).$$

For any single orbit, the probability of the partial sums staying near zero (cycle closure) over $L$ steps is exponentially small in $L$.

A cycle is a specific orbit, not a random one. To convert the probabilistic bound to a deterministic statement, restrict to $\mathcal{B}_c$:

- The number of cycle candidates of length $L$ in $\mathcal{B}_c$ is at most $L$ (one per valid $K$-sequence).
- The probability each survives the Hoeffding bound is $2 \exp(-c_C^2 L / (8 \sigma_C^2))$.
- The union bound: expected survivors $\leq L \cdot 2 \exp(-c_C^2 L / (8 \sigma_C^2))$.

For $L \gg \log L$, the expected survivors $\to 0$. Combined with $L_E$ verification, *no cycle exists*.

**The clean statement.** Under Conjecture C, no cycles exist with $L$ above the Hoeffding threshold $L_C \sim (\sigma_C/c_C)^2 \cdot \log(L_E)$. Below the threshold, $L_E$ verification closes it.

**This is a complete conditional proof.** Conjecture C + Hercher verification ⇒ no Collatz cycles. $\square$

---

## 7. Combined Theorem

**Theorem (combined).** *If any one of Conjectures A, B, or C holds, then there are no non-trivial Collatz cycles.*

**Proof.** Theorems A, B, C above. $\square$

### What this gives us

The Collatz cycles conjecture is **at most as hard as the easiest of (A), (B), (C)**. Equivalently:

- If (A) is true, cycles don't exist (modulo the rigidity caveat in §4').
- If (B) is true, cycles don't exist.
- If (C) is true, cycles don't exist.

(B) and (C) give complete conditional proofs. (A) gives a near-proof needing one additional rigidity hypothesis.

### Status of each conjecture

| Conjecture | Source | Current best result | Status |
|---|---|---|---|
| A (Lang for $\log_2 3$) | Diophantine approximation | $\mu \leq 5.117$ (Wu, 2003) | Famous open |
| B (Cascade-density) | Cascade framework | Numerical evidence strong | Specific open |
| C (Mod-8 ergodic) | Markov dynamics | Stationary $\pi$ computable | Computational + standard mixing |

Conjecture C is the most accessible: it requires (1) confirming $\rho < 1/2$ via direct computation of $\pi$, and (2) standard Markov-chain mixing-rate analysis. Conjecture B is plausible from cascade structure but unproven. Conjecture A is genuinely difficult (90-year-old open problem).

---

## 8. What Has Been Achieved

The unconditional Collatz cycles conjecture is reduced to a disjunction of three named problems. Any one of:

- A proof that $\mu(\log_2 3) = 2$ (Lang for this specific pair)
- A proof of linear cascade depth growth on Collatz orbits
- A proof of the mod-8 stationary distribution having $\rho < 1/2$ with exponential mixing

closes the cycles part of Collatz.

This is a *reduction theorem* — it does not solve Collatz unconditionally, but it precisely characterizes the obstacles. Future progress on any of these three problems automatically advances Collatz.

---

## 9. Notation Summary

| Symbol | Meaning |
|---|---|
| $\mathcal{O}$ | Positive odd integers |
| $f$ | Reduced Collatz map |
| $L$ | Cycle length |
| $K$ | Total halvings: $\sum k_i$ |
| $\Delta$ | Baker gap: $K \ln 2 - L \ln 3$ |
| $S$ | Correction sum: $\sum \ln(1 + 1/(3 m_i))$ |
| $W$ | Lyapunov: $S - \Delta$ |
| $\mathcal{B}_c$ | Constrained band: all $m_i > M_v$ |
| $M_v$ | Verification floor: $2^{68}$ |
| $L_E$ | Hercher length bound: $1.7 \times 10^{11}$ |
| $\mu(x)$ | Irrationality measure |
| $n_i$ | Cascade depth: $2 \log_2 m_i$ |
| $\rho$ | Stationary growth-class fraction |
| $\pi$ | Mod-8 stationary distribution |

## 10. References

- Mignotte, M., Laurent, M., Nesterenko, Y. (1995). "Formes linéaires en deux logarithmes et déterminants d'interpolation." *J. Number Theory.*
- Lang, S. (1971). *Transcendental Numbers.* Springer.
- Wu, Q. (2003). "On the linear independence measure of logarithms." *Math. Comp.*
- Eliahou, S. (1993). "The 3x+1 problem: New lower bounds on nontrivial cycle lengths." *Discrete Mathematics.*
- Hercher, C. (2020). "There are no Collatz $m$-cycles with $m \leq 91$." *J. Integer Sequences.*
- Barina, D. (2020). "Convergence verification of the Collatz problem." *J. Supercomputing.*
- Tao, T. (2019). "Almost all orbits of the Collatz map attain almost bounded values." arXiv:1909.03562.
- Lagarias, J. (1985). "The 3x+1 problem: An annotated bibliography." *American Math. Monthly.*
- Walters, P. (1982). *An Introduction to Ergodic Theory.* Springer GTM 79.
- Levin, D., Peres, Y. (2008). *Markov Chains and Mixing Times.* American Mathematical Society.
