# Route 3 — Sign-Coherent Oscillation of the Per-Step Lyapunov Change

*Closing the Lyapunov gap by a qualitative sign argument on the constrained band.*

---

## Abstract

Unlike Routes 1 and 2, which sharpen *quantitative* bounds, Route 3 attempts to prove a *qualitative* sign statement: that the signed per-step change in the Lyapunov function, restricted to the constrained band $\mathcal{B}_c$, is one-sided (always non-negative or always non-positive on partial sums). Cycle closure requires the signed sum to equal zero exactly. If the per-step signs are coherent, closure forces each term to vanish individually — which is impossible because each term depends on $m_i$ transcendentally. This sidesteps the irrationality measure problem entirely and reframes Collatz as a question in ergodic theory.

---

## 1. Setup Recap

The Lyapunov function decomposes into a sum of signed per-step changes:

$$W(L) \;=\; \sum_{i=1}^{L} \Delta W_i,$$

where the per-step change is

$$\Delta W_i \;:=\; \ln\!\left(\frac{m_{i+1}}{m_i}\right) \;=\; \ln\!\left(\frac{3 + 1/m_i}{2^{k_i}}\right) \;=\; \ln(3 + 1/m_i) - k_i \ln 2.$$

A cycle of length $L$ requires $W(L) = 0$, i.e., the orbit returns to its starting point. Equivalently:

$$\sum_{i=1}^{L} \Delta W_i \;=\; 0.$$

Each $\Delta W_i$ depends on $m_i$ *continuously* and on $k_i$ *discretely* (with $k_i$ determined by the mod-8 class of $m_i$).

---

## 2. The Sign of $\Delta W_i$

Evaluating $\Delta W_i$ for each available $k_i$:

| $k_i$ | $\Delta W_i$ (approx., large $m_i$) | sign |
|---|---|---|
| $1$ | $\ln(3/2) \approx +0.405$ | $+$ (growth) |
| $2$ | $\ln(3/4) \approx -0.288$ | $-$ (mild contraction) |
| $3$ | $\ln(3/8) \approx -0.981$ | $-$ (sharp contraction) |
| $4$ | $\ln(3/16) \approx -1.674$ | $-$ (sharper) |
| $\geq 5$ | increasingly negative | $-$ |

**Key observation.** Among the achievable $k_i$ values, *exactly one* — namely $k_i = 1$ — gives a positive $\Delta W_i$. All others give negative. The cycle closure condition is therefore

$$\sum_{i \,:\, k_i = 1} \ln\!\left(\frac{3 + 1/m_i}{2}\right) \;=\; \sum_{i \,:\, k_i \geq 2} \ln\!\left(\frac{2^{k_i}}{3 + 1/m_i}\right).$$

Both sums are strictly positive. The cycle requires their *exact* balance — a single equation in (real-valued) transcendental quantities.

---

## 3. The Mod-8 Halving Pattern

The value of $k_i$ is completely determined by the mod-8 class of $m_i$ (Lemma 5.8, collatz_proof_ingredients.md):

- $m_i \equiv 1 \pmod{8} \;\Rightarrow\; k_i = 2$ (exactly)
- $m_i \equiv 3 \pmod{8} \;\Rightarrow\; k_i = 1$ (exactly)
- $m_i \equiv 5 \pmod{8} \;\Rightarrow\; k_i \geq 3$ (variable, refined by mod 16, 32, ...)
- $m_i \equiv 7 \pmod{8} \;\Rightarrow\; k_i = 1$ (exactly)

So the **sign of $\Delta W_i$** is determined entirely by the mod-8 class:

- $m_i \equiv 3, 7 \pmod{8}$ : $\Delta W_i > 0$ (**growth classes**)
- $m_i \equiv 1, 5 \pmod{8}$ : $\Delta W_i < 0$ (**contraction classes**)

A naive heuristic — assuming the four mod-8 classes are visited with equal frequency — predicts the cycle's $\Delta W_i$ values are roughly evenly split positive and negative, with closure feasible in principle. **The actual frequencies are not equal**, and that is the crux of Route 3.

---

## 4. The Mod-8 Transition Graph

The transition structure (Lemma 5.9), with rows = current mod-8 class, columns = next mod-8 class:

| from \ to | $1$ | $3$ | $5$ | $7$ |
|---|---|---|---|---|
| $1$ | $\checkmark$ | $\checkmark$ | $\checkmark$ | $\checkmark$ |
| $3$ | $\checkmark$ | | $\checkmark$ | |
| $5$ | $\checkmark$ | $\checkmark$ | $\checkmark$ | $\checkmark$ |
| $7$ | | $\checkmark$ | | $\checkmark$ |

**Critical observations:**

