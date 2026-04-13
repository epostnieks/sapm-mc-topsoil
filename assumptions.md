# Monte Carlo Assumptions — Topsoil Erosion / Pedogenesis Floor

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $255.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 4.41 | Confirmed by N=100,000 draws |
| ΔW median (result) | $1,123.4B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_carbon_release` | lognormal | $138.0B | $230.0B | $345.0B | $230B/yr; 0.8-1.2 Pg C/yr released, SCC at $51/tCO2 |
| `C2_water_retention_loss` | lognormal | $108.0B | $180.0B | $270.0B | $180B/yr; 1% SOM = 20K gal/acre storage, 40-60% OC lost |
| `C3_nutrient_replacement` | lognormal | $99.0B | $165.0B | $248.0B | $165B/yr; N2O from synthetic fertilizer, P reserve depletion |
| `C4_biodiversity_collapse` | lognormal | $78.0B | $130.0B | $195.0B | $130B/yr; mycorrhizal disruption, 10B organisms per teaspoon |
| `C5_downstream_sedimentation` | lognormal | $72.0B | $120.0B | $180.0B | $120B/yr; reservoir sedimentation, Gulf hypoxia, water costs |
| `C6_subsidy_lock_in` | lognormal | $168.0B | $280.0B | $420.0B | $280B/yr; CAP/Farm Bill subsidies maintaining tillage dependency |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 1.8 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 1.8) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 4.33 | 20% DC adj = 3.47 | 40% DC adj = 2.6

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $1,123B = 1.1% of world GDP ($106T) ✓
- **β_W range**: 4.41 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
