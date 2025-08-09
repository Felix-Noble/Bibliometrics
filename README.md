# Bibliometrics: End-to-End data pipeline for forecasting academic impact from article abstracts

## Overview
This project implements a **two-stage, end-to-end machine learning pipeline** for acquiring, processing, and modeling scholarly publication data.  
It combines **large-scale data ingestion**, **feature engineering**, and **predictive modeling** to explore and forecast research impact.

The workflow is split into **two modular repositories**:
1. **Data Acquisition & Feature Engineering**
2. **Model Training, Hyperparameter Tuning & Temporal Cross-Validation**

---

## Project Workflow

### **1. Data Acquisition → Feature Extraction**  
**Repo:** [(Bibliometrics-Data)](https://github.com/Felix-Noble/Bibliometrics-Data)  
- **Scraping**:
  - Collects metadata, abstracts, and citation networks from the OpenAlex API.
  - Handles polite API usage, retries, and reference expansion.
- **Integration**:
  - Merges raw CSV batches into a unified, deduplicated Parquet dataset using Dask.
- **Feature Engineering**:
  - Generates bibliometric features (e.g., yearly citation medians, above/below median flags).
  - Creates semantic embeddings from titles and abstracts using SentenceTransformers.
  - Produces **reference-aware features** by incorporating embeddings of cited works.

---

### **2. Model Training → Hyperparameter Tuning → Temporal Cross-Validation**  
**Repo:** [(Bibliometrics-Forecasting)](https://github.com/Felix-Noble/Bibliometrics-Forecasting)  
- **Data Loading**:
  - Streams large datasets efficiently with `tf.data` pipelines and on-disk caching.
- **Model Architecture**:
  - Conv1D-based network processes sequences of reference embeddings + focal paper embedding.
- **Hyperparameter Optimization**:
  - Bayesian search with Keras Tuner over architecture and training parameters.
- **Temporal Cross-Validation**:
  - Sliding-window evaluation to prevent future data leakage.
  - Produces per-slice metrics (accuracy, balanced accuracy, precision, recall, PR curves).
- **Outputs**:
  - Best model saved in `.h5` format.
  - Metrics stored as CSV for reproducibility.

---

---

## Key Features
- **Config-driven architecture** for reproducibility.
- **Scalable data handling** with Dask, DuckDB, and PyArrow.
- **Semantic embeddings** for text representation.
- **Network-aware modeling** via reference embeddings.
- **Time-aware evaluation** for realistic forecasting.
- **Modular two-repo design** — each stage can be run independently.

---

## How to Explore
- **Stage 1:** [Data Acquisition & Feature Engineering]([https://github.com/Felix-Noble/Bibliometrics-Data])  
  Learn how raw scholarly data is scraped, cleaned, and transformed into rich feature sets.
- **Stage 2:** [Model Training & Evaluation]([https://github.com/Felix-Noble/Bibliometrics-Forecasting])  
  See how the processed data is used to train, tune, and evaluate predictive models.

---

## Author
**Felix Noble**  
Contact: `felix.noble@live.co.uk`  
LinkedIn: *(https://www.linkedin.com/in/felix-noble-6901b117b/)*  
Portfolio: *[(GitHub)](https://github.com/Felix-Noble)*

---
