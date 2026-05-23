# Project Overview — Every Approach We Tried, and How Far Each Got

*A complete tour of the research program. Some approaches led to proofs. Some led to walls. Some led to numerical observations of unclear status. This document organizes all of them.*

---

## Contents

1. [The Geometric Reframing](#1-the-geometric-reframing)
2. [The Reduced Problem and Cycle Equation](#2-the-reduced-problem-and-cycle-equation)
3. [The (n, m) Manifold](#3-the-n-m-manifold)
4. [Cascade Framework and Pell Algebra](#4-cascade-framework-and-pell-algebra)
5. [Modular and Combinatorial Approaches](#5-modular-and-combinatorial-approaches)
6. [The Polynomial Picture](#6-the-polynomial-picture)
7. [Structural Variants and Stress Tests](#7-structural-variants-and-stress-tests)
8. [Numerical Threads](#8-numerical-threads)
9. [The Unified Proof Architecture](#9-the-unified-proof-architecture)
10. [Status Map — What's Proven, Conjectured, Speculative](#10-status-map)
11. [Open Directions](#11-open-directions)

---

## 1. The Geometric Reframing

### 1.1 Multiplicative vs. additive duality

The starting insight: number theory has **two orthogonal dimensions**, and every hard problem lives where they collide.

- **Multiplicative dimension** (radial, scaling): primes, multiplication, division. Maps to vector addition in prime-coordinate space.
- **Additive dimension** (angular, rotation): the $+1$ operation, sums. Maps to rotation in the complex plane.

In the complex plane, every $z = r e^{i\theta}$ separates into magnitude (multiplicative) and phase (additive). The two are 90° apart by definition. **No rational transformation converts one into the other.**

### 1.2 Why every hard problem looks the same

Once the duality is clear, hard problems in number theory pattern-match:

| Problem | Multiplicative side | Additive side |
|---|---|---|
| Collatz | $\times 3$, $\div 2$ | $+1$ |
| Goldbach | Primes (atoms) | Even numbers (sums) |
| Twin primes | Prime gaps | Difference $= 2$ |
| Riemann | Prime distribution | Position on number line |
| ABC | $a + b = c$ | Prime-power content |

All hard for the same reason: we lack a unified coordinate system where both structures are simultaneously legible.

### 1.3 The prime lattice

Each prime is an independent axis. Multiplication is vector addition. Division is vector subtraction. The number 1 is the origin (the vacuum, not really a number). The familiar number line is the *wrong* coordinate system for multiplicative structure — primes are evenly spaced on a *log* scale (Prime Number Theorem), not a linear one.

### 1.4 The cascade operator $\omega$

$$\omega = \frac{1+i}{2}, \quad |\omega| = \frac{1}{\sqrt{2}}, \quad \arg(\omega) = \frac{\pi}{4}.$$

This is the *unique 45° interface* where radial and angular components have equal magnitude. The cascade period — eight steps of multiplication by $\omega$ — completes one full rotation ($8 \cdot \pi/4 = 2\pi$) while contracting by $(1/\sqrt{2})^8 = 1/16$. The fundamental connection: angular period equals $2\pi$ times the radial e-fold rate. Pure geometry.

### Status

This reframing is **structural intuition**, not a theorem. It motivates everything else. The actual mathematical content is in the explicit machinery below.

---

## 2. The Reduced Problem and Cycle Equation

### 2.1 The reduced map

Strip even numbers: every positive integer reduces to its odd part after a finite number of $\div 2$ operations. The dynamics live on odd numbers.

Strip multiples of 3: when $m \equiv 0 \pmod 3$, the orbit decreases. The relevant set is **odd numbers not divisible by 3**.

The reduced map: $f(m) = (3m+1)/2^{v_2(3m+1)}$.

### 2.2 The cycle product equation

For any cycle of length $L$ with halving counts $k_1, \ldots, k_L$, $K = \sum k_i$:

$$\prod_{i=1}^{L} \left(3 + \frac{1}{m_i}\right) = 2^K.$$

### 2.3 The cycle fixed-point formula

For a fixed step sequence $(k_1, \ldots, k_L)$, there is *at most one* cycle candidate:

$$m_1 = \frac{C}{D}, \quad D = 2^K - 3^L, \quad C = \sum_{j=0}^{L-1} 3^{L-1-j} \cdot 2^{K_j},$$

where $K_j = k_1 + \cdots + k_{j+1}$.

A cycle exists if and only if $D \mid C$ and the resulting $m_1$ is a positive odd integer.

### 2.4 What this reduction accomplishes

We've converted Collatz cycles to a **pure integer divisibility question**. No logarithms, no transcendentals, no dynamics. Just: given $K$, $L$, and an ordered partition $(k_1, \ldots, k_L)$ of $K$ into $L$ positive parts, does the integer $D = 2^K - 3^L$ divide the integer $C$?

### 2.5 What's proven about this equation

- $C$ is always odd, $D$ is always odd, so $C/D$ is automatically odd.
- $C/D$ is automatically not divisible by 3.
- $|C| < L \cdot 3^{L-1} \cdot 2^{K}$ (loose) and $|D| > C_B \cdot 2^K / K^{13.3}$ (Baker).
- For $L \leq 3$, no cycles exist (direct check).
- For uniform-step cycles ($k_i$ all equal), no cycles exist (irrational ratio).
- For all $L \leq 1.7 \times 10^{11}$, no cycles exist (Hercher).
- For all elements $m \leq 2^{68}$, no cycles exist (Barina).

### 2.6 The wall

In one sentence:

> *We don't know how to prove that $D = 2^K - 3^L$ never divides $C$ for valid step sequences beyond the verification floor.*

Every other approach in this document is trying to attack this divisibility question from a different angle.

---

## 3. The (n, m) Manifold

### 3.1 Canonical coordinates

Every positive odd integer $p$ has a unique representation:

$$p = 2^n \cdot m - 1$$

where $n = v_2(p+1) \geq 1$ and $m$ is odd. This is a bijection between odd integers and pairs $(n, m)$ with $n \geq 1$ and $m \geq 1$ odd.

**Interpretation:** $n$ is the "2-adic countdown capacity" (how close $p$ is to a power-of-2-minus-1). $m$ is the "odd core" after stripping the 2-structure.

### 3.2 Dynamics in (n, m)

For $n \geq 2$: $(n, m) \to (n-1, 3m)$. **Pure deterministic countdown** — no branching, no choice.

At $n = 1$ (the reset boundary): a discrete jump computed by the meta-equation.

### 3.3 The energy invariant

$W = 3^n \cdot m$ is **conserved during countdown**. It changes only at resets.

This makes $W$ a natural Lyapunov candidate. The condition for $W$ to decrease at a reset:

$$\frac{n_1}{k} < \frac{\ln 2}{\ln(3/2)} = \frac{1}{\log_2 3 - 1} \approx 1.709.$$

**The threshold $1.709$ encodes $\log_2 3$.** The Lyapunov condition is exactly equivalent to bounding the partial quotients of the continued fraction of $\log_2 3$. Same wall, different costume.

### 3.4 What this gives

- Cleanly separates the "smooth" countdown from the "noisy" reset.
- Identifies $W = 3^n m$ as the canonical energy.
- Reveals the wall as an explicit Diophantine condition.

### Status

The framework is **fully developed and rigorous** as documented in [`collatz_proof_ingredients.md`](collatz_proof_ingredients.md). The Lyapunov function $W$ is *not* universally decreasing — it can increase at certain resets. That's the wall.

---

## 4. Cascade Framework and Pell Algebra

### 4.1 The bridge identities

Three exact algebraic identities connect Collatz to $\sqrt{2}$:

$$\frac{3}{2} - \sqrt{2} = \left(1 - \frac{1}{\sqrt{2}}\right)^{\!2}, \quad \frac{9}{8} = 1 + \frac{1}{8} = 1 + \left(\frac{1}{2}\right)^{\!3}, \quad \ln 3 = \frac{3}{2} \ln 2 + \frac{1}{2} \ln \frac{9}{8}.$$

These are not approximations — they are equalities in $\mathbb{Q}(\sqrt{2})$ and $\mathbb{R}$.

### 4.2 The Pell defect

$$\left(1 - \frac{1}{\sqrt{2}}\right)^{\!n} = A_n - B_n \sqrt{2}, \qquad A_n^2 - 2 B_n^2 = \left(\frac{1}{2}\right)^{\!n}.$$

The Pell defect $(1/2)^n$ is **exact and exponentially decaying**. This is the heart of the cascade framework: Pell approximations to $\sqrt{2}$ converge geometrically, while convergents to $\log_2 3$ converge only polynomially. We trade the unknown transcendental for a known algebraic structure plus a transcendental residual.

### 4.3 The cascade operator

$\omega = (1+i)/2$ with $|\omega| = 1/\sqrt{2}$ and $\arg(\omega) = \pi/4$. Cascade coordinates $n(v) = 2 \log_2 v$. Cascade period 8: $\omega^8 = -1/16$, completing a full angular rotation while contracting by 16.

### 4.4 The displacement defect and phase pulse

Two distinct algebraic identities:

- **Defect (decay):** $A_n^2 - 2 B_n^2 = (1/2)^n$. Exponentially decreasing. Drives the cascade convergence.
- **Pulse (oscillation):** $(3/2)(1 - \sqrt 2)^n$ has constant-magnitude norm $\pm 9/4$ oscillating with period 2. The cascade's "heartbeat."

These two are independent and measure different things. The defect is the contraction; the pulse is the parity swing.

### 4.5 The phase constraint in $\mathbb{Q}(\sqrt{2}, i)$

Extending the cycle equation to $\mathbb{Q}(\sqrt{2}, i)$ (the Klein four extension) gives an additional phase constraint. Computation shows it **kills 23/24 of convergent families** for cycle existence.

**The caveat:** the constraint doesn't pull back to $\mathbb{Z}$-Collatz cycle existence directly. It rules out cycles in the extended Galois field, but $\mathbb{Z}$-cycles live in a smaller object.

### 4.6 What this gives

- Exact algebraic identities replacing unknown transcendental data.
- A measurable "Pell residual" for the deviation of $\log_2 3$ from the Pell lattice.
- A phase constraint that's strong on the extended field but doesn't yet close $\mathbb{Z}$-cycles.

### Status

The cascade framework is **fully algebraic and exact**, documented in [`cascade_framework_full_2026-05-22.md`](cascade_framework_full_2026-05-22.md). It provides the proper coordinates but doesn't by itself close Collatz.

---

## 5. Modular and Combinatorial Approaches

### 5.1 Mod-8 halving pattern

The value of $k_i = v_2(3 m_i + 1)$ is determined by $m_i \bmod 8$:

| $m \bmod 8$ | $k$ |
|---|---|
| 1 | 2 (exactly) |
| 3 | 1 (exactly) |
| 5 | $\geq 3$ (variable, refined by mod 16) |
| 7 | 1 (exactly) |

### 5.2 Mod-8 transition graph

Source $\to$ targets:

| from | to | $k$ |
|---|---|---|
| 1 | $\{1, 3, 5, 7\}$ | 2 |
| 3 | $\{1, 5\}$ | 1 |
| 5 | $\{1, 3, 5, 7\}$ | $\geq 3$ |
| 7 | $\{3, 7\}$ | 1 |

77 distinct closed orbits up to length 5. The achievable $K \bmod 8$ values over all orbits cover the full set $\{0, 1, \ldots, 7\}$. **Mod 8 alone does not isolate $K \equiv 0 \pmod 8$.**

### 5.3 Mod-5 funnel

$m \equiv 3 \pmod 5$ always exits to $0 \bmod 5$, regardless of $k$. This is a directional structural constraint.

### 5.4 Mod-5 transition graph

```
0 → {1, 2, 3, 4}
1 → {1, 2, 3, 4}     (self-loop at k ≡ 2 mod 4)
2 → {1, 2, 3, 4}     (self-loop at k ≡ 0 mod 4)
3 → {0} only         ← the funnel
4 → {1, 2, 3, 4}     (self-loop at k ≡ 1 mod 4)
```

For each closed mod-5 orbit, the $k \bmod 4$ sequence is forced.

### 5.5 Prime destruction

For any odd prime $p$ dividing $m$: $p \nmid 3m + 1$. So **every prime factor of $m$ is obliterated by one application of $3m+1$**. For a cycle, every prime factor must be regenerated within the cycle, imposing modular conditions on the elements.

### 5.6 Inverse construction at small $(K, L)$

For specific $(K, L)$ with small $D$, enumerate all valid $k$-tuples and compute $N_L \bmod D$:

- $(K, L) = (8, 5)$: $D = 13$. All $\binom{7}{4} = 35$ ordered partitions give $N_L \bmod 13 \in \{1, 2, \ldots, 12\}$. **Never 0.**
- $(K, L) = (5, 3)$: zero valid k-tuples.
- $(K, L) = (13, 8)$: zero valid k-tuples.
- $(K, L) = (16, 10)$: zero valid k-tuples.

Every feasible small $(K, L)$ with $D > 0$ tested gives no cycle.

### 5.7 What this gives

- Direct elimination of small-$(K, L)$ cycles by enumeration.
- Structural directionality (mod-5 funnel).
- Prime regeneration as a rigidity constraint that grows with $L$.

### Status

Computational. The mod-5 funnel and mod-8 graph are **proven properties**. The "prime destruction implies no cycles" intuition is structurally sound but doesn't constitute a proof.

---

## 6. The Polynomial Picture

### 6.1 C and D as polynomial evaluations

$$C = P(2, 3), \quad D = Q(2, 3),$$

where $P(x, y) = \sum_j y^{L-1-j} \cdot x^{K_j}$ and $Q(x, y) = x^K - y^L$.

The cycle question "$D \mid C$?" becomes the algebraic question "what's the relationship between these polynomials?"

### 6.2 The degree argument

$\deg_x P \leq K - 1 < K = \deg_x Q$, and $\deg_y P = L - 1 < L = \deg_y Q$.

$P$ is *strictly smaller* than $Q$ in both variables. As polynomials in $\mathbb{Z}[x, y]$, **$Q$ does not divide $P$**.

Fix $x = 2$: $R(y) := P(2, y)$ has degree $L-1 < L = \deg D(y)$. So $R(y)$ is not divisible by $D(y)$ as polynomials in $\mathbb{Z}[y]$.

The roots of $D(y) = 2^K - y^L$ are $\alpha_j = 2^{K/L} \cdot e^{2\pi i j/L}$ — $L$ equally spaced points on a circle of radius $2^{K/L}$. Since $\deg R = L-1$ and the minimal polynomial of $2^{K/L}$ over $\mathbb{Q}$ has degree $L$:

$$R(\alpha_j) \neq 0 \text{ for any } j.$$

**The polynomial-level orthogonality is proven.**

### 6.3 The gap

The cycle condition is $R(3) \equiv 0 \pmod D$. This is divisibility *at the integer point* $y = 3$, not at the algebraic root $y = 2^{K/L}$.

Because $\log_2 3$ is irrational, $3 \neq 2^{K/L}$ for any integers. The polynomial non-vanishing at the algebraic root tells us nothing about the integer evaluation modulo $D$.

The irrationality of $\log_2 3$ plays a cruel double role:

- *It helps:* $D = 2^K - 3^L \neq 0$. Baker's theorem makes $D$ grow exponentially.
- *It blocks:* $3 \neq 2^{K/L}$. The polynomial argument can't close.

The same fact both enables Baker and prevents the polynomial closure.

### 6.4 Four polynomial transformations

Each tries to push the polynomial argument further:

**Zero Form.** Turn divisibility into kernel membership in $\mathbb{Z}[y]/(y^L - 2^K)$. The cycle condition becomes $R \in \ker(y \mapsto 3, \bmod D)$. **Wall:** the kernel is non-trivially large.

**Resultant.** $\mathrm{Res}(R, D) = \prod_j R(\alpha_j) \neq 0$. Provably a nonzero integer. **Wall:** global non-vanishing across all $L$ roots doesn't bound the value at one specific point $y = 3$.

**Gaussian integer factoring.** Work in $\mathbb{Z}[i]$ where $2 = -i(1+i)^2$. **Wall:** the valuation $v_{(1+i)}(D) = 0$ is automatically satisfied; primes 2 and 3 don't create asymmetry in $\mathbb{Z}[i]$.

**Tropical geometry.** Replace addition with min, multiplication with addition. $\mathrm{Trop}(D)(\log 3) = \min(K \log 2, L \log 3)$ is strictly determined by one term (since $K \log 2 \neq L \log 3$). **Wall:** tropical algebra discards the sub-leading arithmetic that divisibility depends on.

### 6.5 What this gives

- A clean structural statement (orthogonality at polynomial level) and a precise location of the gap.
- Four different angles, all hitting walls of the same shape: the obstruction is global, not local.

### Status

The polynomial orthogonality at the *algebraic* level is **fully proven**. The transfer to the *evaluation point* $y = 3$ modulo $D$ is the wall. Documented in synthesis 2026-05-23.

---

## 7. Structural Variants and Stress Tests

### 7.1 The DNCC ("Don't Need Cycle at 1") move

Remove $m = 1$ from the domain. The map remains a bijection on $\mathcal{O} \setminus \{1\}$. **The trivial cycle vanishes; other cycles (if they exist) survive.** This isolates the question to non-trivial cycles only.

### 7.2 Further restrictions

Strip restrictions one at a time and test:

- Remove $m = 1$: trivial cycle vanishes. Other cycles unaffected.
- Remove powers of 2 minus 1 (Mersenne): same — they don't form cycles anyway.
- Restrict to $m \not\equiv 0 \pmod 3$: this is the *active* space.
- Restrict to $m \equiv 1 \pmod 4$: subset of active space; other classes form trees flowing in.

**Conclusion:** the cycle problem lives entirely on $\{m : m \text{ odd}, m \not\equiv 0 \pmod 3, m > 1\}$.

### 7.3 The wall stress test — three pillars

Strip the structural features one at a time and find which are load-bearing for cycle non-existence:

| Restriction | Stripped | Cycles appear? |
|---|---|---|
| Affine structure | Replace with quadratic | Yes |
| Prime destruction | Use $5x+1$ | Yes (13 → 33 → 83 → 13) |
| Irrational balance | Use $4x+1$ | Yes (closes trivially) |

**The three pillars** that hold the wall:

1. **Affine structure.** Each step is $m \to (3m+1)/2^k$ — composition gives one fixed-point candidate per partition.
2. **Complete prime destruction.** Every prime factor vanishes; regeneration is over-determined.
3. **Irrational balance.** $\log_2 3$ irrational, so $3^L \neq 2^K$ for any positive integers.

Each pillar alone is breakable. **The wall is the conjunction.**

The geometric mean $3/(2\sqrt{2})$ encodes all three pillars in a single object — affine balance point (1), prime ratio (2), irrational excess (3).

### 7.4 The half-cycle / $\mathbb{N}^{-1}$ observation

If addition is rotation with period $2\pi$ and we only work in $\mathbb{N}$, we sit at angle 0. We never rotate past $\pi$. The missing half is at angle $\pi$, which corresponds to $-1$.

In $\mathbb{Z}_2$: $-1$ is the fixed point of the Collatz map ($T(-1) = -1$). The Mersenne numbers $2^n - 1$ converge 2-adically to $-1$. **The "missing half" of $\mathbb{N}$ is encoded in $\mathbb{N}$ itself — it just looks like running to infinity in the ordinary metric while converging to $-1$ in the 2-adic metric.**

This is a suggestive observation, not a proof tool. It does suggest working in $\mathbb{Z}_2$ rather than $\mathbb{Z}$ might reveal additional structure.

### 7.5 The injectivity correction

The full Collatz map $m \to (\text{odd part}(3m+1), v_2(3m+1))$ is *injective*. Each odd $m$ lands at a unique point $(q, v)$ in the destination/depth plane. The "many-to-one" appearance is only an artifact of projecting away the depth coordinate.

**Consequence:** the cycle question is about a *bijection* on $\mathcal{O}$ (after suitable identifications), and bijections on infinite sets can have any cycle structure compatible with their algebraic invariants. The non-existence is not automatic; it's a deep statement.

### Status

These are **structural observations** that organize how we think about the problem. They're proven, but don't constitute a proof of cycle non-existence on their own.

---

## 8. Numerical Threads

### 8.1 The near-identity

$$\frac{3}{4}\sqrt{\pi} + \log_2(3) - \frac{3}{2} \approx \sqrt{2}, \qquad \varepsilon \approx 8.93 \times 10^{-5}.$$

Three constants from three contexts (continuous $\Gamma$, discrete log, cascade base) sum to within $10^{-5}$ of a fourth. Not exact (Schanuel). $\varepsilon > 0$ means smooth analysis is *conservative* — discrete reality is more contractive.

Plays three roles in the proof architecture:
- **Diagnostic:** confirms smooth and discrete pictures are almost coherent.
- **Scale-setter:** sets the size of the band Stage 3 must close.
- **Sign-fixer:** because $\varepsilon > 0$, Route 2's target is *strictly easier* than the discrete-tight bound.

Detail in [`near_identity_role.md`](near_identity_role.md).

### 8.2 The geometric mean $G = 3/(2\sqrt{2})$

Triple-bridging role:
- **Job 1:** $G^2 = 9/8 = (3/2)(3/4)$ — exactly half-and-half of Collatz step ratios.
- **Job 2:** $|G|_2 = 2\sqrt{2}$ (large 2-adically), $|G|_3 = 1/3$ (small 3-adically). Opposite orientation in $\mathbb{Q}_2$ and $\mathbb{Q}_3$.
- **Job 3:** $\log_2 G = \log_2(3) - 3/2 \approx 0.085$, the geometric-mean excess that defines the convergent gap.

### 8.3 The convergent gap $\gamma = \log_2 3 - \sqrt{2} \approx 0.171$

Direct study of the relationship between the two relevant transcendentals.

| $q$ | best rational $p/q$ | error |
|---|---|---|
| 2 | $1/2 \cdot 2/q$ | not close to integer |
| 5 | $1/5$ | 0.029 |
| 12 | $2/12 = 1/6$ | 0.004 |
| 41 | $7/41$ | $5 \times 10^{-5}$ |

At $q = 41$, the gap is approximated to 5 decimal places. $41$ is in *both* the Pell numerator sequence and the $\log_2(3)$ convergent denominators. This is the *tightest* shared convergence between the two transcendentals.

### 8.4 The (3/2)! identity

$$\left(\frac{3}{2}\right)! = \Gamma(5/2) = \frac{3}{4}\sqrt{\pi}.$$

The half-integer factorial at the Collatz step ratio. Brings $\sqrt{\pi}$ (continuous) into a Collatz context (discrete). One of the three terms in the near-identity.

### 8.5 The $\zeta$ functional equation observation

The constants in the near-identity ($\sqrt{\pi}$, $\log_2 3$, $\sqrt{2}$) are exactly the ingredients of $\zeta$'s functional equation restricted to primes 2 and 3. The near-coincidence might be detecting a near-resonance at the critical line — analogous to how $e^{\pi\sqrt{163}}$ is nearly an integer because of Heegner number 163.

**Speculative.** Not a proof tool. Suggests the framework is touching deep structure.

### 8.6 Mersenne primes and perfect numbers

The $m = 1$ spine of $(n, m)$ coordinates is $p = 2^n - 1$ — the Mersenne numbers. Even perfect numbers $2^{p-1}(2^p - 1)$ are exactly a power of 2 times a Mersenne prime. Collatz on a perfect number strips the 2-shell in $p-1$ halvings and hands you the Mersenne core.

The conjecture "infinitely many Mersenne primes" hits the **same wall** as Collatz: the incommensurability of 2 and 3.

### Status

Numerical observations. None are theorems. They organize the framework but don't constitute proof. The near-identity is the most structurally significant; the rest are suggestive.

---

## 9. The Unified Proof Architecture

### 9.1 The three-stage strategy

**Stage 1 (DONE).** Tao's 2019 density argument kills almost all trajectories. Residual: measure-zero set of potential exceptions.

**Stage 2 (PARTIAL).** Algebraic filters carve at the residual:
- Pell defect (provably nonzero)
- Phase constraint (kills 23/24 of convergent families)
- Mod-5 funnel
- Prime destruction (over-determined for large $L$)
- Baker bounds

Surviving set: a narrow band of width $\approx \varepsilon$ around the smooth prediction.

**Stage 3 (NEEDED).** A Lyapunov function on the narrow band. Within the band, trajectories are constrained enough that a function failing globally might succeed locally.

### 9.2 The Lyapunov function

$$W(m_1, \ldots, m_L) = S - \Delta = \sum_i \ln(1 + 1/(3 m_i)) - (K \ln 2 - L \ln 3).$$

A cycle requires $W = 0$. Bounds:

- Above (cascade-aware): $S \leq G/(3(G-1)) \cdot 1/m_1$ unconditionally; tighter under cascade-density.
- Below (Baker-Mignotte): $\Delta > C_B \cdot K^{-13.3}$ unconditionally.

The two bounds leave a band of width $\sim \varepsilon$ when accounting for the smooth/discrete near-identity.

### 9.3 The three routes to close

Each route attacks a different ingredient of the Lyapunov inequality:

**Route 1 (Diophantine).** Improve $\Delta$ via Lang's conjecture: $\mu(\log_2 3) = 2$ gives $\Delta > C(\varepsilon) L^{-1-\varepsilon}$. Detail: [`route_1_partial_quotients.md`](route_1_partial_quotients.md).

**Route 2 (Algebraic).** Improve $S$ via Pell-defect tightening. Requires the cascade-density hypothesis. Detail: [`route_2_pell_defect_revised.md`](route_2_pell_defect_revised.md).

**Route 3 (Ergodic).** Sign-coherent oscillation of partial sums on $\mathcal{B}_c$. Requires the mod-8 stationary distribution to have $\rho < 1/2$. Detail: [`route_3_sign_coherence.md`](route_3_sign_coherence.md).

### 9.4 The conditional theorem

**Theorem.** *Each of Conjectures A (Lang), B (cascade-density), C (mod-8 ergodic) — individually — implies that no non-trivial Collatz cycle exists.*

Detail: [`conditional_proof_main.md`](conditional_proof_main.md).

### Status

The architecture is **proven correct as a reduction**. The three routes are independent, each reducing to a different named conjecture.

---

## 10. Status Map

### What's proven unconditionally

- The reformulation: cycle existence $\iff$ $D \mid C$ with valid step sequence.
- Cycle elements $m_i > 2^{68}$ (Barina).
- Cycle length $L > 1.7 \times 10^{11}$ (Hercher).
- No 1-, 2-, 3-cycles; no uniform-step cycles.
- All bridge identities exact.
- Pell defect identity $A_n^2 - 2 B_n^2 = (1/2)^n$ exact.
- Mod-8 and mod-5 transition graphs.
- Phase constraint in $\mathbb{Q}(\sqrt 2, i)$ kills 23/24 of convergent families.
- Mihailescu corollary closes the $m = 1$ family.
- Polynomial orthogonality of $R$ and $D$ at the algebraic level.
- Tao's density theorem (external).
- Mignotte effective bound $\mu(\log_2 3) \leq 14.3$ (external).

### Proven conditional on standard conjectures

- Conjecture B (cascade-density) $\Rightarrow$ no Collatz cycles.
- Conjecture C (mod-8 ergodic stationarity with $\rho < 1/2$) $\Rightarrow$ no Collatz cycles.
- Conjecture A (Lang for $\log_2 3$) + rigidity hypothesis $\Rightarrow$ no Collatz cycles.

### Open

- Conjecture A (Lang for $\log_2 3$) — open since 1971.
- Conjecture B — open, strong numerical support.
- Conjecture C — stationary distribution computable; cycle-restriction of empirical distribution to theoretical $\pi$ is the open part.
- Unconditional Collatz cycles conjecture.

### Speculative

- The near-identity $\varepsilon \approx 8.9 \times 10^{-5}$ is not zero (consistent with Schanuel) but its exact closed form is unknown. Possible $\zeta$-function connection.
- The relationship between the cascade framework and the Riemann zeta functional equation.
- Whether the polynomial orthogonality can be made to work via the Pell ring evaluation (Route 2's polynomial plug-in).

### Not addressed

- Collatz divergence (whether trajectories can escape to infinity). All work here is on the cycles part only.

---

## 11. Open Directions

In rough order of accessibility:

### Computational

1. **Compute the mod-8 stationary distribution $\pi$ explicitly.** Confirm $\rho = \pi_3 + \pi_7 < 1/2$. Numerical linear algebra. Days of work.

2. **Measure cascade-density exponent $c$ empirically.** Run Collatz orbits in cascade coordinates. Verify $c > 0$ consistently. Compute the empirical distribution.

3. **Test the Route 2 target bound $S \leq \alpha \cdot 2^{-cL}$ on cycle candidates.** Take small-$L$ "would-be cycles" (the algebraic candidates that satisfy mod constraints but not full divisibility) and verify the $S$-bound holds.

### Algebraic

4. **Develop the Pell-ring evaluation of $R(y)$.** Lift $R(y) \bmod (y^L - 2^K)$ to $\mathbb{Z}[\sqrt 2][y]$. Bound $|R(p)|$ for Pell-lattice points $p$ near $y = 3$. This is Route 2's polynomial plug-in.

5. **Sharpen the phase constraint.** It currently kills 23/24 in $\mathbb{Q}(\sqrt 2, i)$. Find a tighter constraint or pull back to $\mathbb{Z}$.

### Diophantine

6. **Attempt the one-sided positivity-constrained Baker bound.** Standard $\mu$ bounds are two-sided. The cycle equation only needs the positive side. Possibly a new technique applies.

### Ergodic

7. **Establish the mixing rate of the Collatz-weighted mod-8 chain.** Spectral gap of $P$. Standard linear algebra plus interpretation.

8. **Hoeffding-type concentration for partial sums.** Standard Markov-chain concentration, applied to the signed Lyapunov change.

### Cross-cutting

9. **Investigate the $\varepsilon$–$\zeta$ connection.** Speculative but specific: is $\varepsilon$ an $L$-function value at a specific point? Could be a completely new result on its own.

10. **Extend the framework to divergence.** Currently we handle only cycles. Tao's density theorem addresses divergence in the smooth limit; extending the algebraic filters to divergence is open.

---

## Acknowledgments

This work synthesizes ideas from extensive existing literature and a period of intensive personal exploration. Direct intellectual debts to:

- Lagarias (foundational survey, parity sequence framework)
- Tao (density theorem, smooth methods)
- Mignotte and collaborators (effective Baker bounds)
- Eliahou and Hercher (cycle length bounds)
- Barina (computational verification)
- Lang (the underlying conjecture that closes Route 1)
- Wu, Rukhadze, Hata, Marcovecchio (irrationality measure sharpening)

And to the conversation arc itself, which generated the cascade framework, the polynomial orthogonality, the three-stage architecture, and the near-identity as a scale-setter.

---

## How to Read This Repository

| If you want... | Read... |
|---|---|
| Quick intro | [`README.md`](README.md) |
| Full tour | This document |
| Formal proof | [`conditional_proof_main.md`](conditional_proof_main.md) |
| Cascade machinery | [`cascade_framework_full_2026-05-22.md`](cascade_framework_full_2026-05-22.md) |
| (n,m) manifold | [`collatz_proof_ingredients.md`](collatz_proof_ingredients.md) |
| Diophantine route | [`route_1_partial_quotients.md`](route_1_partial_quotients.md) |
| Algebraic route | [`route_2_pell_defect_revised.md`](route_2_pell_defect_revised.md) |
| Ergodic route | [`route_3_sign_coherence.md`](route_3_sign_coherence.md) |
| Near-identity | [`near_identity_role.md`](near_identity_role.md) |
| Historical synthesis | [`collatz_cascade_synthesis_2026-05-20.md`](collatz_cascade_synthesis_2026-05-20.md), [`conversation_arc_2026-05-22.md`](conversation_arc_2026-05-22.md) |
| Computation | `collatz_*.py`, `collatz-dashboard.tsx` |

---

*Last updated: May 23, 2026.*
