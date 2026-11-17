# Many-body entanglement quantification through a few partial-transpose moments

Code and data for the Letter

> S. Chakrabarty and A. S. Majumdar,
> *Many-body entanglement quantification in arbitrary states through a few partial-transpose moments*
> (2026).

The Jupyter notebook `entanglement_quantification.ipynb` reproduces every number, table and figure of the Letter, its End Matter and its Supplemental Material (SM). Its last section compares each number quoted in the manuscript with the computed value and stops with an error if any of them disagree.

## What the notebook computes

| Section | Content | Manuscript |
|---|---|---|
| 1 | Closed-form quantifiers E4, E6, E8 | Eqs. (10)-(13) |
| 2 | Quadrature rules for any even order K (Lanczos and Hankel routes) | Theorem 1, SM Sec. S7 |
| 3 | Werner state and pure two-qubit state | Fig. 1 |
| 4 | Ground states of the TFIM, XXZ chain and LMG model, n = 12 | Fig. 2 |
| 5 | Gibbs state of the TFIM, sudden death | Fig. 3 |
| 6, 7 | Convergence of the hierarchy up to K = 160 | Figs. 4, 5 |
| 8 | Finite statistics | Fig. 6 |
| 9 | DMRG up to n = 32 (quimb) | Fig. 7 |
| 10 | Bounds from all moments, certified by linear programming | SM Sec. S8, Table S1, Fig. S1 |
| 11 | Windows of 2+2 sites | SM Sec. S9, Fig. S2 |
| 12 | Bound at a stated confidence | SM Sec. S10, Fig. S3 |
| 13 | Stabilizer states, pure and mixed | Corollary 1, SM Sec. S4 |
| 14 | Every quoted number, checked | |

## How to run

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace entanglement_quantification.ipynb
```

or open the notebook in Jupyter and run all cells. A full run takes about 25 minutes on a laptop, mostly in the DMRG and linear-programming sections. To reuse stored DMRG results instead of recomputing them, set `REUSE_DMRG=1` in the environment.

## Output

All figures are written to `figures/` as PDF (as used in the manuscript) and PNG. The data behind them are stored in the same folder:

| File | Content |
|---|---|
| `manybody_scans.npz` | Quantifiers along the parameter scans of Fig. 2 |
| `thermal_thresholds.json` | Sudden-death temperature and zero crossings |
| `manybody_K_convergence.json` | High-order values, number of distinct magnitudes |
| `noise_results.json` | Finite-statistics study |
| `dmrg_results.json` | DMRG values and convergence checks |
| `odd_moments.json` | Certified bounds from all moments, Table S1 |
| `confidence.json` | Bound at a stated confidence |

## Numerical methods in brief

* Ground states by sparse Lanczos diagonalization in a fixed symmetry sector (even parity for the TFIM and the LMG model, zero magnetization for the XXZ chain), so that they are unique at degenerate points.
* Partial transposes diagonalized in full, without truncation.
* High-order quadrature rules from the spectrum by the Lanczos procedure in 80-digit arithmetic, cross-checked with the moment-only Hankel route in 100-digit arithmetic.
* Bounds from all moments by linear programming, certified by the dual solution, which is verified in exact rational arithmetic.
* DMRG with two bond-dimension schedules; a point is kept only if energies, moments, admissibility and parity checks pass.

## Citation

If you use this code, please cite the Letter above.
