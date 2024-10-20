Confusion matrix:

|  | Predicted Positive | Predicted Negative |
| :--: | :--: | :--: |
| Actual Positive | True Positive (TP) | False Negative (FN) |
| Actual Negative | False Positive (FP) | True Negative (TN) |



- Accuracy: Accuracy provides the proportion of correctly classified instances.
  
  $Accuracy = \frac{True \, Positives + True \, Negatives}{Total}$  
- Precision: Precision focuses on the accuracy of positive predictions.
  
  $Precision = \frac{True \, Positives }{True\, Positives + False \, Positives}$ 
- Recall (Sensitivity or True Positive Rate): Recall measures the proportion of correctly predicted positive instances among all actual positive instances.
    
    $Recall = \frac{ True \, Positives}{True\, Positives + False \, Negatives}$   
- F1 Score: F1 score is the harmonic mean of precision and recall.
    
    $F1 \space Score = 2 * \frac{Precision * Recall}{Precision + Recall}$

Summary：
- Accuracy gives an overall measure of correctness but can be misleading if the classes are imbalanced.
- Precision focuses on the quality of positive predictions 
- Recall emphasizes the completeness of positive cases.
- F1 Score balances precision and recall, providing a single metric to assess performance.