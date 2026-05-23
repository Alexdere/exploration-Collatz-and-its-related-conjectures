# Route 2 — Pell-Defect Tightening of the Correction Sum

*Closing the Lyapunov gap by sharpening the upper bound on $S$ using the algebraic structure of $\sqrt{2}$.*

---

## Abstract

Where Route 1 sharpens the *lower* bound on $\Delta$ (the Baker gap) by attacking transcendence theory, Route 2 sharpens the *upper* bound on $S$ (the correction sum) by exploiting the algebraic structure of the Pell defect. The key observation: $\sqrt{2}$ has a periodic continued fraction (period 1: $[1; 2, 2, 2, \ldots]$), making it among the most accessible irrationals in number theory. The Collatz step ratio $3/2$ is linked to $\sqrt{2}$ via the exact identity

$$\frac{3}{2} - \sqrt{2} \;=\; \left( 1 - \frac{1}{\sqrt{2}} \right)^{\!2}.$$

This embeds Collatz into a frame where the structural constants are algebraic and exactly known, sidestepping the irrationality measure problem.

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

## 2. Why $\sqrt{2}$? The Bridge Identity

The cascade base $\sqrt{2}$ enters Collatz via an exact algebraic identity:

$$\frac{3}{2} - \sqrt{2} \;=\; \left(1 - \frac{1}{\sqrt{2}}\right)^{\!2}.$$

**Verification.** Expand the right side:

$$\left(1 - \frac{1}{\sqrt{2}}\right)^{\!2} \;=\; 1 - \frac{2}{\sqrt{2}} + \frac{1}{2} \;=\; 1 - \sqrt{2} + \frac{1}{2} \;=\; \frac{3}{2} - \sqrt{2}. \;\checkmark$$

**Intuition.** The Collatz growth ratio is $3/2$ (one $\times 3$, one $\div 2$ — the most common rung). The cascade base is $\sqrt{2}$. Their difference is the perfect square of an algebraic unit. This is not a coincidence: it says the Collatz step ratio sits at a *specific algebraic distance* from the cascade lattice, with the distance squared being itself an algebraic unit of norm $1/2$.

### Two more identities in the same family

$$\frac{9}{8} \;=\; 1 + \frac{1}{8} \;=\; 1 + \left(\frac{1}{2}\right)^{\!3}.$$

Note $9/8 = (3/2)^2 / 2$. So the "square of the growth ratio, divided by the contraction" is *exactly* $1 + (1/2)^3$. The cascade has the growth-squared/contraction ratio at a precise 2-adic offset from unity.

$$\ln 3 \;=\; \frac{3}{2} \ln 2 \,+\, \frac{1}{2} \ln \frac{9}{8}.$$

This rewrites $\ln 3$ as a $\sqrt{2}$-friendly linear combination. The first term is the Pell convergent $3/2$ times $\ln 2$; the second is the exact correction. Substituting into the Baker gap:

$$K \ln 2 - L \ln 3 \;=\; \left( K - \frac{3L}{2} \right) \ln 2 \;-\; \frac{L}{2} \ln \frac{9}{8}.$$

This is a linear form in $\ln 2$ and $\ln(9/8)$. The number $9/8 = 3^2 / 2^3$ has *purely* prime-2-and-3 structure. The substitution isolates a "Pell residual" whose 2-adic profile is much more transparent than $\ln 3$ itself.

---

## 3. The Pell Defect

The Pell equation $x^2 - 2 y^2 = \pm 1$ has infinitely many integer solutions:

$$(x, y) = (1, 0), \,(1, 1), \,(3, 2), \,(7, 5), \,(17, 12), \,(41, 29), \,(99, 70), \,\ldots$$

These come from powers of the fundamental unit $1 + \sqrt{2}$:

$$(1 + \sqrt{2})^{n} \;=\; x_n + y_n \sqrt{2}, \qquad x_n^{\,2} - 2 y_n^{\,2} = (-1)^{n}.$$

The **dual identity**, using $1 - 1/\sqrt{2}$ (which has algebraic norm $1/2$):

$$\left( 1 - \frac{1}{\sqrt{2}} \right)^{\!n} \;=\; A_n - B_n \sqrt{2}, \qquad A_n^{\,2} - 2 B_n^{\,2} \;=\; \left(\frac{1}{2}\right)^{\!n}.$$

This is the **Pell defect identity**. The number $1 - 1/\sqrt{2} \approx 0.293$ has algebraic norm $1/2$, so its powers have norm $1/2^n$. The defect $A_n^{\,2} - 2 B_n^{\,2}$ measures how close the rational $A_n / B_n$ is to $\sqrt{2}$:

