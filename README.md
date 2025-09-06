# Dynamically Faithful ML Emulators for Chaotic Dynamics (Lorenz–96)

**TL;DR**: We study when machine-learning emulators reproduce the *dynamical* behavior of a chaotic system—not just one-step accuracy. Using Lorenz–96, we compare direct next-state models to **increment prediction with Adams–Bashforth 3 (ΔX+AB3)**, analyze **memory length \(q\)** in LSTMs, and test **training regimes** (single-regime, mixed-regime, and explicit conditioning on the forcing \(F\)). We propose a **chaos-aware evaluation suite** that cleanly separates short-term error from long-horizon divergence.

---

## What this project is about

Modern ML surrogates can nail one-step forecasts yet drift off-attractor during long rollouts. We provide:
- A **taxonomy** of exposure modes (single-implicit per \(F\), multiple-implicit mixed \(F\), and multiple-explicit with \(F\) as input) and targets (direct \(X\) vs. **ΔX+AB3** hybridization).
- A **chaos-aware evaluation suite**: perturbation-ensemble **\(\alpha/\gamma\) maps**, fixed-\(t_0\) ensemble-RMSE curves, and component-wise ensemble envelopes.
- A **three-measure procedure** to choose LSTM lookback \(q\) that balances short-term accuracy with dynamical faithfulness.

---

## Key findings (practitioner’s takeaways)

- **Prefer ΔX+AB3** for per-\(F\) deployment: lower early error, better saturation fidelity, and preserved qualitative structure.
- **Explicit \(F\) helps**: conditioning on \(F\) stabilizes training across regimes and removes late re-growth in mixed-regime settings.
- **Short-memory LSTM-X** is robust in mixed-regime training without \(F\), maintaining a sustained error plateau by inferring regime from context.
- **Lookback matters but is regime-dependent**: our three-measure selection yields \(q^\star\) that is accurate *and* dynamically faithful—longer isn’t always better.
- Always report standard metrics **and** chaos-aware diagnostics; one-step MAE/RMSE alone is insufficient for chaotic rollouts.

---

## Repository status

This is a **temporary research repository** with analysis code used to generate figures and diagnostics for the study. A more polished release (with full training/evaluation pipelines and docs) may follow.

---

## Getting started

> Minimal environment (illustrative):
- Python ≥ 3.10  
- NumPy, SciPy, PyTorch (or JAX), Matplotlib  
- TQDM, Pandas

Clone and create an environment of your choice, then install the usual scientific Python stack. Data for Lorenz–96 can be generated on the fly (deterministic ODE with chosen \(F\), step size, and integrator). We recommend:
- Many short trajectories with held-out initial conditions
- Physical-unit scoring after inverse normalization
- Fixed seeds for reproducibility where appropriate

---

## Cite this work

If you use these ideas, diagnostics, or procedures, please cite the paper:

```bibtex
@article{YourLastName2025DynamicalFaithfulness,
  title   = {From One‑Step Accuracy to Dynamical Faithfulness: Chaos‑Aware Emulation of Lorenz–96 with ANN/LSTM and Increment–AB3 Rollouts},
  author  = {Jialin Chen, Sara Shamekh},
  journal = {arXiv (not published)},
  year    = {2025},
  eprint  = {TBD},
  url     = {TBD}
}
