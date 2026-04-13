# SAPM Monte Carlo — Topsoil Erosion / Pedogenesis Floor

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Topsoil Erosion (Pedogenesis Floor).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **4.41** |
| β_W mean | 4.47 |
| β_W std | 0.73 |
| **90% CI** | **[3.4, 5.8]** |
| 99% CI | [3.0, 6.4] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$1,123.4B/yr** |
| Π (revenue) | $255.0B/yr |

**β_W = 4.41** means the topsoil erosion industry destroys **$4.41 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 1 — Impossibility

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-topsoil.git
cd sapm-mc-topsoil
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 4.41` and `ΔW median : $1,123.4B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_carbon_release | $229.7B | [$152.9B, $344.5B] | Lognormal |
| C2_water_retention_loss | $179.9B | [$119.8B, $270.8B] | Lognormal |
| C3_nutrient_replacement | $164.9B | [$109.8B, $247.9B] | Lognormal |
| C4_biodiversity_collapse | $130.1B | [$86.6B, $194.8B] | Lognormal |
| C5_downstream_sedimentation | $119.8B | [$80.1B, $179.4B] | Lognormal |
| C6_subsidy_lock_in | $279.7B | [$186.8B, $420.0B] | Lognormal |
| **Total ΔW** | **$1,123.4B** | **[$862.2B, $1,468.4B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 1.8 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Topsoil Erosion (Pedogenesis Floor)*.
> GitHub: epostnieks/sapm-mc-topsoil.
> https://github.com/epostnieks/sapm-mc-topsoil