$$\frac{A_n^{\,2}}{B_n^{\,2}} - 2 \;=\; \frac{(1/2)^n}{B_n^{\,2}}, \qquad \left| \frac{A_n}{B_n} - \sqrt{2} \right| \;\approx\; \frac{(1/2)^n}{2 \sqrt{2} \cdot B_n^{\,2}}.$$

**The Pell approximations to $\sqrt{2}$ converge exponentially in $n$.**

This is fundamentally different from $\log_2 3$, where the convergent approximations are only polynomially fine. The Pell structure provides a *known, exact, exponentially-fine* algebraic ruler.

### Why this matters for Collatz

Collatz's transcendental obstruction is $\log_2 3$. But the cascade framework reformulates Collatz with $\sqrt{2}$ as the structural constant. The cascade obstruction is the *deviation* of $\log_2 3$ from the Pell lattice — and that deviation has an algebraic part (which the Pell defect controls exactly) plus a transcendental residual (which is the only thing left to bound).

This is the reformulation strategy: replace the unknown CF of $\log_2 3$ with the known CF of $\sqrt{2}$, plus a measurable residual.

---

## 4. Cascade Coordinates

Define the **cascade coordinate** of a positive real $v$:

$$n(v) \;:=\; 2 \log_2 v.$$

In these coordinates:

$$n(1) = 0, \quad n(2) = 2, \quad n(\sqrt{2}) = 1, \quad n(2^k) = 2k.$$

The cascade operator $\omega = (1 + i)/2$ has magnitude $|\omega| = 1/\sqrt{2}$ and angle $\pi/4$. Applying $\omega$ to a positive real scales it by $1/\sqrt{2}$, shifting $n$ by $-1$. Eight applications of $\omega$ rotate by $8 \cdot \pi/4 = 2\pi$ (full angular cycle) and scale by $(1/\sqrt{2})^{8} = 1/16$ (radial shrinkage). This is the **cascade period**.

### Collatz step in cascade coordinates

A Collatz step $m \to (3m + 1)/2^k$ becomes, in cascade coordinates,

$$n(m_{i+1}) - n(m_i) \;=\; 2 \log_2 \frac{3 + 1/m_i}{2^{k_i}}.$$

The per-step change in $n$ is twice the per-step log-ratio. Evaluating for the available $k$ values:

- $k_i = 1$: $\Delta n \approx 2 \log_2 (3/2) = 1.17$ (jump up)
- $k_i = 2$: $\Delta n \approx 2 \log_2 (3/4) = -0.83$ (small drop)
- $k_i \geq 3$: $\Delta n$ becomes increasingly negative

In cascade coordinates the orbit looks like a random walk on a 1-dimensional lattice with step sizes drawn from a 2-adically structured distribution.

---

## 5. The Pell Lattice and Orbit Embedding

The values $A_n - B_n \sqrt{2}$ for $n = 1, 2, 3, \ldots$ form a discrete sequence converging to zero exponentially. Combined with their conjugates $A_n + B_n \sqrt{2}$, they form the **Pell lattice** in $\mathbb{Q}(\sqrt{2})$:

$$\Lambda_{\text{Pell}} \;:=\; \{ a + b \sqrt{2} \,:\, a, b \in \mathbb{Z} \}.$$

Each Collatz orbit element $m_i$ embeds into $\Lambda_{\text{Pell}}$ via the cascade coordinate. The **cascade lift** assigns to $m_i$ a pair $(\alpha_i, \beta_i)$ such that

$$\log_2 m_i \;\approx\; \alpha_i + \beta_i \sqrt{2}$$

is the best Pell approximation. The **cascade residual** is

$$\varepsilon_i \;:=\; \log_2 m_i - (\alpha_i + \beta_i \sqrt{2}).$$

This residual is the part of $\log_2 m_i$ that doesn't fit the Pell lattice — the genuinely transcendental piece.

**Working hypothesis:** The per-step Collatz change, in cascade coordinates, separates into

(i) a Pell-lattice contribution (exactly known, exponentially controlled), plus

(ii) a residual depending on the $+1$ corrections.

If this separation holds with the residual controlled by the Pell defect $(1/2)^n$, we recover an exponential bound on $S$.

---

## 6. From Aggregate to Term-by-Term

Here is the **crux of Route 2** — and the place where current tools fall short.

The Pell defect identity controls *aggregate* behavior. Sums over the cascade orbit can be related to telescoping Pell expansions, giving:

