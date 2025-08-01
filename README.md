# Comparative Analysis of BERT-Based Models for Emotion Detection
### Contributers: Simran Gill, Vicky Liu, Jo Zhu

**Purpose:** Identify whether modern transforer models (RoBERTa, DistilBERT, DeBERTa) out perform BERT or if performance improvements come from training strategies. 

This project explores multi-label emotions classifiation on the GoEmitions-105 dataset using transformer-based models. We compare serveral pre-trained langiage models, apply techniques to handel class imbalance, and investigate training strategies that imporve predivtive performance.

### Transformer Models Evaluated
Experimented with four transformer models. 
 
| Model          | Description                                                               |
|----------------|---------------------------------------------------------------------------|
| **BERT**       | Baseline model; strong contextual understanding.                          |
| **RoBERTa**    | Dynamic masking; improved F1 in prior studies.                            |
| **DistilBERT** | Lightweight; 60% faster with 97% of BERT’s performance.                   |
| **DeBERTa**    | Advanced attention mechanism; better position/content disentanglement.    |


### Summary of Experiments
We ran five modeling experiments on all four models to see if modern models perform better compared to BERT. 

| # | Name                                | Description                                                                 |
|---|-------------------------------------|-----------------------------------------------------------------------------|
| 1 | Simple Baseline                     | Creating a simple model without adding weights, thresholds, or freezing layers. |
| 2 | Simple Baseline + Thresholds        | Apply thresholds to the predictions of the baseline model to improve classification performance. |
| 3 | Weighted Loss                       | Add class weights to the loss function to address class imbalance.         |
| 4 | Weighted + Threshold                | Combine class weighting with threshold tuning (thresholds derived from weighted model). |
| 5 | Weighted + Threshold + Freezing Layers | Add freezing of lower layers in the model to reduce overfitting and improve generalization. |

#### Precision, Recall, and F1 Scores by Model and Experiment

| Model      | Exp | Precision | Recall  | F1 Score   |
|------------|-----|-----------|---------|------------|
| **BERT**       | 1   | 0.7778    | 0.3564  | 0.3581     |
|                | 2   | 0.5274    | 0.6329  | **0.5753** |
|                | 3   | 0.4076    | 0.6403  | 0.4981     |
|                | 4   | 0.5016    | 0.6423  | 0.5633     |
|                | 5   | 0.5016    | 0.6423  | 0.5633     |
| **RoBERTa**    | 1   | 0.7808    | 0.3531  | 0.4862     |
|                | 2   | 0.5185    | 0.6479  | **0.5761** |
|                | 3   | 0.2814    | 0.8684  | 0.4251     |
|                | 4   | 0.4710    | 0.6804  | 0.5567     |
|                | 5   | 0.4532    | 0.6477  | 0.5552     |
| **DistilBERT** | 1   | 0.7564    | 0.3793  | 0.5053     |
|                | 2   | 0.5346    | 0.6286  | **0.5778***|
|                | 3   | 0.4190    | 0.6406  | 0.5067     |
|                | 4   | 0.5111    | 0.6358  | 0.5667     |
|                | 5   | 0.5179    | 0.6211  | 0.5648     |
| **DeBERTa**    | 1   | 0.7806    | 0.3346  | 0.4684     |
|                | 2   | 0.4938    | 0.6478  |**0.5604**  |
|                | 3   | 0.2664    | 0.8802  | 0.4090     |
|                | 4   | 0.4847    | 0.6574  | 0.5580     |
|                | 5   | 0.4837    | 0.6088  | 0.5391     |

> **Bolded** F1 scores are the best for each experiment.  
> *Asterisk* marks the highest F1 score across all models and experiments.


### Train N Binary Models 
To see if binary classification models perform better compared to multi-label classification models, we selected three best and worst performing labels based on the F1 score from the baseline model, BERT. The goal here is to see if training a binary model could improve performance on the minority and low performing labels

#### Per-label Performance for Best and Binary Versions of Each Model (F1 Score)

| Label     | BERT (Best) | BERT (Binary) | RoBERTa (Best) | RoBERTa (Binary) | DistilBERT (Best) | DistilBERT (Binary) | DeBERTa (Best) | DeBERTa (Binary) |
|-----------|-------------|----------------|----------------|------------------|-------------------|----------------------|----------------|-------------------|
| Love      | 0.7850      | 0.5938         | 0.7853         | 0.6077           | 0.7794            | 0.6122               | **0.7918**     | 0.6059            |
| Gratitude | 0.7592      | 0.6032         | 0.7467         | 0.5706           | 0.7546            | 0.6031               | **0.7625**     | 0.5947            |
| Amusement | 0.7540      | 0.5523         | **0.7638**     | 0.5664           | 0.7480            | 0.5243               | 0.7564         | 0.5435            |
| Relief    | 0.2625      | 0.1014         | **0.2957**     | 0.1536           | 0.2904            | 0.1084               | 0.2457         | 0.1291            |
| Pride     | 0.1050      | 0.0920         | 0.1642         | 0.0401           | **0.1884**        | 0.0970               | 0.1348         | 0.0823            |
| Grief     | 0.1596      | 0.0548         | 0.2044         | 0.0847           | **0.2397**        | 0.0672               | 0.1158         | 0.0612            |

Overall, this suggests multi-label models are better suited for emotion classification takes where emotions overlap and contextual cues are shared across labels.

### Final Results 
Our findings show that DistilBERT, fine-tuned with threshold optimization (F1 = 0.5778) and enhanced by layer freezing (F1 = 0.5798), outperforms other models and binary classifiers.

Performance for minority emotion labels is still relatively low when binary classification models are applied per label. To be able to identify overlapping emotion labels, future work could include exploring contextual similarities between labels as a potential strategy to better distinguish subtle emotional expressions.   

