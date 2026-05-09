# Master Thesis - Prediction of Equine Body Condition from 3D Shape Parameters

This repository contains the code and data of my master's thesis. The work investigates whether 3D shape parameters (beta coefficients derived from a statistical shape model) can be used to predict the Body Condition Score (BCS) of horses, both as a total score and broken down by anatomical region.

---

## Data

`COMBINED_HORSES_DATA.xlsx` - the consolidated dataset containing 39 3D shape parameters (`beta_0` to `beta_38`), total BCS, and sub-scores for seven anatomical regions (neck, withers, back, tailhead, shoulder, ribs, thighs). This is a private dataset and is not included in the repository.

---

## Notebooks

The analysis is structured as four successive modelling phases, each building on the findings of the previous one.

**`EDA.ipynb`**: Exploratory Data Analysis.

**`Phase1_modelling.ipynb`**: Baseline modelling. Trains and compares unconstrained and regularised models (OLS, Lasso, Ridge, Random Forest, MLP, Ordinal Logistic Regression, Voting Regressor) on all 39 features. Metrics: R², MSE, MAE, and clinical tolerance (±0.5 and ±1.0 BCS).

**`Phase2_kFold_modelling.ipynb`**: Repeated k-fold cross-validation (5 folds × 3 repeats). Re-evaluates the same model family with more robust cross-validation, adding PLS Regression.

**`Phase3_ForwardSequentialFeatureSelection.ipynb`**:  Forward Sequential Feature Selection (SFS) to identify the optimal subset of shape parameters. Uses nested cross-validation (inner loop for tuning, outer loop for evaluation) to produce unbiased performance estimates on the reduced feature set.

**`Phase4_StackingMethod.ipynb`**: Sub-BCS stacking. Base models (Ridge, Lasso, Ordinal Logistic Regression) are trained independently on each anatomical region, their out-of-fold predictions are used as meta-features for a Ridge meta-model. Uses the optimal features identified in Phase 3.
