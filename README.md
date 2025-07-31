# Comparative Analysis of BERT-Based Models for Emotion Detection
### Contributers: Simran Gill, Vicky Liu, Jo Zhu

**Purpose:** Identify whether modern transforer models (RoBERTa, DistilBERT, DeBERTa) out perform BERT or if performance improvements come from training strategies. 

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

### Test Set Evaluation Metrics by Model and Experiment

| Model      | Exp. # | Subset Accuracy | Precision | Recall | F1      |
|------------|--------|------------------|-----------|--------|---------|
| *RoBERTa*  | 1      | 0.1505           | 0.7808    | 0.3531 | 0.4862  |
|            | **2**  | **0.0860**       | **0.5185**| **0.6479** | **0.5761** |
|            | 3      | 0.0103           | 0.2814    | 0.8684 | 0.4251  |
|            | 4      | 0.0593           | 0.4710    | 0.6804 | 0.5567  |
|            | 5      | 0.0629           | 0.4532    | 0.6477 | 0.5552  |
| *DistilBERT* | 1    | 0.1525           | 0.7604    | 0.3764 | 0.5036  |
|            | **2**  | **0.0942**       | **0.5317**| **0.6307** | **0.5770*** |
|            | 3      | 0.0600           | 0.4190    | 0.6406 | 0.5067  |
|            | 4      | 0.0812           | 0.5111    | 0.6358 | 0.5667  |
|            | 5      | 0.0755           | 0.5179    | 0.6211 | 0.5648  |
| *DeBERTa*  | 1      | 0.1452           | 0.7806    | 0.3346 | 0.4684  |
|            | **2**  | **0.0777**       | **0.4938**| **0.6478** | **0.5604** |
|            | 3      | 0.0089           | 0.2664    | 0.8802 | 0.4090  |
|            | 4      | 0.0632           | 0.4847    | 0.6574 | 0.5580  |
|            | 5      | 0.0602           | 0.4837    | 0.6088 | 0.5391  |


### Train N Binary Models 
To see if binary classification models perform better compared to multi-label classification models, we selected three best and worst performing labels based on the F1 score from the baseline model, BERT. The goal here is to see if training a binary model could improve performance on the minority and low performing labels

#### Per-label Performance for Best and Binary Versions of Each Model (F1 Score)

| Label     | BERT (Best) | BERT (Binary) | RoBERTa (Best) | RoBERTa (Binary) | DistilBERT (Best) | DistilBERT (Binary) | DeBERTa (Best) | DeBERTa (Binary) |
|-----------|-------------|----------------|----------------|------------------|-------------------|----------------------|----------------|-------------------|
| Love      | 0.7744      | 0.5986         | 0.7853         | 0.6077           | 0.7798            | 0.6071               | **0.7918**    | 0.6059            |
| Gratitude | **0.7694**  | 0.6032         | 0.7467         | 0.5706           | 0.7612            | 0.5989               | 0.7625         | 0.5947            |
| Amusement | 0.7601      | 0.5523         | **0.7638**     | 0.5664           | 0.7546            | 0.5297               | 0.7564         | 0.5435            |
| Relief    | 0.2740      | 0.1014         | 0.2957         | 0.1536           | **0.3177**        | 0.1193               | 0.2457         | 0.1291            |
| Pride     | 0.1299      | 0.0920         | 0.1642         | 0.0401           | **0.1892**        | 0.0927               | 0.1348         | 0.0823            |
| Grief     | 0.1250      | 0.0548         | **0.2044**     | 0.0847           | 0.1596            | 0.0689               | 0.1158         | 0.0612            |

Overall, this suggests multi-label models are better suited for emotion classification takes where emotions overlap and contextual cues are shared across labels.

### Final Results 
Across the five experiments, we found that DistilBERT performed the best when only thresholds are applied with an F1 score of 0.5770. This could mean a lighter model could have strong results when properly tuned.

Performance for minority emotion labels is still relatively low when binary classification models are applied per label. To be able to identify overlapping emotion labels, future work could include exploring contextual similarities between labels as a potential strategy to better distinguish subtle emotional expressions. 

