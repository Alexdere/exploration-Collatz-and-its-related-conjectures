# Collatz — A Reduction Framework

A research framework for the cycles part of the Collatz conjecture, developed through intensive exploration in May 2026.

## The Main Result

The non-existence of non-trivial Collatz cycles is **reduced to a disjunction of three named conjectures**. Each of:

- **Conjecture A** — Lang's conjecture for $\log_2 3$ (Diophantine approximation, 1971)
- **Conjecture B** — Cascade-density hypothesis (algebraic dynamics)
- **Conjecture C** — Mod-8 ergodic stationarity (Markov chain theory)

is independently sufficient to rule out non-trivial Collatz cycles. Any progress on any one of these conjectures advances Collatz.

See [`conditional_proof_main.md`](conditional_proof_main.md) for the formal statement and proof.

## What This Is

A **reduction theorem**. The framework clarifies the structure of the obstacle: whatever specifically makes Collatz cycles hard is not a single inscrutable wall, but a *choice between three reductions* to known-hard open problems in three different branches of mathematics.

## What This Is Not

- This is **not a solution** to Collatz. The three conjectures are themselves open.
- This **does not address divergence** — only the cycles part. Whether trajectories can escape to infinity is a separate problem.
- This **is not a single new theorem** — it is a body of organizing work that makes the obstacle precise.

## Quick Tour

If you have 5 minutes:
- Read [`PROJECT_OVERVIEW.md`](PROJECT_OVERVIEW.md) §1 and §10 (the geometric reframing and final status).

If you have 30 minutes:
- Read [`PROJECT_OVERVIEW.md`](PROJECT_OVERVIEW.md) in full.

If you want the formal claim:
- Read [`conditional_proof_main.md`](conditional_proof_main.md).

If you want the cascade framework:
- Read [`cascade_framework_full_2026-05-22.md`](cascade_framework_full_2026-05-22.md).

If you want a specific route:
- Route 1 (Lang/Diophantine): [`route_1_partial_quotients.md`](route_1_partial_quotients.md)
- Route 2 (Pell-defect): [`route_2_pell_defect_revised.md`](route_2_pell_defect_revised.md)
- Route 3 (ergodic): [`route_3_sign_coherence.md`](route_3_sign_coherence.md)

## File Map

### Top-level

- [`README.md`](README.md) — this file
- [`PROJECT_OVERVIEW.md`](PROJECT_OVERVIEW.md) — comprehensive tour of every approach tried
- [`conditional_proof_main.md`](conditional_proof_main.md) — formal conditional proof using Conjectures A, B, or C

### The three routes

- [`route_1_partial_quotients.md`](route_1_partial_quotients.md) — improve the Baker bound via Lang
- [`route_2_pell_defect_revised.md`](route_2_pell_defect_revised.md) — tighten the correction sum via Pell algebra
- [`route_3_sign_coherence.md`](route_3_sign_coherence.md) — close the gap via ergodic theory

### Foundational framework

- [`cascade_framework_full_2026-05-22.md`](cascade_framework_full_2026-05-22.md) — cascade operator $\omega = (1+i)/2$, Pell algebra, bridge identities
- [`collatz_proof_ingredients.md`](collatz_proof_ingredients.md) — cycle equation, $(n, m)$ manifold, mod constraints
- [`near_identity_role.md`](near_identity_role.md) — the role of $\varepsilon \approx 8.9 \times 10^{-5}$

### Historical / synthesis

- [`collatz_cascade_synthesis_2026-05-20.md`](collatz_cascade_synthesis_2026-05-20.md) — earlier synthesis
- [`conversation_arc_2026-05-22.md`](conversation_arc_2026-05-22.md) — exploration log
- [`collatz-proof-attempt.md`](collatz-proof-attempt.md) — initial proof attempt
- [`collatz-formalization.md`](collatz-formalization.md) — formalization notes

### Computational