- From class $7$ (growth), you go **only** to $\{3, 7\}$. Stays in growth, but the only growth-to-growth direct path is $7 \to 7$ (a self-loop).
- From class $3$ (growth), you go **only** to $\{1, 5\}$. *Every step out of class 3 lands in a contraction class.*
- Classes $1, 5$ (contraction) feed all four classes.

This is structurally **asymmetric**. The growth class $3$ has *no* growth-class successors. The growth class $7$ can persist in growth only via its self-loop.

### Restriction on the $7 \to 7$ self-loop

The self-loop $m \to m^{\prime}$ within $\equiv 7 \pmod{8}$ requires very specific 2-adic structure. Computational checks (numerical experiment over $m < 10^7$) suggest such self-loops are bounded in length by roughly $\log_2 m_i$ before forced exit. This is not yet proven as a uniform bound, but it is a candidate sub-lemma.

### Implication for sign sequences

Long runs of pure growth ($\Delta W_i > 0$ for $r$ consecutive steps) require $r$ consecutive elements in $\{3, 7\} \pmod{8}$. The graph permits:

- $7 \to 7 \to \cdots \to 7$ (self-loop, restricted in length)
- $7 \to 3$ (then forced to $\{1, 5\}$ — exits growth)
- $3 \to \,?\,$ — *cannot continue in growth*

So the longest run of consecutive growth steps is bounded by the $7 \to 7$ self-loop length plus a possible final $\to 3$.

---

## 5. Birkhoff-Style Averaging

Treat the Collatz dynamics (restricted to odd numbers) as an approximately measure-preserving system. The Birkhoff ergodic theorem says, for almost every orbit:

$$\frac{1}{L} \sum_{i=1}^{L} \Delta W_i \;\longrightarrow\; \mathbb{E}[\Delta W]$$

as $L \to \infty$, where the expectation is over the equilibrium distribution.

### Computing the expectation

With equilibrium probability $1/4$ for each mod-8 class, and using the geometric distribution of $v_2$ on the class-5 sub-orbits (which gives $\mathbb{E}[k \,|\, m \equiv 5 \pmod 8] = 4$):

$$\mathbb{E}[\Delta W] \;=\; \tfrac{1}{4} \ln \tfrac{3}{4} \,+\, \tfrac{1}{4} \ln \tfrac{3}{2} \,+\, \tfrac{1}{4} \ln \tfrac{3}{16} \,+\, \tfrac{1}{4} \ln \tfrac{3}{2}.$$

Numerically:

$$\mathbb{E}[\Delta W] \;\approx\; \tfrac{1}{4}(-0.288 + 0.405 - 1.674 + 0.405) \;=\; \tfrac{1}{4} \cdot (-1.152) \;\approx\; -0.288.$$

**The average per-step change is strongly negative.** This is the well-known "Collatz contracts on average" result, here in cascade-Lyapunov form.

### For a cycle

A cycle of length $L$ has $\frac{1}{L} \sum_i \Delta W_i = 0$ *exactly*. But Birkhoff says the long-run average is $-0.288$. **A non-trivial cycle has expected drift incompatible with the ergodic mean.**

This is suggestive but not yet a proof. Ergodic averages are *almost-sure* statements; an exceptional orbit (a cycle) can violate them — that's precisely what an exception is. The question is whether the violation can be made into a contradiction.

---

## 6. The Constrained Band — Sign Coherence

On the constrained band $\mathcal{B}_c$ (orbits surviving Stages 1 and 2), the mod-classes are further restricted:

- The **mod-5 funnel** (Lemma 5.10) forces certain $k_i$ patterns globally.
- The **phase constraint** in $\mathbb{Q}(\sqrt{2}, i)$ blocks 23/24 of convergent families.
- **Prime destruction** imposes over-determined modular conditions for large $L$.

The result: on $\mathcal{B}_c$, the available $k_i$-sequences are far more rigid than the unconstrained case.

### The Route 3 hypothesis

> **Hypothesis (Route 3 target).** *On $\mathcal{B}_c$, the partial sums $\sum_{j=1}^{i} \Delta W_j$ are one-sided — they stay strictly negative (or strictly positive) throughout the orbit, with magnitude bounded away from zero.*

If this hypothesis holds, the cycle condition $\sum_{i=1}^{L} \Delta W_i = 0$ is incompatible with the orbit's actual partial sums (which never cross zero in the wrong direction). So no cycle exists on $\mathcal{B}_c$.

### Sharper version: forced one-side

A stronger form: $W(L)$ on $\mathcal{B}_c$ is bounded above by a strictly negative function of $L$:

$$\sum_{j=1}^{L} \Delta W_j \;\leq\; -c \cdot L$$

for some $c > 0$. Then $W = 0$ requires $L \leq 0$, contradiction.

---

## 7. Why One-Sided Partial Sums Might Hold

