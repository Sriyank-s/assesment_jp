# README — Running the Census Income Classification & Segmentation Project

This document explains **how to install dependencies and execute the full project** from scratch.

The project contains two components:

1. **Income Classification Model** — predicts income >50K or ≤50K
2. **Customer Segmentation Model** — groups customers for marketing

All implementation is inside:

```
jp4.ipynb
```

---

## 1. System Requirements

### Python

Python **3.8 or higher** is required.

Check version:

```bash
python --version
```

If not installed, download from:
https://www.python.org/downloads/

---

## 2. Required Libraries

The notebook depends on the following libraries:

| Library      | Purpose                    |
| ------------ | -------------------------- |
| numpy        | numerical operations       |
| pandas       | dataset handling           |
| matplotlib   | plotting                   |
| seaborn      | visualization              |
| scikit-learn | preprocessing + evaluation |
| lightgbm     | classification model       |
| jupyter      | notebook execution         |

---

## 3. Install Dependencies

Run this command in terminal inside the project folder:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn lightgbm jupyter
```

### If pip is not installed

Install pip first:

**Windows**

```bash
python -m ensurepip --upgrade
```

**Mac/Linux**

```bash
sudo apt install python3-pip
```

Then rerun:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn lightgbm jupyter
```

---

## 4. Dataset Setup

Place these files in the same directory:

```
census-bureau.data
census-bureau.columns
jp4.ipynb
```

Directory example:

```
project/
│── jp4.ipynb
│── census-bureau.data
│── census-bureau.columns
```

---

## 5. Running the Project

### Step 1 — Launch Notebook

Open terminal in the folder:

```bash
jupyter notebook
```

Open:

```
jp4.ipynb
```

---

### Step 2 — Execute Entire Pipeline

Run cells **from top to bottom**:

```
Kernel → Restart & Run All
```

Do NOT skip cells — later sections depend on earlier preprocessing.

---

## 6. What the Notebook Executes

### Part A — Data Preparation

* Loads census dataset
* Cleans missing values
* Creates target variable `income_high`
* Removes leakage columns

---

### Part B — Preprocessing Pipeline

Automatically builds ML preprocessing:

* Numeric → StandardScaler
* Categorical → OneHotEncoder
* Combined via ColumnTransformer

---

### Part C — Income Classification

Trains LightGBM model:

* Train/validation/test split
* Class imbalance handling
* Threshold optimization
* Final evaluation metrics

Outputs:

* Accuracy
* Precision / Recall / F1
* PR-AUC
* Feature importance plot

---

### Part D — Customer Segmentation

Performs clustering:

* Removes label
* Encodes features
* PCA dimensionality reduction
* KMeans clustering
* Generates marketing segments

Outputs:

* Cluster characteristics
* Income distribution per group
* Business interpretation

---

## 7. Expected Runtime

| Step           | Approx Time |
| -------------- | ----------- |
| Preprocessing  | 1–2 min     |
| Classification | 2–4 min     |
| Segmentation   | 2–3 min     |
| Total          | ~10 minutes |

(Depends on CPU/RAM)

---

## 8. Outputs Produced

Inside notebook you will see:

### Classification

* Model performance metrics
* Threshold tuning results
* Feature importance

### Segmentation

* Cluster profiles
* Customer personas
* Marketing recommendations

No extra files are created — everything is displayed in notebook.

---

## 9. Troubleshooting

### ModuleNotFoundError

Install missing package:

```bash
pip install <package>
```

### File Not Found

Ensure dataset files are in same folder as notebook.

### LightGBM Installation Issue (Windows)

If installation fails:

```bash
pip install lightgbm --only-binary :all:
```

---

## 10. Reproducibility

Random seeds are fixed.
Running multiple times will produce consistent results.

---

You can now execute the entire pipeline and reproduce both models end-to-end.
