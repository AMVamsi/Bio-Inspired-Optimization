# Bio-Inspired Optimization for Insulin Planning

This repository contains a research notebook that explores glucose-control strategies using multiple simulation and optimization approaches:

- Rule-based/discrete glucose update models
- Mini Bergman-inspired glucose-insulin dynamics
- Hybrid ODE glucose model
- Evolutionary search (genetic algorithms) for intervention planning

The core artifact is [Insulin_Optimization.ipynb](Insulin_Optimization.ipynb), which is organized as a progressive workflow from baseline simulations to optimization experiments.

## What The Notebook Covers

1. Baseline glucose simulations with meal, insulin, and exercise events
2. Grid search and discrete genetic algorithm baselines
3. DEAP-based evolutionary optimization
4. Hybrid ODE + GA experiments
5. Final standardized metrics table for cross-model comparison

## Environment

Recommended:

- Python 3.10+
- Jupyter Notebook or VS Code Notebook support

Key packages used in the notebook:

- numpy
- pandas
- matplotlib
- scipy
- deap

The notebook includes `%pip` setup cells for these dependencies.

## Running

1. Open [Insulin_Optimization.ipynb](Insulin_Optimization.ipynb)
2. Run cells top-to-bottom in a fresh kernel
3. Review the final section: `Final Results Summary (Standardized Metrics)`

## Final Metrics (Important)

The notebook now reports a standardized comparison table using shared trajectory-level metrics where possible:

- `mean_abs_error_target`
- `rmse_target`
- `time_in_range_pct` (70-180 mg/dL)
- `minutes_below_70`
- `minutes_above_180`

This avoids comparing raw objective values from different models directly, since each model uses different fitness formulations and penalty scales.

It also includes a follow-up fair-comparison cell that resamples trajectories to a common 1-minute grid before computing the same metrics.

## Quick Scan Results (Reviewer View)

Snapshot from the latest fair-comparison (common 1-minute resampled) table in the notebook:

| Experiment                         | MAE to 100 | Time in 70-180 | Below 70 (min) | Above 180 (min) | Quick interpretation                 |
| ---------------------------------- | ---------: | -------------: | -------------: | --------------: | ------------------------------------ |
| Hybrid ODE + GA                    |       0.46 |        100.00% |              0 |               0 | Best overall in this run             |
| Improved Mini Bergman              |       7.47 |         96.37% |            217 |               1 | Good control with hypo-risk episodes |
| Mini Bergman (interval, resampled) |       9.14 |        100.00% |              0 |               0 | Stable but less precise than hybrid  |
| Grid search (discrete, resampled)  |      25.76 |        100.00% |              0 |               0 | Simple baseline, not competitive     |
| GA discrete (resampled)            |      45.39 |         52.28% |            115 |               0 | Weak physiological plausibility      |

Lower MAE is better. Higher time-in-range is better.

For detailed values, see the final two notebook outputs:

- Standardized metrics summary table
- Fair-comparison (common-grid resampled) summary table

## Interpretation Notes

- Some models operate on coarse time steps (for example, 6-hour intervals), while others are minute-level.
- The final table is intended for practical model comparison, not as a clinical-grade benchmark.
- This project is research software and does not provide medical advice.

## Repository Structure

- [Insulin_Optimization.ipynb](Insulin_Optimization.ipynb): main notebook
- [Avatars/](Avatars/): avatar assets/profiles used by experiments
- [README.md](README.md): project documentation