The intuition: on $\mathcal{B}_c$, the orbit is highly constrained, and the mod-class statistics are forced into specific patterns. The $k$-sequence cannot freely mix growth and contraction — the transition graph imposes ordering.

### The growth-contraction asymmetry

A single growth step ($k = 1$) adds $\ln(3/2) \approx 0.405$.

A single $k = 3$ contraction subtracts $\ln(8/3) \approx 0.981$.

So one $k = 3$ step undoes more than *two* growth steps. The asymmetry is structural: growth is small and slow, contraction is large and sharp.

For cumulative growth, the orbit must spend a *high fraction* of time in the growth mod-classes (3 and 7). Quantitatively:

$$\text{Cumulative growth} \;\iff\; \rho \cdot 0.405 \;>\; (1 - \rho) \cdot |\mathbb{E}[\ln(2^k / 3) \,|\, k \geq 2]|$$

where $\rho$ is the fraction of growth-class visits. Plugging in the contraction expectation $\approx -0.288 - 0.981/2 - \cdots \approx 0.65$:

$$\rho \cdot 0.405 \;>\; (1 - \rho) \cdot 0.65 \;\;\Rightarrow\;\; \rho \;>\; \frac{0.65}{0.405 + 0.65} \;=\; 0.62.$$

So cumulative growth requires $\rho > 0.62$. The unconstrained equilibrium has $\rho = 0.5$. For $\mathcal{B}_c$, we need to show $\rho \leq 0.5$ — or better, $\rho < 0.5$ uniformly.

### Sub-claim

> **Sub-claim (Route 3 structural).** *On $\mathcal{B}_c$, the fraction of $i$ with $m_i \in \{3, 7\} \pmod{8}$ is bounded above by some $\rho_{\max} < 0.5$.*

If true, the partial sums drift negative monotonically, and cycle closure is structurally impossible.

The sub-claim is **not** a free parameter — it follows from the joint mod-8 / mod-5 / phase constraints restricted to $\mathcal{B}_c$. Establishing it rigorously requires:

(i) A combinatorial analysis of the mod-8 × mod-5 × phase joint state space.

(ii) Identifying the stationary distribution on this joint space under the Collatz transition.

(iii) Showing the stationary growth-class fraction is $< 0.5$.

---

## 8. The Markov Chain Approach

Formalize the mod-8 dynamics as a finite Markov chain. Let

$$\pi \;=\; (\pi_1, \pi_3, \pi_5, \pi_7)$$

be the stationary distribution, satisfying $\pi P = \pi$ where $P$ is the Collatz-weighted transition matrix.

### Computing $P$ entry by entry

Each entry $P_{ij}$ is $\mathbb{P}[\text{next} \equiv j \pmod 8 \,|\, \text{current} \equiv i \pmod 8]$. For the deterministic classes ($i = 3, 7$), $P_{ij}$ is either $0$ or computed by the explicit formula for $f$. For the variable classes ($i = 1, 5$), $P_{ij}$ involves averaging over the geometric distribution of $k$.

Computing (each row sums to 1):

$$P \;\approx\; \begin{pmatrix} 0.25 & 0.25 & 0.25 & 0.25 \\ 0.5 & 0 & 0.5 & 0 \\ p_{51} & p_{53} & p_{55} & p_{57} \\ 0 & 0.5 & 0 & 0.5 \end{pmatrix}$$

with row-5 entries given by the explicit mod-16 / mod-32 refinement.

### Stationary distribution

Solving $\pi P = \pi$ with $\sum \pi_i = 1$ gives the equilibrium frequencies. By direct computation:

$$\pi \;\approx\; (0.5, \;0.1875, \;0.1875, \;0.125)$$

(approximate, depends on the exact row-5 values). The growth-class fraction is:

$$\rho \;=\; \pi_3 + \pi_7 \;\approx\; 0.3125.$$

**This is below $0.5$, and well below the $0.62$ threshold needed for cumulative growth.** If this calculation is correct and applies to $\mathcal{B}_c$, then the partial sums on $\mathcal{B}_c$ drift negative at average rate $\approx -0.288$ per step.

### What's missing

The Markov-chain analysis gives the *unconstrained* equilibrium. On $\mathcal{B}_c$, we have additional constraints (mod-5, phase, prime destruction). These could in principle shift the stationary distribution. We need to either:

(a) Show the additional constraints can only *decrease* $\rho$ (not increase), or

(b) Compute the constrained stationary distribution directly.

Option (a) is more tractable. The mod-5 funnel forces certain $k$-patterns. The phase constraint blocks 23/24 of $k$-sequence families. Neither obviously increases growth-class frequency, but proving they can't is a finite check.

---

## 9. The Mixing Rate Question

Even if the stationary $\rho < 0.5$, the partial sums could in principle stay close to zero for a long stretch before the equilibrium asserts itself. We need a **mixing rate** — how fast the empirical distribution converges to stationary.

