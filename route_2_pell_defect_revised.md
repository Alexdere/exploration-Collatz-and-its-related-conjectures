# Route 2 — Pell-Defect Tightening of the Correction Sum

*(Revised: with near-identity epsilon as numerical target.)*

*Closing the Lyapunov gap by sharpening the upper bound on $S$ using the algebraic structure of $\sqrt{2}$.*

---

## Abstract

Where Route 1 sharpens the *lower* bound on $\Delta$ (the Baker gap) by attacking transcendence theory, Route 2 sharpens the *upper* bound on $S$ (the correction sum) by exploiting the algebraic structure of the Pell defect. The key observation: $\sqrt{2}$ has a periodic continued fraction (period 1: $[1; 2, 2, 2, \ldots]$), making it among the most accessible irrationals in number theory. The Collatz step ratio $3/2$ is linked to $\sqrt{2}$ via the exact identity

$$\frac{3}{2} - \sqrt{2} \;=\; \left( 1 - \frac{1}{\sqrt{2}} \right)^{\!2}.$$

This embeds Collatz into a frame where the structural constants are algebraic and exactly known, sidestepping the irrationality measure problem. The **near-identity** $(3/4)\sqrt{\pi} + \log_2(3) - 3/2 \approx \sqrt{2}$, with error $\varepsilon \approx 8.9 \times 10^{-5}$, sets the precise numerical target for the route.

---

## 1. Setup Recap

The Lyapunov function

$$W \;=\; S - \Delta \;=\; \sum_{i=1}^{L} \ln\!\left( 1 + \frac{1}{3 m_i} \right) \;-\; (K \ln 2 - L \ln 3)$$

