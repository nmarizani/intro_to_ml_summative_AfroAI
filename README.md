# ***AfroAI-VaxDemand: Predicting Regional Vaccine Demand Using Machine Learning***

***Presentation Video: https://drive.google.com/file/d/13a8awZWdeYTa2zykYMsp5ROuixZg1liv/view?usp=sharing***
***Problem Statement***
In Africa, the lack of accurate demand forecasting has been a significant barrier to establishing sustainable local vaccine manufacturing. Without reliable insights into when, where, and how much demand exists, manufacturers struggle with overproduction, underproduction, and inefficient supply chains. This often leads to over-reliance on imports, increased costs, and delayed immunization campaigns.

This project aims to build a machine learning classification model that predicts the level of vaccine demand (Low, Medium, High) across different regions based on vaccine uptake data and organizational activities. By accurately classifying regional demand levels, the model will support data-driven decisions in vaccine production planning, inventory allocation, and ultimately contribute to the development of resilient local vaccine manufacturing systems.

# The Dataset

***Dataset Description***
The dataset, cleaned_vaccine_data.csv, contains records related to vaccine uptake across various regions and organizations. Each row represents a data point for a specific region-organization instance and includes:

Region: The geographical area where the vaccine program was implemented.

Org_Name: The name of the organization managing or supporting the vaccination effort.

Uptake_Percent: The percentage of vaccines that were utilized or administered in that region.

demand_level (derived): A categorical variable derived from Uptake_Percent to indicate whether demand was:**Low, Medium, High**

The demand_level is the target variable to be predicted.


### 🔍 Model Evaluation and Comparison

We implemented and compared five models using different combinations of optimizers, regularization, and training techniques. Here's a summary:

| Training Instance    | Optimizer Used | Regularizer Used | Epochs | Early Stopping               | Layers | Learning Rate        | Accuracy | F1 Score | ROC AUC | Precision |
|----------------------|----------------|------------------|--------|------------------------------|--------|----------------------|----------|----------|---------|-----------|
| Logistic Regression  | solver - newton-cg           |  c -  10           |  200  | No                           | 3      | None                 | 0.94     | 0.91     | 0.91    | 0.91      |
| Simple NN Model      | Adam           | None             | 30     | No                           | 3      | None                 | 0.91     | 0.91     | 0.85    | 0.94      |
| Instance 1           | Adam           | L1               | 20     | val_loss (patience = 7)      | 3      | 0.005                | 0.94     | 0.91     |   0.98  | 0.91      |
| Instance 2           | RMSprop        | L2               | 20     | val_accuracy (patience = 6)  | 3      | 0.1                  | 0.64     | 0.78    | **0.93**     | 0.64      |
| Instance 3           | SGD            | L1               | 20     | val_loss (patience = 5)      | 3      | 0.001, momentum = 0.8| 0.70     | 0.29     | 0.77    | 0.67      |

---

### 🧠 Analysis & Key Insights

- **Logistic Regression**: Performed well, proving the dataset is linearly separable.
- **Simple NN (Adam, no reg)**: Matched baseline — indicating regularization is needed for improvement.
- **Best Model: Instance 2 (RMSProp + L2)**: Best **ROC AUC (0.93)** and solid overall scores. Regularization + tuned LR helped generalization.
- **Instance 3 (SGD + L1 + Momentum)**: Worst precision and F1. Despite decent ROC AUC, the model failed to classify properly — slow convergence or threshold issue.

---

### 🏁 Conclusion

> A combination of **RMSprop optimizer with L2 regularization** gave the best trade-off between accuracy and generalization. Simpler models performed better when fine-tuned, reinforcing the importance of **regularization and learning rate tuning** over mere complexity.

### Which implementation worked best between ML Algorithm and Neural Network?
Logistic Regression: Best baseline model; simple and effective.
NN with RMSprop + L2 (Instance 2): Best overall model for detecting important classes and improving generalization.
Adam & SGD setups, underperform unless significantly tuned.