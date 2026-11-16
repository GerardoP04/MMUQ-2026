# Assignment 2 parameter perturbation classification — historical version

**Historical note:** This document records an earlier decision to hold `snw_att` fixed. The current study subsequently reinstated all 18 parameters, including `snw_att`. Use `Assignment2_Experiment_Report.tex` and its PDF for the current plan and results.

## Model and classification principles

Use the HBV001a model, `calibration_config.py` calibration bounds, and `calibration_outputs/best_parameters.csv` from the specified Assignment 1 course folder. Its best parameters differ from the workspace copy; the course folder was selected as the reference. Original calibration bounds are hard limits. This historical note classifies perturbations and does not itself calculate sensitivity. It considers whether multiplication by 0.8 and 1.2 stays within bounds and whether percentage perturbation has a suitable physical interpretation.

## Category 1: both 0.8 and 1.2 permitted (11 parameters)

| Module | Parameter | Meaning |
|---|---|---|
| Snow | `snw_pmf` | Precipitation-induced melt factor |
| Snow | `snw_amf` | Air-temperature-induced melt factor |
| Soil | `sl0_bt0` | Soil runoff exponent |
| Upper reservoir | `urr_dth` | Initial storage |
| Lower reservoir | `lrr_dth` | Initial storage |
| Upper reservoir | `urr_ulc` | Percolation fraction to lower reservoir |
| Upper reservoir | `urr_tdh` | Fast-outlet threshold |
| Upper reservoir | `urr_tdr` | Fast-outlet coefficient |
| Upper reservoir | `urr_ndr` | Normal outlet coefficient |
| Upper reservoir | `urr_uct` | Subsurface export fraction |
| Lower reservoir | `lrr_lct` | Subsurface export fraction |

## Category 2: one 20% endpoint exceeds calibration bounds (6 parameters)

| Parameter | Baseline | Calibration range | Infeasible endpoint | Maximum permitted change in constrained direction |
|---|---:|---:|---:|---:|
| `snw_dth` | 8.58808 | 0–10 | ×1.2 = 10.30570 | +16.44% |
| `sl0_dth` | 49.06446 | 0–50 | ×1.2 = 58.87735 | +1.91% |
| `sl0_pwp` | 646.54862 | 5–700 | ×1.2 = 775.85834 | +8.27% |
| `sl0_fcy` | 122.27323 | 100–700 | ×0.8 = 97.81858 | −18.22% |
| `urr_wsr` | 0.99104 | 0–1 | ×1.2 = 1.18925 | +0.90% |
| `lrr_dre` | 0.00913049 | 0–0.01 | ×1.2 = 0.01095658 | +9.52% |

### Agreed treatment: asymmetric perturbations

From the baseline, change by at most 20% in each direction; stop at the calibration bound if it is reached first. The other direction may still reach 20%.

| Parameter | Lower direction | Upper direction |
|---|---:|---:|
| `snw_dth` | −20% | to upper bound, +16.44% |
| `sl0_dth` | −20% | to upper bound, +1.91% |
| `sl0_pwp` | −20% | to upper bound, +8.27% |
| `sl0_fcy` | to lower bound, −18.22% | +20% |
| `urr_wsr` | −20% | to upper bound, +0.90% |
| `lrr_dre` | −20% | to upper bound, +9.52% |

For example, `sl0_dth` starts at about 49.06, with an upper bound of 50: it can decrease to about 39.25, but can only increase to 50. The chart must label the actual upper change of approximately +1.91%, not +20%.

Parameter ranges differ, which matters when comparing sensitivities. The positive ranges of `sl0_dth` and `urr_wsr` are especially narrow, limiting conclusions in that direction. These values apply to this saved parameter vector; another random seed requires new boundary checks. Similar NSE values with different parameter vectors remain a separate question.

## Category 3: temperature threshold held fixed in this historical plan (1 parameter)

The historical plan held `snw_att` fixed at approximately −0.00604556 °C, close to 0 °C. A 20% change corresponds to only about ±0.00120911 °C. The threshold was considered physically plausible and the perturbation small. Actual rain-snow transitions do not always occur at a single temperature. Since this historical plan did not perturb the threshold, it could not establish its sensitivity.

**Superseding decision:** The current experiment includes `snw_att` as well as all other parameters. It reports the limitations of percentage changes near zero on the Celsius scale.

## Historical classification summary

Eleven parameters permitted both 20% endpoints, six used asymmetric ranges, and one temperature threshold was held fixed: 18 in total. This classification applies only to that historical baseline and decision.