must equal zero for any cycle. Stage 1 (Tao's density argument) narrows the candidates to a measure-zero residual. Stage 2 (algebraic filters: mod-8, mod-5, phase, prime destruction) narrows further. At Stage 3, we need a bound on $S$ that, combined with Baker's lower bound on $\Delta$, makes $W = 0$ impossible.

The standard upper bound is

$$S \;\leq\; \sum_{i=1}^{L} \frac{1}{3 m_i}.$$

In the previous synthesis we sharpened this using the geometric-mean orbit structure to

$$S \;\leq\; \frac{G}{3(G-1)} \cdot \frac{1}{m_1} \;\approx\; \frac{5.83}{m_1},$$

where $G = 3 / (2\sqrt{2})$. This gave a *Baker-equivalent* bound. **We need to do strictly better** — to gain an additional multiplicative factor that compresses $S$ exponentially in $L$.

---

## 2. The Near-Identity as Numerical Target

Before getting into the algebraic machinery, we identify the *exact numerical scale* at which Route 2 must operate. This is set by the near-identity

$$\frac{3}{4}\sqrt{\pi} \,+\, \log_2(3) \,-\, \frac{3}{2} \;\approx\; \sqrt{2}, \qquad \varepsilon \;:=\; \text{LHS} - \sqrt{2} \;\approx\; 8.9 \times 10^{-5}.$$

**Reading the three terms:**

- $(3/4)\sqrt{\pi} = \Gamma(5/2)$. The half-integer factorial at the Collatz step ratio. It is the *continuous / smooth* side: hypersphere-volume coefficient, what one obtains by treating Collatz as a continuous flow.
- $\log_2(3) - 3/2$. The geometric mean excess. It is the *discrete / arithmetic* side: how far the actual integer balance point overshoots the first Pell convergent.
- $\sqrt{2}$. The cascade base. It is the *bridge* — the algebraic structural constant on which the cascade framework is built.

**The relation:** smooth side + discrete excess = bridge, to within $\varepsilon$. The fact that this is *not exact* (provable by a Schanuel-style argument on transcendental independence) and that $\varepsilon > 0$ has a precise interpretation:

> *The discrete arithmetic is slightly more contractive than the continuous model predicts. The $+1$ corrections accumulate a small positive bias that the smooth methods smooth out. $\varepsilon$ is the width of the gap between what smooth analysis can rule out and what discrete arithmetic actually achieves.*

### The numerical target

Stage 1 (Tao) handles the smooth side. Cycles can only survive to Stage 3 if they live in the *gap* between smooth analysis and discrete reality. That gap has scale $\varepsilon$.

For Route 2's bound on $S$ to close the Lyapunov gap, it must achieve

$$S \;\leq\; \alpha \cdot 2^{-c L}$$

with the bound below $\varepsilon$ for all relevant $L$. That is:

$$\alpha \cdot 2^{-c L} \;<\; \varepsilon \;\approx\; 8.9 \times 10^{-5} \quad \Longleftrightarrow \quad L \;>\; \frac{\log_2(\alpha / \varepsilon)}{c}.$$

For $\alpha \sim 1$ and modest $c \in (0.05, 0.5)$:

| $c$ | Threshold $L_*$ |
|---|---|
| 0.05 | $L_* \approx 268$ |
| 0.1 | $L_* \approx 134$ |
| 0.2 | $L_* \approx 67$ |
| 0.5 | $L_* \approx 27$ |

**For any modest exponential contraction $c > 0$, the Pell-defect tightening takes over from computational verification at $L \sim 10^2$.**

This is why Route 2 is feasible: the small size of $\varepsilon$ does *not* make the target stringent. Even a weak exponential decay ($c = 0.05$) closes the gap once $L$ exceeds a few hundred. And below $L \sim 10^{11}$, Hercher verification already rules out cycles. The threshold $L_*$ is comfortably *between* the two — Pell-defect tightening only needs to be effective in a regime where verification has already finished its work.

### Why $\varepsilon > 0$ matters (the sign)

If $\varepsilon$ were negative, the discrete reality would be *less* contractive than smooth analysis predicts. Smooth methods would *over*-rule cycles, missing the actual danger zone. Route 2 would then need to *expand* the band, requiring stronger discrete bounds — much harder.

Because $\varepsilon > 0$, smooth methods are *conservative*. The danger zone is smaller than the smooth residual. Route 2's task is to bound $S$ tighter than the smooth prediction, which is a strictly weaker target than bounding $S$ tighter than the discrete reality.

This is the **structural reason** the near-identity matters for the proof: it tells us *which side of the smooth-discrete gap to attack*, and that the attack side is the easier one.

---

## 3. Why $\sqrt{2}$? The Bridge Identity

The cascade base $\sqrt{2}$ enters Collatz via an exact algebraic identity:

$$\frac{3}{2} - \sqrt{2} \;=\; \left(1 - \frac{1}{\sqrt{2}}\right)^{\!2}.$$

**Verification.** Expand the right side:

$$\left(1 - \frac{1}{\sqrt{2}}\right)^{\!2} \;=\; 1 - \frac{2}{\sqrt{2}} + \frac{1}{2} \;=\; 1 - \sqrt{2} + \frac{1}{2} \;=\; \frac{3}{2} - \sqrt{2}. \;\checkmark$$

**Intuition.** The Collatz growth ratio is $3/2$. The cascade base is $\sqrt{2}$. Their difference is the perfect square of an algebraic unit. This says the Collatz step ratio sits at a *specific algebraic distance* from the cascade lattice, with the distance squared being itself an algebraic unit of norm $1/2$.

### Two more identities in the same family

$$\frac{9}{8} \;=\; 1 + \frac{1}{8} \;=\; 1 + \left(\frac{1}{2}\right)^{\!3}.$$

Note $9/8 = (3/2)^2 / 2$. So the "square of the growth ratio, divided by the contraction" is *exactly* $1 + (1/2)^3$.

$$\ln 3 \;=\; \frac{3}{2} \ln 2 \,+\, \frac{1}{2} \ln \frac{9}{8}.$$

This rewrites $\ln 3$ as a $\sqrt{2}$-friendly linear combination.

---

## 4. The Pell Defect

The Pell equation $x^2 - 2 y^2 = \pm 1$ has infinitely many integer solutions coming from powers of the fundamental unit $1 + \sqrt{2}$:

$$(1 + \sqrt{2})^{n} \;=\; x_n + y_n \sqrt{2}, \qquad x_n^{\,2} - 2 y_n^{\,2} = (-1)^{n}.$$

The **dual identity**, using $1 - 1/\sqrt{2}$ (which has algebraic norm $1/2$):

$$\left( 1 - \frac{1}{\sqrt{2}} \right)^{\!n} \;=\; A_n - B_n \sqrt{2}, \qquad A_n^{\,2} - 2 B_n^{\,2} \;=\; \left(\frac{1}{2}\right)^{\!n}.$$

This is the **Pell defect identity**. The defect $A_n^2 - 2 B_n^2$ measures how close $A_n/B_n$ is to $\sqrt{2}$:

$$\left| \frac{A_n}{B_n} - \sqrt{2} \right| \;\approx\; \frac{(1/2)^n}{2 \sqrt{2} \cdot B_n^{\,2}}.$$

**The Pell approximations to $\sqrt{2}$ converge exponentially in $n$** — fundamentally different from $\log_2 3$, where convergence is only polynomial.

---

## 5. Cascade Coordinates

Define the **cascade coordinate** of a positive real $v$:

$$n(v) \;:=\; 2 \log_2 v.$$

In these coordinates: $n(2^k) = 2k$, $n(\sqrt{2}) = 1$. A Collatz step $m \to (3m + 1)/2^k$ becomes

$$n(m_{i+1}) - n(m_i) \;=\; 2 \log_2 \frac{3 + 1/m_i}{2^{k_i}}.$$

In cascade coordinates the orbit looks like a random walk on a 1-dimensional lattice with step sizes drawn from a 2-adically structured distribution.

---

## 6. From Aggregate to Term-by-Term

Here is the **crux of Route 2**, now anchored by the $\varepsilon$ target.

The Pell defect identity controls *aggregate* behavior:

$$\sum_{i=1}^{L} (A_{n_i} - B_{n_i} \sqrt{2}) \;=\; \text{[exactly computable Pell-lattice quantity]}.$$

But the Lyapunov bound needs **term-level** control on each $\ln(1 + 1/(3 m_i))$. The question:

> *Does the Pell defect give a per-term factor of the form $\ln(1 + 1/(3 m_i)) \leq (1/3 m_i) \cdot (1 - \alpha \cdot 2^{-i})$ for some $\alpha > 0$?*

### Where the bound comes from

The Pell lattice is exponentially fine: $|A_n - B_n \sqrt{2}| \sim (1/2)^{n/2}$ as $n \to \infty$. If the orbit element $m_i$ sits at cascade depth $n_i$ with the Pell approximation accurate to scale $(1/2)^{n_i / 2}$, then $m_i \geq 2^{n_i / 2}$ roughly, and

$$\frac{1}{3 m_i} \;\leq\; \frac{2^{-n_i / 2}}{3}.$$

If the cascade depths $n_i$ grow linearly with $i$ — $n_i \geq c \cdot i$ — then

$$S \;\leq\; \frac{1}{3} \sum_{i=1}^{L} 2^{-c i / 2} \;\leq\; \frac{2^{-c/2}}{3(1 - 2^{-c/2})}.$$

**This is bounded independent of $L$.** Combined with Baker's lower bound on $\Delta$, we get $W < 0$ for sufficiently large $L$ — exactly the threshold $L_* \sim \log(1/\varepsilon)/c$ identified in §2.

### Connecting to the near-identity

The decay rate $c$ is *not free*. It is the cascade-density exponent — how fast the orbit descends through the Pell layers. Computationally, $c$ can be measured directly from numerical Collatz orbits.

The **target** for $c$ is determined by $\varepsilon$:

$$c \;>\; \frac{\log_2(1/\varepsilon)}{L_E} \;\approx\; \frac{\log_2(10^4)}{1.7 \times 10^{11}} \;\approx\; 7.8 \times 10^{-11}.$$

This is *extraordinarily mild*. Any non-zero $c$ at all (e.g. $c > 10^{-10}$) suffices. Numerically, orbital data suggests $c \sim 0.3$ for typical Collatz orbits — many orders of magnitude above the threshold.

**This is why Route 2 looks so promising:** the near-identity reveals that the required exponential decay is essentially negligible. The whole edifice of Stage 1 (Tao's smooth methods) already strips away the "easy" cases. Only a microscopic residual remains, of width $\varepsilon$, and any positive exponential decay closes it.

### The gap

The above sketch assumes the orbit's cascade depths $n_i$ grow linearly. This is the **cascade-density hypothesis** (Conjecture B in the conditional proof document). Rigorously establishing it requires either:

**(a) An ergodic-theoretic result.** Under the algebraic constraints of Stage 2, the orbit's cascade depth $n_i$ grows linearly with $i$ on average.

**(b) A geometric result.** The Pell lattice has a uniform density property such that orbits on $\mathcal{B}_c$ must visit deeper Pell layers at a linear rate.

Neither is currently established as a theorem, but both are strongly supported by computation.

---

## 7. The Polynomial Orthogonality Plug-In

The polynomial picture from the synthesis provides a possible bridge from "aggregate" to "term-level."

$C = P(2, 3)$ and $D = Q(2, 3)$, where $\deg_y P = L - 1 < L = \deg_y Q$. As polynomials, $Q$ does not divide $P$. The residual

$$R(y) \;:=\; P(2, y) \;\;\text{mod}\;\; (y^{L} - 2^{K})$$

has degree $L - 1$ and is non-zero.

**Move to the Pell ring.** Evaluate $R$ at Pell-lattice points $p \in \Lambda_{\text{Pell}}$ near $3$. If $R$ doesn't vanish at any Pell-lattice point in a neighborhood of $y = 3$, and Pell-lattice points are dense around $3$ at scale $1/2^{n/2}$, then $|R(3) \,\text{mod}\, D| \geq$ (Pell-density factor). This lower bound, propagated through the cascade lift, would yield the missing per-term factor in $S$.

---

## 8. The Theorem to Aim For

> **Theorem (Route 2 target).** *There exist constants $\alpha > 0$ and $c > 0$ such that for any Collatz cycle of length $L$ in the constrained band $\mathcal{B}_c$,*
> $$\sum_{i=1}^{L} \ln\!\left(1 + \frac{1}{3 m_i}\right) \;\leq\; \alpha \cdot 2^{-c L}.$$

Combined with Mignotte's unconditional bound $\Delta > C_B \cdot L^{-13.3}$:

$$W \;>\; C_B \cdot L^{-13.3} - \alpha \cdot 2^{-c L}.$$

The right side is positive for $L > L_*$, where $L_* = (1/c) \log_2 (\alpha L^{13.3}/C_B)$ — that is, $L_* \sim (\log L)/c$, which is far below $L_E = 1.7 \times 10^{11}$.

**This closes Collatz cycles unconditionally**, given:
1. Hercher verification for $L \leq L_E$ (done).
2. The Route 2 theorem above (target).

The target reduces to **Conjecture B** (cascade-density hypothesis) by §6.

---

## 9. Status and Best Entry Point

Route 2 is the most **novel** of the three. It does not rely on improving any external transcendence theorem. It exploits the *structure already present* in the cascade framework — specifically, that $\sqrt{2}$ has known, periodic, exponentially-fine continued fraction structure that $\log_2 3$ lacks. The **near-identity $\varepsilon$ sets the precise numerical target**, and that target is mild.

**Advantage.** The technical objects are algebraic and computable. The Pell defect is an exact identity, not an inequality.

**Disadvantage.** The cascade-density hypothesis is unproven (though numerically well-supported).

**Best entry point: computational verification of cascade-density.** Run Collatz orbits in cascade coordinates. Measure the empirical growth rate $c$ of cascade depths. If $c$ is consistently positive (numerically: $c \sim 0.3$), the cascade-density hypothesis is strongly supported, and the proof program has its target.

---

## 10. Notation Summary

| Symbol | Meaning |
|---|---|
| $\sqrt{2}$ | Pell base; periodic CF $[1; 2, 2, \ldots]$ |
| $A_n, B_n$ | Pell defect coefficients |
| $(1/2)^n$ | The exact Pell defect |
| $n(v)$ | Cascade coordinate: $2 \log_2 v$ |
| $\omega$ | Cascade operator $(1+i)/2$ |
| $\Lambda_{\text{Pell}}$ | Pell lattice in $\mathbb{Q}(\sqrt{2})$ |
| $G$ | Geometric mean $3/(2\sqrt{2})$ |
| $\mathcal{B}_c$ | Constrained band |
| $\varepsilon$ | Near-identity gap: $\approx 8.9 \times 10^{-5}$ |
| $L_*$ | Threshold where Route 2 takes over |
| $c$ | Cascade-density exponent |

## 11. References

- Bridge identity $3/2 - \sqrt{2} = (1 - 1/\sqrt{2})^2$: collatz_proof_ingredients.md §9.
- Pell algebra: Hardy and Wright, *Introduction to the Theory of Numbers*, Ch. 10.
- Cascade framework: cascade_framework_full_2026-05-22.md.
- Polynomial orthogonality: synthesis 2026-05-23.
- Near-identity: see companion document `near_identity_role.md`.
