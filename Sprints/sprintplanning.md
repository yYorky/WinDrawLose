# Sprint Planning Document: Football Match Outcome Prediction (WinDrawLose)

* **Created**: 26 Aug 2025
* **Last Updated**: 26 Aug 2025

## Project Overview

We aim to build a **production-grade ML MVP** that predicts the outcome (Win/Draw/Lose) of football matches based on user-provided inputs. The final deliverable will be a **dockerised ML pipeline** with modular components for data extraction, cleaning, feature engineering, model training, evaluation, inference, and a webapp demo with explainability.

Users should be able to run the pipeline end-to-end or execute individual components (e.g., only retrain the model, only run inference) via a simple CLI command, configured through a `config.yaml` file.

---

## Sprint Plan (1 week per sprint)

### **Sprint 1 – Data Discovery & EDA**

**Goals:**

* Identify and evaluate available datasets (Kaggle, Football-Data.co.uk, DataHub, OpenFootball, APIs, scraping)【5†ChatGPT Deep Research.pdf】.
* Document reliability, update frequency, ease of access, and cost.
* Select core dataset(s) for initial MVP (e.g., Kaggle Club Football 2000–2025, Football-Data.co.uk).
* Perform Exploratory Data Analysis (EDA): outcome distribution, missing values, feature correlations.
* Create initial schema and metadata documentation.

**Deliverables:**

* Data discovery report
* Jupyter notebook with EDA visuals
* Initial draft of `config.yaml` for data sources

---

### **Sprint 2 – Data Extraction Pipeline**

**Goals:**

* Implement reproducible pipeline to extract raw match data.
* Support multiple data sources (CSV from Kaggle, Football-Data.co.uk API, scraping module if needed).
* Standardise storage format (Parquet/CSV).

**Deliverables:**

* `src/data_extraction.py`
* Config-driven extraction via CLI (`python main.py extract --config config.yaml`)
* Unit tests for data ingestion

---

### **Sprint 3 – Data Cleaning Pipeline**

**Goals:**

* Implement pipeline for data cleaning and normalization:

  * Handle missing values
  * Standardize team names, date formats
  * Remove duplicates
  * Validate outcome labels
* Modular structure so it can be re-run on new data.

**Deliverables:**

* `src/data_cleaning.py`
* CLI integration (`python main.py clean --config config.yaml`)
* Data quality report

---

### **Sprint 4 – Feature Engineering Pipeline**

**Goals:**

* Generate predictive features:

  * Team form (e.g., last 5 matches results, goals scored/conceded)
  * Home/away advantage
  * Elo/SPI ratings (from external sources)
  * Betting odds (if available)
* Store engineered dataset for training.

**Deliverables:**

* `src/feature_engineering.py`
* Feature documentation
* Updated `config.yaml` with feature toggles

---

### **Sprint 5 – Model Training Pipeline**

**Goals:**

* Implement training pipeline:

  * Train baseline models (Logistic Regression, Decision Tree, Random Forest, Gradient Boosting).
  * Enable re-training with new data.
  * Save trained models with versioning.
* Config-driven selection of model and hyperparameters.

**Deliverables:**

* `src/model_training.py`
* CLI command (`python main.py train --config config.yaml`)
* Model registry (local directory or MLflow integration)

---

### **Sprint 6 – Model Evaluation**

**Goals:**

* Evaluate models with proper metrics:

  * Accuracy, Precision, Recall, F1, AUC-ROC
  * Confusion Matrix
  * Cross-validation
* Select best-performing model.

**Deliverables:**

* Evaluation notebook and plots
* Metrics stored as JSON/CSV for reproducibility
* Auto-selection of best model for inference

---

### **Sprint 7 – Inference Pipeline**

**Goals:**

* Implement pipeline to load trained model and run inference on user inputs.
* Support both batch prediction and single-match prediction.
* Ensure CLI integration.

**Deliverables:**

* `src/inference.py`
* CLI command (`python main.py infer --config config.yaml`)
* Example test cases with sample predictions

---

### **Sprint 8 – Webapp Demo (with Explainability)**

**Goals:**

* Build interactive webapp (Streamlit/Flask) for predictions.
* User inputs: team names, match date, optional odds, etc.
* Outputs: predicted outcome (Win/Draw/Lose) with probabilities.
* Integrate SHAP explainability to show feature contributions.
* Add analytics dashboard: team form trends, odds vs predictions, etc.

**Deliverables:**

* `app/` folder with webapp code
* SHAP plots (waterfall, beeswarm)
* Docker-compose setup for webapp

---

### **Sprint 9 – Dockerisation & CLI Orchestration**

**Goals:**

* Dockerise the entire pipeline for easy reuse.
* Single entrypoint (`main.py`) to run:

  * `extract`
  * `clean`
  * `feature`
  * `train`
  * `evaluate`
  * `infer`
  * `webapp`
* Finalise `config.yaml` for flexible control.

**Deliverables:**

* `Dockerfile` and `docker-compose.yaml`
* Final `config.yaml`
* End-to-end tested Docker container

---

### **Sprint 10 – Documentation & Handover**

**Goals:**

* Write detailed documentation:

  * Project structure
  * How to run each step
  * How to retrain/update model
  * Deployment instructions
* Add contribution guidelines for future collaborators.

**Deliverables:**

* `README.md`
* `docs/` folder with usage examples
* Technical report (data discovery, modeling approach, evaluation)

---

## Final Deliverables

* Dockerised ML pipeline
* Configurable CLI interface
* Production-ready trained model
* Webapp demo with SHAP explainability
* Documentation for future improvements
