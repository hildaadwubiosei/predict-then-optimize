# Fairness Under Prediction Error in Predict-Then-Optimize

**Author:** Hilda Adwubi Osei

## What this is

How error in an ML prediction, used to make a budget-limited allocation
decision for a group of people, affects whether a demographic parity
constraint stays satisfied when checked against people's true outcomes
instead of the predictions, and how the size of that violation scales
with the prediction error.

Fairness constraints in deployed systems are almost always enforced on
*predictions* ŷ, because true outcomes y aren't known at decision time.
This project asks whether that guarantee survives contact with reality,
and bounds how far it can drift.

## Approach

1. **Synthetic study** — controllable prediction error (σ) on top of a
   two-group allocation problem (CVXPY), comparing the fairness gap
   measured on ŷ vs. on y as σ and sample size n vary.
2. **Empirical pattern** — the true-outcome gap grows with σ and
   saturates; best fit is `c·(1 − e^(−σ/τ))`.
3. **Theoretical bound** — a two-piece result: (i) a local sensitivity
   formula showing only two "marginal" individuals per decision
   determine the gap's first-order behavior, derived via LP duality/KKT
   and verified numerically against the solver; (ii) a universal,
   σ-independent ceiling from the boundedness of the decision variable.
4. **Real-data study** — the same pipeline on US Census income data
   (folktables `ACSIncome`, California, 2018), with a real trained
   predictor (R² ≈ 0.41) in place of simulated noise. Result stable
   across 10 independent train/test splits: enforcing the constraint on
   predictions removes most, but not all (≈34% survives), of the true
   disparity.

## Repository structure

```
fairness-predict-optimize/
├── predict-optimize.ipynb   # main notebook: all experiments
├── results/ 
├── data/                         # saved figures and summary tables
├── LICENSE                           # MIT — applies to code
├── LICENSE-CONTENT                   # CC BY 4.0 — applies to paper/figures/text
└── README.md
```

## Running it

```bash
pip install numpy cvxpy pandas matplotlib scipy scikit-learn folktables
jupyter notebook fairness-predict-optimize.ipynb
```

The real-data section downloads US Census PUMS data on first run via
`folktables` (requires an internet connection).

## License

- **Code** (notebook cells, functions, scripts) is licensed under the
  [MIT License](./LICENSE).
- **Written content** (paper text, figures, tables once the preprint is
  finalized) is licensed under
  [CC BY 4.0](./LICENSE-CONTENT).

## Citation

A citation entry will be added once this is posted to arXiv.
