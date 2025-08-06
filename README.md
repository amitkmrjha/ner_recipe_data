# 🥘 Named Entity Recognition (NER) for Recipe Data using CRF

This project builds a **Named Entity Recognition (NER)** system to automatically extract **ingredients**, **quantities**, and **units** from recipe texts using a **Conditional Random Fields (CRF)** model.

---

## 📌 Business Objective

With the rise of cooking apps and meal planning platforms, there's a growing need to **automate recipe tagging**.  
This project helps:

- Improve recipe search and filtering
- Enable ingredient-based or portion-based recommendations
- Eliminate manual tagging for food-tech businesses

---

## 📈 Project Overview

- **Task**: Entity extraction from recipe text
- **Model**: Conditional Random Field (CRF)
- **Tech Stack**: Python, sklearn-crfsuite, spaCy, pandas, matplotlib
- **Entities Recognized**:
  - `ingredient` (e.g., sugar, tomato)
  - `quantity` (e.g., 1, 1/2, few)
  - `unit` (e.g., cup, tsp, grams)

---

## 🛠️ Feature Engineering

Custom features extracted per token:

- Token: lowercase form
- Lemma and POS tag using spaCy
- Word shape, capitalization, punctuation
- Regex detection for:
  - Fractions (e.g., `1/2`)
  - Decimals (e.g., `1.5`)
  - Whole numbers
- Contextual features (previous/next word)
- Flags for known `unit_keywords` and `quantity_keywords`

---

## 🧪 Model Training

| Parameter              | Value          |
|------------------------|----------------|
| Algorithm              | `lbfgs`        |
| L1 Regularization (`c1`)| `0.5`         |
| L2 Regularization (`c2`)| `1.0`         |
| Max Iterations         | `100`          |
| All Possible Transitions | `True`       |
| Class Weights          | Custom (inverse frequency) |

> ⚖️ `ingredient` was down-weighted to balance its dominance in the training data.

---

## 📊 Evaluation on Validation Set

### 🔍 Classification Report

| Label       | Precision | Recall | F1-Score | Support |
|-------------|-----------|--------|----------|---------|
| ingredient  | 0.984     | 0.996  | 0.990    | 2107    |
| quantity    | 0.988     | 0.985  | 0.987    | 411     |
| unit        | 0.979     | 0.911  | 0.944    | 358     |
| **Overall** |           |        | **0.984 Accuracy** | 2876 |

---

## 💡 Key Insights

- **High accuracy (98.4%)** achieved using CRF for structured extraction.
- `ingredient` class shows strong performance due to high support.
- `unit` and `quantity` suffer from ambiguity (e.g., `few`, `tablespoon`, `spoon`).
- Contextual features (previous and next tokens) significantly improved accuracy.
- Regex patterns and domain-specific keywords are effective for entity detection.
- Misclassifications mostly occurred with overlapping vocabulary and inconsistent unit formats.

---

## 📁 Files Included

- `ingredient_and_quantity.json` – Input dataset
- `ner_crf_model.pkl` – Trained CRF model
- `pos_tag_distribution.png` – POS tag imbalance plot
- `NER_Recipe_Data_Report.pdf` – Project summary report

---

## 🚀 Future Enhancements

- Introduce BiLSTM-CRF or transformer-based models (e.g., BERT)
- Expand labeled data for underrepresented tags like `unit`
- Add lemmatized normalization for unit and quantity variants
- Integrate into a recipe search engine or cooking app backend

---

## 🤝 Contributions

Contributions, bug reports, and improvements are welcome!  
Feel free to fork the repo and open a pull request.

---

## 📜 License

This project is licensed under the MIT License.

---