$$\sum_{i=1}^{L} (A_{n_i} - B_{n_i} \sqrt{2}) \;=\; \text{[exactly computable Pell-lattice quantity]}.$$

But the Lyapunov bound needs **term-level** control on each $\ln(1 + 1/(3 m_i))$. The question:

> *Does the Pell defect give a per-term factor of the form $\ln(1 + 1/(3 m_i)) \leq (1/3 m_i) \cdot (1 - \alpha \cdot 2^{-i})$ for some $\alpha > 0$?*

### Where the bound would come from

The Pell lattice is exponentially fine: $|A_n - B_n \sqrt{2}| \sim (1/2)^{n/2}$ as $n \to \infty$. If the orbit element $m_i$ sits at cascade depth $n_i$ where the Pell approximation has error $(1/2)^{n_i / 2}$, then

$$m_i \;\geq\; 2^{n_i / 2} \quad (\text{roughly}),$$

and the $+1$ correction satisfies

$$\frac{1}{3 m_i} \;\leq\; \frac{2^{-n_i / 2}}{3}.$$

Summing:

$$S \;\leq\; \frac{1}{3} \sum_{i=1}^{L} 2^{-n_i / 2}.$$

If the cascade depths $n_i$ grow linearly with $i$ — meaning $n_i \geq c \cdot i$ for some $c > 0$ — then

$$S \;\leq\; \frac{1}{3} \sum_{i=1}^{L} 2^{-c i / 2} \;\leq\; \frac{1}{3} \cdot \frac{2^{-c/2}}{1 - 2^{-c/2}}.$$

**This is bounded independent of $L$.** Combined with Baker's lower bound on $\Delta$:

$$W \;=\; S - \Delta \;\leq\; (\text{constant}) - C_B \cdot L^{-\kappa}.$$

For $L$ sufficiently large, the Baker bound exceeds the constant, forcing $W < 0$ — contradiction.

### The gap

The above sketch assumes the orbit's cascade depths $n_i$ grow linearly. This is **not automatic**. It is a statement about how Collatz orbits distribute in cascade coordinates, and rigorously establishing it requires either:

**(a) An ergodic-theoretic result.** Under the algebraic constraints of Stage 2, the orbit's cascade depth $n_i$ grows linearly with $i$ on average, with bounded fluctuations.

**(b) A geometric result.** The Pell lattice has a uniform density property such that orbits on $\mathcal{B}_c$ must visit deeper Pell layers at a linear rate.

Neither is currently established. The standard cascade framework suggests the Pell numerators grow geometrically (with ratio $1 + \sqrt{2}$), but the Collatz orbit may sample these depths at a polynomial or even constant rate, depending on the $k$-sequence.

---

## 7. The Polynomial Orthogonality Plug-In

The polynomial picture (from the synthesis document) provides one possible bridge from "aggregate" to "term-level."

Recall: $C = P(2, 3)$ and $D = Q(2, 3)$, where

$$P(x, y) \;=\; \sum_{j=0}^{L-1} y^{L-1-j} \cdot x^{K_j}, \quad Q(x, y) \;=\; x^{K} - y^{L}.$$

With $\deg_y P = L - 1 < L = \deg_y Q$: as polynomials, $Q$ does not divide $P$. The residual

$$R(y) \;:=\; P(2, y) \;\;\text{mod}\;\; (y^{L} - 2^{K})$$

has degree $L - 1$ and is non-zero (since $P$ is not in the principal ideal $(y^{L} - 2^{K})$).

### The bridge to Route 2

The orthogonality says $R(y)$ is non-zero as a polynomial. The cycle condition says $R(3) \equiv 0 \pmod{D}$. The gap is "polynomial non-zero" vs "evaluated integer divisible."

**Move to the Pell ring.** Instead of evaluating $R$ at the integer $y = 3$, evaluate it at Pell-lattice points $p \in \Lambda_{\text{Pell}}$ near $3$. If $R$ doesn't vanish at any Pell-lattice point in a neighborhood of $y = 3$, and Pell-lattice points are dense around $3$ at scale $1/2^{n/2}$, then

$$|R(3) \,\,\text{mod}\,\, D| \;\geq\; (\text{Pell-density factor}).$$

This lower bound, propagated through the cascade lift of the cycle equation, would yield the missing per-term factor in $S$.

### Making it rigorous

This is speculative but structurally sound. It connects the algebraic (polynomial orthogonality) to the analytic (Pell lattice density) via the cycle equation. Making it rigorous requires:

(i) Defining the Pell-lift of $R(y)$ precisely as a polynomial over $\mathbb{Z}[\sqrt{2}]$.

