## Overview
This project explores the **impact of linguistic data curation** on the performance of a sentiment classification model for Spanish text. Following a **data-centric AI approach**, I compared a baseline multilingual DistilBERT model against a version fine-tuned with linguistically preprocessed data.

## 📊 Key Results
Linguistic data curation in `spaCy` showed a **consistent improvement across all metrics** in all sets.

| Model | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: |
| **Model 1 (Raw)** | 0.638 | 0.631 | 0.624 |
| **Model 2 (spaCy Curation)** | **0.663** | **0.659** | **0.660** |

* **F1 Improvement: +0.036 points**.
* **Consistency:** Performance gains were replicated across training, development, and test sets, indicating high model robustness.
* **Neutral Class:** Significant accuracy boost in neutral labels (from 16 to 26 correct predictions).

## 🛠️ Methodology
* **Base Architecture:** `distilbert-base-multilingual-cased`.
* **Dataset:** 5,000 Spanish-labeled samples from the *MultiLingual Sentiment* dataset (ClapAI, 2024).
* **Training Config:** 3 epochs, learning rate 2e-5, 16-bit precision (fp16), and `load_best_model_at_end` strategy.
* **Linguistic Pipeline:**
    * **POS Tagging:** Used to isolate nouns, verbs, and adjectives.
    * **Lemmatization:** Verbs and nouns were reduced to their canonical forms to mitigate **lexical sparsity**.
    * **Negation Shielding:** Specific focus on preserving negative adverbs (e.g., "no") to prevent polarity flipping.

## 🔍 Error Analysis
1.  **Irony Detection:** The model struggles with irony (e.g., *"Increíble el trauma..."*).
2.  **Label Noise:** Identified instances where human annotation in the original dataset was inconsistent with the textual sentiment.
3.  **Neutral Bias:** Model 2 became more "careful," occasionally classifying extreme sentiments as neutral to avoid false positives.

## 🛠️ Requirements & Resources
* `transformers` library for model fine-tuning.
* `spaCy` for POS tagging and lemmatization.
* `MultiLingualSentiment` dataset from Hugging Face.
* For all the libraries required, please, check `requirements.txt`.
