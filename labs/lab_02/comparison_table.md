# Lab 1 vs Lab 2 - Comparison Table
| Model / Baseline | Accuracy | Precision | Recall | F1 | ROC-AUC |
|------------------------|----------|-----------|--------|-------|---------|
| Majority class (Lab 1) | 0.501 | 0.501 | 1.000 | 0.668 | 0.500 |
| Domain heuristic (Lab 1) | 0.731 | 0.730 | 0.736 | 0.733 | 0.797 |
| Prior-period baseline (Stretch) | 0.715 | 0.762 | 0.627 | 0.688 | 0.715 |
| Lab 2 model (LogReg) | 0.777 | 0.782 | 0.768 | 0.775 | 0.830 |
## Primary metric: F1 (justified in Lab 1)
## Interpretation (3-5 sentences)
The Lab 2 model beat all three baselines, achieving F1=0.775 compared to the domain heuristic baseline (F1=0.733), a gain of +4.2%. The domain heuristic was the hardest baseline to beat, reflecting that simple pre-race rules capture clear signal in F1 prediction. The engineered features (previous finish position, rolling 3-race average, and constructor tier) provided additional predictive leverage beyond grid position alone, validating that domain-informed feature engineering improves over naive heuristics. The model's ROC-AUC of 0.830 is also competitive with all baselines, showing robust ranking quality. This demonstrates that structured historical features unlock value for Top-10 prediction when combined with a simple, interpretable model.