(ii) Bounding $|R(p)|$ for $p$ a Pell-lattice point near $3$, using the degree of $R$ and the algebraic structure of $\mathbb{Z}[\sqrt{2}]$.

(iii) Translating that lower bound into a term-level upper bound on $\ln(1 + 1/(3 m_i))$ via the cascade coordinate identification.

Step (iii) is the place where ergodic theory or a quantitative equidistribution theorem would plug in.

---

## 8. The Theorem to Aim For

The clean target statement:

> **Theorem (Route 2 target).** *There exist constants $\alpha > 0$ and $c > 0$ such that for any Collatz cycle of length $L$ in the constrained band $\mathcal{B}_c$,*
> $$\sum_{i=1}^{L} \ln\!\left(1 + \frac{1}{3 m_i}\right) \;\leq\; \alpha \cdot 2^{-c L}.$$

Combined with Mignotte's bound $\Delta > C_B \cdot L^{-\kappa}$:

$$W \;>\; C_B \cdot L^{-\kappa} - \alpha \cdot 2^{-c L}.$$

For $L \geq L_0$ (computable from $C_B, \alpha, c, \kappa$), the right side is positive — so $W > 0$, contradicting $W = 0$ for a cycle. Combined with computational verification covering $L < L_0$, this closes the conjecture.

The theorem is **plausible** but **not currently proven**. The ingredients exist (Pell defect, cascade structure, polynomial orthogonality) but a complete proof requires the missing ergodic / geometric step described in §6.

---

## 9. Status and Best Entry Point

Route 2 is the most **novel** of the three. It does not rely on improving any external transcendence theorem. It exploits the *structure already present* in the cascade framework — specifically, that $\sqrt{2}$ has known, periodic, exponentially-fine continued fraction structure that $\log_2 3$ lacks.

**Advantage.** The technical objects are algebraic and computable. The Pell defect is an exact identity, not an inequality. The cascade coordinates make the orbit geometry explicit.

**Disadvantage.** The "from aggregate to term-by-term" step requires a new lemma about how Collatz orbits distribute in cascade coordinates. This may itself be hard.

**Best entry point: computational.** Take cycle candidates from the verification database (small-$L$ cycles that survive Stages 1 and 2 *in simulation* — i.e., the algebraic filters but ignoring the actual cycle non-existence). Compute their cascade-coordinate trajectories. Measure the empirical bound on $S$. If it has the form $\alpha \cdot 2^{-c L}$ with $c > 0$ consistently, that is strong evidence for the structural claim and a guide for proving it.

A related computational check: measure the empirical growth rate of cascade depth $n_i$ along Collatz orbits. If $n_i \approx c \cdot i$ with $c > 0$, that supports the ergodic hypothesis (a).

---

## 10. Notation Summary

| Symbol | Meaning |
|---|---|
| $\sqrt{2}$ | Pell base; periodic CF $[1; 2, 2, \ldots]$ |
| $A_n, B_n$ | Pell defect coefficients: $(1 - 1/\sqrt{2})^n = A_n - B_n \sqrt{2}$ |
| $(1/2)^n$ | The exact Pell defect: $A_n^2 - 2 B_n^2$ |
| $n(v)$ | Cascade coordinate: $2 \log_2 v$ |
| $\omega$ | Cascade operator $(1+i)/2$; $\|\omega\| = 1/\sqrt{2}$, $\arg(\omega) = \pi/4$ |
| $\Lambda_{\text{Pell}}$ | Pell lattice in $\mathbb{Q}(\sqrt{2})$ |
| $G$ | Geometric mean $3/(2\sqrt{2}) = \sqrt{9/8}$ |
| $\mathcal{B}_c$ | Constrained band surviving Stages 1 and 2 |
| $P, Q$ | Two-variable polynomials with $C = P(2,3), D = Q(2,3)$ |
| $R(y)$ | $P(2, y) \bmod (y^L - 2^K)$ — the cycle residual |

## 11. References

- Bridge identity $3/2 - \sqrt{2} = (1 - 1/\sqrt{2})^2$: established in collatz_proof_ingredients.md §9, Bridge Identities.
- Pell algebra and the unit $1 + \sqrt{2}$: Hardy and Wright, *An Introduction to the Theory of Numbers*, Ch. 10.
- Cascade framework and cascade coordinates: cascade_framework_full_2026-05-22.md.
- Polynomial orthogonality of $C$ and $D$: synthesis 2026-05-23, §"Polynomial Orthogonality."
- Ergodic theory of $\mathbb{Z}_2$-Collatz: Lagarias (1985), "The $3x+1$ problem: an annotated bibliography."
