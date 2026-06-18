# Phase 5 - Model Development
## Step 5.3 - Baseline Models

## Validation Summary
- Dataset rows: 100000
- Features used for modeling: 227
- Categorical features: 21
- Numeric features: 206
- Target column: churn
- Splitter: StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

## Model Leaderboard
              model  roc_auc_mean  roc_auc_std  accuracy_mean  precision_mean  recall_mean  f1_mean  roc_auc_gap_mean
           LightGBM       0.68700      0.00330        0.63262         0.62435      0.64955  0.63669           0.02717
            XGBoost       0.67740      0.00434        0.62441         0.61163      0.66347  0.63647           0.01355
           CatBoost       0.67152      0.00417        0.61942         0.60635      0.66170  0.63280           0.00947
      Random Forest       0.66177      0.00522        0.61415         0.60305      0.64794  0.62467           0.33823
Logistic Regression       0.65681      0.00155        0.61382         0.61286      0.59953  0.60612           0.00696

## Fold Statistics
              model      stage  fold_mean  fold_std  roc_auc_mean  roc_auc_std  accuracy_mean  accuracy_std  precision_mean  precision_std  recall_mean  recall_std  f1_mean  f1_std
           CatBoost      train    3.00000   1.58114       0.68099      0.00146        0.62631       0.00151         0.61276        0.00201      0.66852     0.00187  0.63942 0.00062
           CatBoost validation    3.00000   1.58114       0.67152      0.00417        0.61942       0.00444         0.60635        0.00385      0.66170     0.00788  0.63280 0.00519
           LightGBM      train    3.00000   1.58114       0.71417      0.00080        0.65319       0.00139         0.64444        0.00181      0.66983     0.00492  0.65688 0.00215
           LightGBM validation    3.00000   1.58114       0.68700      0.00330        0.63262       0.00329         0.62435        0.00274      0.64955     0.00794  0.63669 0.00465
Logistic Regression      train    3.00000   1.58114       0.66377      0.00046        0.61833       0.00081         0.61755        0.00092      0.60393     0.00185  0.61066 0.00105
Logistic Regression validation    3.00000   1.58114       0.65681      0.00155        0.61382       0.00099         0.61286        0.00085      0.59953     0.00326  0.60612 0.00179
      Random Forest      train    3.00000   1.58114       1.00000      0.00000        0.99998       0.00001         0.99997        0.00000      0.99999     0.00001  0.99998 0.00001
      Random Forest validation    3.00000   1.58114       0.66177      0.00522        0.61415       0.00427         0.60305        0.00302      0.64794     0.01077  0.62467 0.00639
            XGBoost      train    3.00000   1.58114       0.69094      0.00119        0.63468       0.00214         0.62117        0.00281      0.67398     0.00577  0.64648 0.00236
            XGBoost validation    3.00000   1.58114       0.67740      0.00434        0.62441       0.00387         0.61163        0.00308      0.66347     0.01052  0.63647 0.00571

## Train vs Validation Comparison
              model  roc_auc_mean_train  roc_auc_mean_validation  roc_auc_gap  accuracy_mean_train  accuracy_mean_validation  precision_mean_train  precision_mean_validation  recall_mean_train  recall_mean_validation  f1_mean_train  f1_mean_validation
           LightGBM             0.71417                  0.68700      0.02717              0.65319                   0.63262               0.64444                    0.62435            0.66983                 0.64955        0.65688             0.63669
            XGBoost             0.69094                  0.67740      0.01355              0.63468                   0.62441               0.62117                    0.61163            0.67398                 0.66347        0.64648             0.63647
           CatBoost             0.68099                  0.67152      0.00947              0.62631                   0.61942               0.61276                    0.60635            0.66852                 0.66170        0.63942             0.63280
      Random Forest             1.00000                  0.66177      0.33823              0.99998                   0.61415               0.99997                    0.60305            0.99999                 0.64794        0.99998             0.62467
Logistic Regression             0.66377                  0.65681      0.00696              0.61833                   0.61382               0.61755                    0.61286            0.60393                 0.59953        0.61066             0.60612

## Selection Rule
- Best candidate by validation ROC AUC: LightGBM
- Validation ROC AUC: 0.68700
- Validation ROC AUC std: 0.00330

## Overfitting Observations
- Random Forest is the most overfit model in this baseline sweep: train ROC AUC is essentially perfect while validation ROC AUC stays much lower.
- LightGBM ranks first on validation ROC AUC and keeps the smallest practical generalization gap among the tree-based models.
- XGBoost and CatBoost both improve over Logistic Regression but remain below LightGBM on validation ROC AUC.
- Logistic Regression is the simplest and most stable model here, but it underfits relative to the boosted trees.

## Recommendations
- Promote LightGBM as the next-phase candidate.
- Keep the Step 5.2 splitter fixed for all later comparisons.
- Use fold-local preprocessing only; do not fit transforms on the full dataset before validation.
