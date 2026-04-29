# Neural Network Credit Risk Prediction

A deep learning project applying a TensorFlow/Keras neural network to predict 
student loan credit ranking — used to demonstrate responsible AI design 
principles in high-stakes financial decision-making contexts.

---

## Business Context

Credit risk prediction models are among the most consequential AI applications 
in financial services. When a model recommends approving or denying a loan, 
it directly affects someone's access to education, housing, or opportunity. 
That makes the governance layer as important as the technical layer.

This project builds a binary classification neural network to predict student 
loan credit ranking, then examines the governance implications: what data 
should inform these decisions, how should bias be detected and mitigated, and 
what human oversight should exist before model outputs affect real people.

---

## What It Does

- Loads and preprocesses a student loan dataset with financial and academic 
  features
- Builds a Sequential neural network with two hidden layers (ReLU activation, 
  sigmoid output)
- Trains with binary crossentropy loss and Adam optimizer over 50 epochs
- Evaluates with accuracy, loss metrics, and a full classification report 
  (precision, recall, F1-score by class)
- Saves and reloads the trained model as a `.keras` file
- Discusses recommendation system design: data requirements, filtering 
  methodology, and real-world fairness challenges

---

## Model Architecture

Input Layer  →  features from student loan dataset
Hidden Layer 1: Dense (ReLU)
Hidden Layer 2: Dense (ReLU)
Output Layer:   Dense (1 unit, Sigmoid) → binary credit ranking prediction

**Loss function:** Binary crossentropy  
**Optimizer:** Adam  
**Epochs:** 50  
**Evaluation:** Accuracy + Classification Report (precision, recall, F1)

---

## Governance & Ethical Considerations

Credit risk models operating on student data sit at the intersection of 
several high-stakes governance concerns:

**Fair Lending Compliance**  
In the United States, credit decisions are governed by the Equal Credit 
Opportunity Act (ECOA) and the Fair Housing Act, which prohibit discrimination 
based on race, color, religion, national origin, sex, marital status, or age. 
A model predicting credit ranking must be audited for disparate impact — 
whether it produces systematically different outcomes for protected groups 
even when those groups are not explicit features in the model. Proxy variables 
(zip code, institution type, field of study) can encode protected 
characteristics indirectly.

**Bias Mitigation**  
As noted in the project's recommendation system discussion: ensuring the model 
is fair so that it does not disadvantage students from lower-income families 
is a design requirement, not an afterthought. Fairness metrics including 
demographic parity and disparate impact ratio should be computed across 
protected attributes before any deployment decision.

**NIST AI RMF Alignment**  
This project's governance approach maps to NIST AI RMF functions:
- **MAP:** Identifying that credit ranking prediction carries high risk of 
  disparate impact on protected groups
- **MEA:** Measuring fairness metrics across demographic groups using 
  classification report disaggregated by subgroup
- **MGO:** Recommending human review of all model-flagged denials before 
  action is taken

**Human-in-the-Loop**  
Model outputs should inform — not automate — credit decisions. Any denial 
recommendation should be reviewed by a human decision-maker with access to 
context the model cannot see. This is consistent with CFPB guidance on 
adverse action notices in AI-assisted credit decisions.

**Data Privacy**  
Student financial data is sensitive. In a production deployment, access 
controls, data minimization, and audit logging would be required. The model 
should never have access to data beyond what is necessary for the prediction 
task.

---

## Limitations & Honest Assessment

- **Dataset scope:** This project uses a structured academic dataset. 
  Real-world student loan data would include many more features and require 
  substantially more preprocessing and validation.
- **No fairness audit conducted:** The current notebook does not compute 
  fairness metrics across demographic subgroups — this is the most important 
  next step before any real-world application.
- **Binary classification only:** Credit risk is not binary in practice. 
  A production model would likely predict a risk score or tier, not a 
  binary ranking.
- **No cross-validation:** A single train/test split gives one estimate of 
  performance. Walk-forward or k-fold cross-validation would provide a more 
  robust accuracy estimate.
- **Model interpretability:** Neural networks are black boxes. A production 
  credit risk deployment would require explainability tooling (SHAP, LIME) 
  so that adverse action notices can explain why a recommendation was made — 
  a legal requirement under ECOA.

---

## What a Production Version Would Need

1. Fairness audit across protected attributes before deployment
2. SHAP or LIME explainability layer for adverse action compliance
3. Human review workflow for all denial recommendations
4. Data access controls and audit logging
5. Ongoing monitoring for model drift and demographic disparity

---

## Origin

This project was developed as part of the Ohio State University AI & ML 
Bootcamp (2024) and expanded with governance framing for portfolio purposes.

---

## Author

**Steven Hill**  
AI Ethics & Policy Professional | Purdue University MSAI  
[LinkedIn](https://linkedin.com/in/stevenrhill) | 
[GitHub](https://github.com/srhill12)