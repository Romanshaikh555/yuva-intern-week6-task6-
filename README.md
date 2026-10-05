<div align="center">

# 🐧 Penguin Species Prediction and Grouping

### Capstone Project - Yuva Intern / NSDC - Virtual Data Science with Python (Week 6)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter&logoColor=white)
![scikit-learn](https://img.shields.io/badge/ML-scikit--learn-f7931e?logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Notebook-runs%20end%20to%20end-brightgreen)
![Accuracy](https://img.shields.io/badge/CV%20accuracy-99.4%25-success)

**Can we tell a penguin's species from a few body measurements, and do the measurements form natural groups on their own?**

</div>

---

## 📑 Quick Navigation

[Overview](#-overview) · [Results](#-results-at-a-glance) · [Visual Tour](#-visual-tour) · [Pipeline](#-pipeline) · [Run It](#-run-it-in-5-steps) · [Files](#-project-files) · [FAQ](#-faq) · [Data Source](#-data-source)

---

## 🔎 Overview

This project runs a **complete data science pipeline** on the public **Palmer Penguins** dataset (344 penguins, 3 species, 3 islands in Antarctica).

| Question | Type | Approach |
|---|---|---|
| Can we predict the species from body measurements, island and sex? | 🎯 Supervised | Logistic Regression, KNN, Random Forest, Gradient Boosting |
| Do the measurements form natural groups without labels? | 🧩 Unsupervised | K-Means, PCA, Hierarchical clustering |

---

## 📊 Results at a Glance

| Item | Result |
|---|---|
| Rows after cleaning | **342** (2 empty rows removed) |
| Best clustering | **Hierarchical (Ward, k=3)** - adjusted rand index **0.916** |
| K-Means (k=3) | adjusted rand index 0.793 |
| Cross validation accuracy | 0.978 to 0.993 across the four models |
| Final model | **Logistic Regression** (chosen by CV score) |
| Test accuracy | 100% on 69 test rows (small test set) |
| Repeated 5-fold CV accuracy | **about 99.4%** (the more realistic estimate) |
| Most important features | bill length, flipper length, bill depth |

<details>
<summary><b>🧠 Why is the test accuracy 100% but I quote 99.4%? (click to open)</b></summary>

<br>

The test set has only 69 penguins, so a perfect score can be partly luck. Repeated cross validation on all the data tests the model many times on different splits, so about **99.4%** is a more honest number to expect on new penguins.

</details>

---

## 🖼️ Visual Tour

> The images below appear when the `figures/` folder is next to this README (it is included in the zip, and the notebook also creates it when you run it).

<details open>
<summary><b>Exploring the data (EDA)</b></summary>

<br>

<p align="center">
  <img src="figures/04_boxplots_by_species.png" width="48%" alt="Box plots by species">
  <img src="figures/06_correlation_heatmap.png" width="40%" alt="Correlation heatmap">
</p>

**Takeaway:** Gentoo is clearly larger. Adelie and Chinstrap overlap, and bill length separates them best.

</details>

<details>
<summary><b>Unsupervised learning (clusters)</b></summary>

<br>

<p align="center">
  <img src="figures/09_pca_species_vs_kmeans.png" width="85%" alt="PCA species vs K-Means">
</p>

**Takeaway:** Natural groups match the real species well. Only Adelie vs Chinstrap gets mixed up.

</details>

<details>
<summary><b>Supervised learning (models)</b></summary>

<br>

<p align="center">
  <img src="figures/12_confusion_matrix.png" width="38%" alt="Confusion matrix">
  <img src="figures/13_feature_importance.png" width="52%" alt="Feature importance">
</p>

**Takeaway:** Bill length and flipper length matter most. Sex is almost unused.

</details>

---

## 🛠️ Pipeline

- [x] **1. Data collection** - seaborn Penguins dataset saved as `penguins.csv`
- [x] **2. Data cleaning** - missing values, duplicates, outliers
- [x] **3. EDA** - distributions, box plots, pair plot, correlation, island and sex
- [x] **4. Unsupervised learning** - K-Means (elbow and silhouette), PCA, hierarchical clustering
- [x] **5. Supervised learning** - 4 classifiers, 5-fold CV, GridSearchCV
- [x] **6. Evaluation** - accuracy, precision, recall, F1, confusion matrix, repeated CV, feature importance
- [x] **7. Conclusions** - limitations, recommendations, reflection

<details>
<summary><b>🧹 What exactly was cleaned?</b></summary>

<br>

- 2 rows had no measurements at all, so they were dropped
- 9 missing `sex` values are filled with the most frequent value inside the pipeline (learned from training data only, so there is no data leakage)
- 0 duplicate rows and 0 outliers (IQR rule), so nothing else was removed

</details>

---

## 🚀 Run It in 5 Steps

**1️⃣ Check Python (3.9 or newer)**
```bash
python --version
```

**2️⃣ Install the libraries**
```bash
pip install -r requirements.txt
```

**3️⃣ Keep `penguins.csv` in the same folder as the notebook**
(if it is missing, the notebook loads the data from seaborn, which needs internet)

**4️⃣ Open the notebook**
```bash
jupyter notebook Week6_Capstone_Penguins.ipynb
```

**5️⃣ Run everything:** click **Kernel > Restart & Run All** (takes about a minute)

> 🎲 The random state is fixed to 42, so you get the same results every time.

---

## 📁 Project Files

| File | What it is |
|---|---|
| 📓 `Week6_Capstone_Penguins.ipynb` | Main notebook with all code, outputs and plots |
| 📄 `Week6_Capstone_Report.docx` | Detailed project report |
| 📊 `penguins.csv` | Dataset (seaborn Penguins data) |
| 🖼️ `figures/` | All 13 plots as PNG files |
| 🧾 `results.json` | Key numbers saved by the notebook |
| 📦 `requirements.txt` | Python libraries needed |
| 📘 `README.md` | This file |

---

## ❓ FAQ

<details>
<summary><b>The notebook shows a "ModuleNotFoundError". What do I do?</b></summary>

<br>

Run `pip install -r requirements.txt` again, then restart the kernel. Make sure Jupyter uses the same Python where you installed the libraries.

</details>

<details>
<summary><b>The notebook cannot find penguins.csv.</b></summary>

<br>

Open Jupyter from the project folder (the folder that contains `penguins.csv`). If the file is still missing, the notebook falls back to seaborn, which needs internet.

</details>

<details>
<summary><b>Can I use a different dataset?</b></summary>

<br>

Yes, but the column names in the notebook (`species`, `island`, `bill_length_mm`, `bill_depth_mm`, `flipper_length_mm`, `body_mass_g`, `sex`) must be changed to match your data.

</details>

<details>
<summary><b>What are the limitations?</b></summary>

<br>

- Small dataset (342 penguins) and fairly easy problem
- 100% test accuracy comes from only 69 test rows
- `island` is almost a shortcut for species (Chinstrap lives only on Dream, Gentoo only on Biscoe)
- Data comes from three islands and a few years only

</details>

<details>
<summary><b>What could be done next?</b></summary>

<br>

- Train without the `island` feature to see how well body measurements alone work
- Try other models such as SVM and compare with statistical tests
- Use the same data for regression (predict body mass)
- Collect more data from more islands and years

</details>

---

## 🧪 Tested With

Python 3.12 · pandas 3.0 · numpy 2.4 · matplotlib 3.10 · seaborn 0.13 · scikit-learn 1.8 · scipy 1.17

---

## 📚 Data Source

**Palmer Penguins dataset.** Data collected by Dr. Kristen Gorman and the Palmer Station LTER. Loaded from the seaborn-data repository: <https://github.com/mwaskom/seaborn-data>

<div align="center">

⭐ Built as the final capstone of the Yuva Intern Virtual Data Science with Python program ⭐

</div>
