# Baseline Report - [Tomas Rodriguez y Joaquin Rodriguez]

## 1. Prediction target
Predict whether each driver will finish in the Top 10 (`is_top10`) for a given race, using only information available before race start.

## 2. Majority-class baseline
- Metric: F1
- Value: 0.668 (validation season 2023)
- Code: `DummyClassifier(strategy='most_frequent', random_state=414)`

## 3. Domain heuristic baseline
- Rule: Predict Top 10 if grid position is 10 or better (`grid_position <= 10`), otherwise predict non-Top-10.
- Metric (same as above): 0.733 (validation season 2023)
- Code cell:

```python
validation_df = df[df["season"] == 2023].copy()
validation_df["prediction"] = (validation_df["grid_position"] <= 10).astype(int)
```

## 4. Metric choice + justification
I chose F1 as my primary metric because the positive class (`is_top10 = 1`) is close to 50% in this dataset, so accuracy alone can be misleading. A false positive means predicting a Top-10 finish for a driver who does not make it, which can overestimate confidence in race outcomes. A false negative means missing a true Top-10 finish, which is also costly because it underestimates competitive drivers. Since both error types matter in this task, F1 is more informative than accuracy because it balances precision and recall in one score.

## 5. Leakage guard item
- Checklist item: Temporal availability of predictors (pre-race only).
- Finding: The domain baseline uses only `grid_position`, which is known before the race; post-race variables such as `finish_position` were excluded from prediction logic.
- Fix required: No additional fix required for baseline logic (already leakage-safe by design).

## 6. Baseline comparison and interpretation
The domain heuristic baseline is harder to beat than the majority baseline (F1: 0.733 vs 0.668), so it is the real floor for Lab 2 improvements. This gap shows that even a simple F1-informed domain rule captures useful pre-race signal beyond class frequency alone. If a later ML model scores below the domain heuristic baseline, I would conclude that feature engineering or data representation is weak relative to domain knowledge. Next, I would improve leakage-safe historical features (lag and rolling form), improve categorical encoding for team strength, and re-check temporal validation consistency.