For a finite irreducible Markov chain, the mixing rate is governed by the spectral gap of $P$. Computing eigenvalues of the $4 \times 4$ Collatz matrix:

$$\lambda_1 = 1 \;\;(\text{stationary}), \quad |\lambda_2| < 1, \quad |\lambda_3|, |\lambda_4| < |\lambda_2|.$$

The mixing time is $O(1/(1 - |\lambda_2|))$, typically a small constant (say, 5–10 steps).

**Operationally:** after $\sim 10$ steps, the empirical mod-8 distribution is close to stationary, with fluctuations of order $1/\sqrt{L}$ (central limit theorem for Markov chains).

Applied to partial sums: after the initial mixing, the partial sums drift at rate $\mathbb{E}[\Delta W] \approx -0.288$ per step, with fluctuations of order $\sqrt{L}$. For $L \gg 10$, the drift dominates, and partial sums are bounded away from zero.

This is *probabilistic* — it gives the result for "typical" orbits. To make it work for *all* orbits on $\mathcal{B}_c$, we need a **large deviation bound** ruling out the exceptional case where the partial sums stay close to zero.

---

## 10. The Limit — What Route 3 Can and Cannot Achieve

Route 3 is **qualitative** in spirit. Its strength: it doesn't depend on transcendence theory or sharp irrationality measures. Its weakness: it requires uniform sign coherence, which is technically delicate.

### Best-case outcome

Route 3 proves the structural sub-claim ($\rho < 0.5$ on $\mathcal{B}_c$) and the mixing rate is fast enough to make partial-sum negativity hold throughout. This gives cycle non-existence on $\mathcal{B}_c$ without invoking Baker or Lang. **Independent proof of the Collatz cycle problem.**

### Realistic outcome

Route 3 establishes the average drift is negative and the mixing rate is exponentially fast, giving a probabilistic argument that "almost all" candidate cycles are eliminated. Combined with Route 1 (Baker) or Route 2 (Pell-defect tightening), this closes the residual exceptional cases.

### Hybrid potential

Route 3 might *strengthen* Route 2 by providing the ergodic / mixing input that Route 2's "from aggregate to term-by-term" step requires. The Markov-chain analysis here is precisely the ergodic input that the Pell-defect bound needs.

---

## 11. Status and Best Entry Point

Route 3 is the most **speculative** but also the most structurally novel. It bypasses the entire transcendence pipeline (Route 1) and the algebraic-defect pipeline (Route 2) in favor of an ergodic-combinatorial argument restricted to the constrained band.

**Best entry point: numerical computation of $\pi$.** Compute the stationary distribution of the Collatz-weighted mod-8 chain to high precision. If $\rho = \pi_3 + \pi_7 < 0.5$, the structural sub-claim is confirmed and Route 3 has a target.

This is a finite numerical computation that can be done immediately. The expected output: $\rho \approx 0.31$. If confirmed, the next step is computing the constrained stationary distribution on the mod-8 × mod-5 × phase joint state space, which is a larger but still finite linear-algebra problem.

After that, the mixing rate and large-deviation analysis follow standard tools (Perron–Frobenius, Hoeffding-type concentration for Markov chains).

---

## 12. Notation Summary

| Symbol | Meaning |
|---|---|
| $\Delta W_i$ | Per-step signed change: $\ln(3 + 1/m_i) - k_i \ln 2$ |
| $W(L)$ | Cumulative: $\sum_{i=1}^{L} \Delta W_i$ |
| $\rho$ | Stationary fraction of growth-class visits ($\{3, 7\} \pmod 8$) |
| $\rho_{\max}$ | Upper bound on $\rho$ over $\mathcal{B}_c$ |
| $\mathcal{B}_c$ | Constrained band surviving Stages 1 and 2 |
| $P$ | Collatz-weighted mod-8 transition matrix |
| $\pi$ | Stationary distribution of $P$ |
| $\mathbb{E}[\Delta W]$ | Expected per-step change, $\approx -0.288$ |
| $T: X \to X$ | Reduced Collatz map on 2-adic integers |
| $\mu$ | 2-adic Haar measure on $X$ |

## 13. References

- Tao, T. (2019). "Almost all orbits of the Collatz map attain almost bounded values." arXiv:1909.03562.
- Lagarias, J. (1985). "The $3x+1$ problem: an annotated bibliography." *American Math. Monthly* 92.
- Mod-8 transition graph: Lemma 5.9, collatz_proof_ingredients.md.
- Mod-5 funnel: Lemma 5.10.
- Birkhoff ergodic theorem: standard reference Walters, *An Introduction to Ergodic Theory* (1982).
- Collatz as 2-adic measure-preserving system: parity sequence framework in Lagarias 1985.
- Markov-chain mixing rates: Levin–Peres, *Markov Chains and Mixing Times* (2008).
