# Repository Structure — AI Emergency Room Medication & Safety Advisor

This repository contains four Google Colab notebooks. Each notebook represents one stage of the system.
Throughout the project, many different models and approaches were tested. After comparing all results, these four notebooks form the final and most stable setup.

All datasets (FAERS, DrugBank, interaction rules) are stored on Google Drive, and each notebook includes the standard Drive mounting:

from google.colab import drive
drive.mount('/content/drive')


No manual downloading is needed.

1. FAERS Model — Training Notebook (Meditron + LoRA)

File: FAERS_Training_Meditron.py
Original Colab: https://colab.research.google.com/drive/1ewjC4xWFc3OB2Cckjse1vrPRZyWbxi_M?usp=sharing

This notebook trains the FAERS model using Meditron-7B with LoRA.
It loads the cleaned FAERS dataset from Drive and performs full fine-tuning.
The final LoRA weights produced here are used later in testing and in the Gradio application.

2. DrugBank Model — Logistic Regression Testing Notebook

File: DrugBank_LogReg_Testing.py
Original Colab: https://colab.research.google.com/drive/1GEBurh1oFOcqAP8Gkmqvl5Otqr-vAVGI?usp=sharing

This notebook tests an earlier version of the DrugBank model using TF-IDF and Logistic Regression.
It was part of the experimentation phase and helped compare classical ML results before selecting the final similarity-based approach.

3. FAERS Model — Testing Notebook

File: FAERS_Model_Testing.py
Original Colab: https://colab.research.google.com/drive/1GEIpGhI99EMSBwb9lvYC0-MKX4qpFHVj?usp=sharing

This notebook loads the trained FAERS Meditron model with its LoRA weights and is used only for testing and debugging.
It checks:

Adverse reaction predictions

How the model behaves with different drug lists, ages, and sexes

Whether the LoRA weights are correctly applied

No training happens here.

4. Final Gradio Application + Drug Preparation Model

File: Final_Gradio.py
Original Colab: https://colab.research.google.com/drive/1Da10YbvN3pvWun3syA-_SKa20LlY07Gq?usp=sharing

(Same Colab also includes the drug prediction training section.)

This is the main application notebook. It includes:

Drug recommendation model (TF-IDF + SVD similarity)

FAERS model (Meditron + LoRA) for adverse reaction prediction

Rule-based drug interaction checker

Complete Gradio interface

User Inputs:

Symptoms

Age

Sex

Current medications

Outputs:

Recommended medication

Predicted adverse reactions

Interaction warnings

This notebook represents the full ER decision-support system.

Final Models Used in the System
1. Medication Recommendation Model

A similarity-based model using TF-IDF and SVD to match symptom text to the most suitable medications.

2. Adverse Reaction Prediction Model

Meditron-7B fine-tuned with LoRA on the FAERS dataset, predicting likely adverse reactions based on the patient’s drug list, age, and sex.
