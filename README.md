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
