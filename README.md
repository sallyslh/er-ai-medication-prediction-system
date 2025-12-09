# Repository Structure — AI Emergency Room Medication & Safety Advisor

This repository contains four Google Colab notebooks. Each notebook corresponds to one stage of the system.
Throughout the project, several models and approaches were tested. After comparing all results, these four notebooks represent the final, most stable setup.

All datasets (FAERS, DrugBank, interaction rules) are stored on Google Drive, and every notebook includes Drive mounting instructions.

1. FAERS Model — Testing Notebook

File: FAERS_Model_Testing.ipynb

This notebook loads the FAERS model trained on Meditron using LoRA and evaluates it. It is used to test:

Adverse reaction predictions

Behavior with different drug lists, ages, and sexes

Whether the LoRA weights are applied correctly

This notebook does not train the model; it is only for testing and debugging.

2. Final Gradio App + Drug Preparation Model Notebook

File: Final_Gradio_And_DrugModel.ipynb

This is the main application notebook. It integrates all components into one system.

Included components:

DrugBank medication recommendation model (similarity-based)

FAERS adverse reaction prediction model (Meditron + LoRA)

Rule-based drug interaction checker

Gradio interface for user interaction

User inputs:

Symptoms

Age

Sex

Current medications

Outputs:

Recommended medication

Predicted adverse reactions

Interaction warnings

This notebook represents the complete ER decision-support system.

3. DrugBank Model — Logistic Regression Testing Notebook

File: DrugBank_LogReg_Testing.ipynb

This notebook tests an earlier machine-learning version of the DrugBank model that uses:

TF-IDF features

Logistic Regression

Symptom-to-medication classification

It was part of the experimentation phase. The results helped in comparing different models before selecting the final similarity-based approach.

4. FAERS Model — Training Notebook (Meditron LoRA)

File: FAERS_Training_Meditron.ipynb

This notebook trains the FAERS model using:

Meditron-7B as the base model

LoRA adapters for efficient fine-tuning

FAERS dataset loaded from Google Drive

The resulting LoRA weights are later used in the testing notebook and in the final Gradio application.

Datasets

All datasets used by the project are stored on Google Drive:

FAERS cleaned dataset

DrugBank indications dataset

Drug interaction rules (CSV)

Every notebook includes the following:

from google.colab import drive
drive.mount('/content/drive')


No manual downloading is required.

Final Models Used

After experimenting with multiple architectures, classical ML methods, and different LLM setups, the following models were chosen as the final version of the system:

1. Drug Model (Medication Recommendation)

A similarity-based model using TF-IDF and SVD to match symptom descriptions to the most suitable medications.

2. FAERS Model (Adverse Reaction Prediction)

Meditron-7B fine-tuned with LoRA on FAERS adverse event data to predict likely side effects and safety issues based on drug list, age, and sex.
