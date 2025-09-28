# Consumer Complaint Text Classifier

This repository contains a machine learning pipeline that classifies consumer complaints into **four predefined categories**:

* Credit reporting, repair, or other
* Debt collection
* Consumer Loan
* Mortgage

The workflow includes data preparation, cleaning, feature extraction, model training, evaluation, and prediction.

---

## Dataset

* Source: Consumer Complaint Database
* The raw dataset is very large (~6 GB zipped).
* Only complaints that belong to the four target categories are retained.
* A preprocessed version is stored as `preprocessed_complaint.csv`.

---

## Project Workflow

### 1. Data Splitting

* The raw CSV is too large to process at once, so it is read in chunks (100,000 rows each).
* Only the required complaint categories are extracted.
* Each filtered chunk is saved in the `splits/` folder for easier handling.

### 2. Exploratory Data Analysis (EDA)

* Visualizations of category counts.
* Distribution of complaint text lengths.
* (Optional) Word clouds to highlight frequently used terms per category.

### 3. Text Cleaning

* Convert text to lowercase.
* Remove punctuation, numbers, and stopwords.
* Apply lemmatization.
* Discard very short words (<=2 characters).
* Drop rows with no remaining text.

### 4. Feature Engineering

* Text is converted into numerical features using **TF-IDF**.
* `max_features=5000` is set to balance accuracy and memory requirements.

### 5. Model Training

* **Random Forest Classifier** with:

  * `n_estimators=100`
  * `class_weight="balanced"` to reduce class imbalance.
* Dataset is split into 80% training and 20% testing sets.

### 6. Model Evaluation

* Accuracy score.
* Precision, Recall, and F1-score (classification report).
* Confusion matrix visualization.

### 7. Predictions

* A helper function allows predictions on new complaints.
* Example:

  ```
  "I keep receiving calls from agencies about a loan I never applied for."
  → Predicted Category: Debt collection
  ```

---

## Folder Structure

```
Consumer_Complaint_Text_Classification/
│
├─ splits/                     # Contains chunked CSV files
├─ preprocessed_complaint.csv  # Cleaned dataset
├─ main_pipeline.py            # Full pipeline implementation
├─ README.md                   # Project documentation
└─ requirements.txt            # Python dependencies
```

---

## Requirements

* pandas
* numpy
* nltk
* scikit-learn
* matplotlib
* seaborn
* xgboost
* wordcloud *(optional)*

Install all dependencies:

```bash
pip install -r requirements.txt
```

---

## Usage

* Run the full pipeline with:

```bash
python main_pipeline.py
```

* Use pandas or another tool for working with very large CSVs.
* Note: Excel can only handle files up to ~1M rows.

---

## Performance Notes

* Training on ~1.3M rows may take 15–45 minutes depending on hardware.
* Adjust `max_features` in TF-IDF to optimize speed and memory usage.

---

## Author

**Manasa Reddy**
