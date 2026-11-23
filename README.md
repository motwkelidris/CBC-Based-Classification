# CBC-Based Classification of Viral Infection, Bacterial Infection and Anemia

A machine learning project that classifies patients as **viral infection**, **bacterial infection**, **anemia**, their combinations, or **normal** from Complete Blood Count (CBC) test results.

> ⚠️ **Disclaimer:** This is a practical Machine learning project  built on a **synthetic dataset**. It is **not** a medical device and must not be used for real clinical diagnosis.

---

## Overview

A CBC is one of the most common blood tests. Different conditions leave different patterns in it:

| Condition | Main CBC markers |
|---|---|
| Anemia | Low HGB and HCT (cutoffs depend on gender) |
| Viral infection | Lymphocytosis (high LYM% / LYM#), low or normal WBC |
| Bacterial infection | Neutrophilia (high NE% / NE#), high WBC |

This project trains and compares several classification algorithms to recognize these patterns. A patient can have more than one condition at the same time, so the problem has **8 classes**.

## Classes

`normal`, `anemia`, `viral`, `bacterial`, `anemia+viral`, `anemia+bacterial`, `viral+bacterial`, `anemia+viral+bacterial`

## Dataset

The dataset contains **20,000 synthetic patient records**, generated programmatically in Python (no real patients).

- **Features:** Gender, WBC, HGB, HCT,  PLT, LYM#, LYM%, NE#, NE%.
- **Target:** `Class` (the concatenated diagnosis), also available as three binary columns: `Anemia`, `Viral`, `Bacterial`
- **Reference ranges:** standard adult CBC values, with these ranges for the white cell parameters:

| Parameter | Normal range |
|---|---|
| WBC | 4.0 – 11.0 ×10³/µL |
| LYM# | 0.80 – 4.0 ×10³/µL |
| LYM% | 20.0 – 40.0 % |
| NE# | 2.0 – 7.8 ×10³/µL |
| NE% | 50.0 – 70.0 % |

- **Labeling rules:**
  - Anemia: HGB below 12 g/dL (female) or below 13 g/dL (male)
  - Viral: LYM% above 40, or LYM# above 4.0, or WBC below 4.0
  - Bacterial: NE% above 70, or NE# above 7.8, or WBC above 11.0
  - Normal: none of the above
  - Combined diagnoses are concatenated, e.g. `anemia+viral`

Because real labeled patient data was not available, the values were generated from distributions based on typical clinical CBC patterns. The class proportions are balanced by design and do not reflect real-world prevalence.

## Models and Results

| Model | Accuracy |
|---|---|
| Random Forest | **0.99675** |
| Gradient Boosting | 0.9875 |
| K-Nearest Neighbors (KNN) | 0.901 |
| Logistic Regression | 0.8665 |

Random Forest performed best. Tree-based models fit this dataset well because the labels follow threshold rules on the CBC values.

## Limitations

- The data is synthetic, and the labels come from explicit rules. The high accuracy shows that the models can learn these rules, not that they would perform the same on real patients.
- Real CBC data is noisier. Conditions overlap, and values near the cutoffs are harder to classify.
- Validation on real, ethically approved clinical data is needed before drawing any clinical conclusion.

## Tech Stack

Python, pandas, NumPy, scikit-learn, Matplotlib / Seaborn

## Author

**Motwkel idris** – [GitHub](https://github.com/motwkelidris) · [LinkedIn](https://www.linkedin.com/in/motwkel-idris)

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
