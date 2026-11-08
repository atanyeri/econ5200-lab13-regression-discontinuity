# Regression Discontinuity: Bandwidths, Manipulation and Close Elections

## Objective
I estimated effects at a cutoff with regression discontinuity, tested whether the design could be refuted, and showed how much the estimate depends on the bandwidth.

## Methodology
- Simulated a grant awarded at a need index of 50, with a true effect of 8 percentage points on enrolment.
- Fitted a global quadratic to all 4,000 students, then a local linear regression with `rdrobust` at a data-driven bandwidth.
- Fitted the local linear estimate at seven hand-chosen bandwidths (3 to 50) and repeated the simulation 300 times to separate bias from variance, using RMSE.
- Ran a density test on clean data and on data where 40% of units just above the cutoff moved just below it.
- Ran a covariate continuity test on a pre-treatment prior score, and on a copy with a 5-point jump planted at the cutoff.
- Applied the same design to US House elections (Lee, Moretti and Butler 2004), with the Democratic vote share as the running variable and the adjusted ADA score as the outcome, plus a density test at 50%.
- Wrote my own local linear estimator with a triangular kernel, using weighted least squares, and checked it against `rdrobust`.

## Key Findings
- The global quadratic estimated +0.0357 against a true +0.0800, less than half the truth. The local linear fit at a bandwidth of 16.1 estimated +0.0789.
- Across 300 draws, the RMSE was smallest at a bandwidth of 20 (0.0127). Narrow windows had little bias but a large spread, and wide windows had a small spread but a large bias.
- The density test gave p = 0.0022 on the data where units moved across the cutoff, and p = 0.965 on the clean data.
- The covariate test found no jump in the clean prior score (+0.243, p = 0.7694) and caught the planted jump (+5.243, p = 0.0000). Passing these tests does not prove the design is valid.
- A Democrat barely winning a House seat, rather than barely losing it, raised the representative's ADA score by +46.491 points. The density test at 50% showed no sign of sorting (p = 0.717). The estimate applies only to very close races.
- My estimator matched `rdrobust` on the grant data (+0.0876 at a bandwidth of 10 and +0.0789 at 16.1) and on the House data (+46.491).
