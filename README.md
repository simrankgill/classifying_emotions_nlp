# Comparative Analysis of BERT-Based Models for Emotion Detection
### Contributers: Simran Gill, Vicky Liu, Jo Zhu

This project explores multi-label emotions classifiation on the GoEmitions-105 dataset using transformer-based models. We compare serveral pre-trained langiage models, apply techniques to handel class imbalance, and investigate training strategies that imporve predivtive performance.

### Transformer Models Evaluated
Experimented with four transformer models. 

| Model          | Description                                                              |
|----------------|---------------------------------------------------------------------------|
| **BERT**       | Baseline model with bidirectional attention for contextual understanding |
| **RoBERTa**    | BERT variant with dynamic masking and no next-sentence prediction        |
| **DistilBERT** | Lightweight, faster version of BERT with 97% performance                 |
| **DeBERTa**    | Improves attention mechanism by disentangling content and position       |


### Summary of Experiments
We ran five modeling experiments on all four models to see if modern models perform better compared to BERT. 

| # | Name                                | Description                                                                 |
|---|-------------------------------------|-----------------------------------------------------------------------------|
| 1 | Simple Baseline                     | Creating a simple model without adding weights, thresholds, or freezing layers. |
| 2 | Simple Baseline + Thresholds        | Apply thresholds to the predictions of the baseline model to improve classification performance. |
| 3 | Weighted Loss                       | Add class weights to the loss function to address class imbalance.         |
| 4 | Weighted + Threshold                | Combine class weighting with threshold tuning (thresholds derived from weighted model). |
| 5 | Weighted + Threshold + Freezing Layers | Add freezing of lower layers in the model to reduce overfitting and improve generalization. |

### Train N Binary Models 
To see if binary classification models perform better for minority classes, we selected three best and worst performing labels based on the F1 score from the baseline model, BERT. The goal here is to see if training a binary model could improve performance on the minority labels.

| Label     | BERT (Best) | BERT (Binary) | RoBERTa (Best) | RoBERTa (Binary) | DistilBERT (Best) | DistilBERT (Binary) | DeBERTa (Best) | DeBERTa (Binary) |
|-----------|-------------|----------------|----------------|------------------|-------------------|----------------------|----------------|-------------------|
| Love      | **0.7744**  | 0.5986         | 0.7853         | 0.6077           | 0.7798            | 0.6071               | 0.7918         | 0.6059            |
| Gratitude | 0.7694      | 0.6032         | **0.7467**     | 0.5706           | 0.7612            | 0.5989               | 0.7625         | 0.5947            |
| Amusement | 0.7601      | 0.5523         | **0.7638**     | 0.5664           | 0.7546            | 0.5297               | 0.7564         | 0.5435            |
| Relief    | 0.2740      | 0.1014         | 0.2957         | 0.1536           | **0.3177**        | 0.1193               | 0.2457         | 0.1291            |
| Pride     | 0.1299      | 0.0920         | 0.1642         | 0.0401           | **0.1892**        | 0.0927               | 0.1348         | 0.0823            |
| Grief     | 0.1250      | 0.0548         | **0.2044**     | 0.0847           | 0.1596            | 0.0689               | 0.1158         | 0.0612            |