- [`collatz_engine.py`](collatz_engine.py) — core dynamics
- [`collatz_convergents.py`](collatz_convergents.py) — convergent computation
- [`collatz_coherence.py`](collatz_coherence.py) — coherence checks
- [`collatz_pell_propagation.py`](collatz_pell_propagation.py) — Pell propagation
- [`collatz_deep_analysis.py`](collatz_deep_analysis.py) — deep analysis tools
- [`collatz-dashboard.tsx`](collatz-dashboard.tsx) — interactive dashboard
- [`run_all.sh`](run_all.sh) — driver script

## Status at a Glance

| Component | Status |
|---|---|
| Reduction theorem (cycles → A or B or C) | **Proven**, modulo §4' caveat on (A) |
| Cycle equation $m_1 \cdot D = C$ | Proven |
| Phase constraint (kills 23/24 of families) | Proven |
| Bridge identity $3/2 - \sqrt{2} = (1 - 1/\sqrt{2})^2$ | Proven, exact |
| Cycle length $L > 1.7 \times 10^{11}$ | Proven (Hercher) |
| Cycle elements $m_i > 2^{68}$ | Proven (Barina) |
| Conjecture A (Lang for $\log_2 3$) | Open since 1971 |
| Conjecture B (cascade-density) | Open; strong numerical support |
| Conjecture C (mod-8 ergodic) | Mostly computable; mixing rigorous |
| Near-identity $\varepsilon \approx 8.9 \times 10^{-5}$ | Verified numerically; not exact (Schanuel) |
| **Collatz cycles unconditional** | **Open** |
| Collatz divergence | Not addressed in this framework |

## Key Numerical Facts

- **$\log_2 3 \approx 1.5849625$**, transcendental (Gelfond–Schneider 1934). Continued fraction: $[1; 1, 1, 2, 2, 3, 1, 5, 2, 23, \ldots]$.
- **$\mu(\log_2 3) \leq 5.117$** unconditionally (Wu, 2003). Conjecturally $\mu = 2$ (Lang).
- **$\varepsilon = (3/4)\sqrt{\pi} + \log_2(3) - 3/2 - \sqrt{2} \approx 8.93 \times 10^{-5}$**. Not zero.
- **$L_E = 1.7 \times 10^{11}$**, Hercher's cycle length lower bound (2020).
- **$M_v = 2^{68}$**, Barina's verification bound (2020).
- **$G = 3/(2\sqrt{2}) \approx 1.0607$**, Collatz geometric mean.

## How to Cite

If this framework is useful for your own work:

> *Conditional reduction of the Collatz cycles conjecture to three independent open problems (Lang's conjecture for $\log_2 3$, the cascade-density hypothesis, or mod-8 ergodic stationarity). [Repository URL].*

## Standing on the Shoulders Of

This work directly builds on:

- **Lagarias, J. (1985).** "The 3x+1 problem: An annotated bibliography." Foundational survey.
- **Mignotte, M. (1999); Laurent–Mignotte–Nesterenko (1995).** Effective bounds on linear forms in two logarithms.
- **Eliahou, S. (1993); Hercher, C. (2020).** Cycle length lower bounds.
- **Barina, D. (2020).** Computational verification to $2^{68}$.
- **Tao, T. (2019).** "Almost all orbits of the Collatz map attain almost bounded values." arXiv:1909.03562.
- **Wu, Q. (2003).** Sharpening the irrationality measure of $\log_2 3$.

## A Note on Honesty

The conditional proof under Conjecture A (Lang) has an additional rigidity caveat — see §4' of [`conditional_proof_main.md`](conditional_proof_main.md). Lang alone gives strong bounds on cycle structure but does not by itself rule out exotic divisibility coincidences at very large $L$. Conjectures B and C give complete conditional proofs without this caveat.

The near-identity $\varepsilon \approx 8.9 \times 10^{-5}$ is a numerical observation, not a theorem. By Schanuel's conjecture (and consistent with numerical evidence to high precision), $\varepsilon$ is a definite nonzero transcendental number. Its smallness organizes the proof architecture but is not itself a proof tool.

## License

[MIT / Apache 2.0 / CC-BY — choose appropriate]

---

*Last updated: May 23, 2026.*
