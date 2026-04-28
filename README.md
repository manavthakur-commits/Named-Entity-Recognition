# Enterprise-Grade NER: Extracting Entities from Fake vs. Real News

![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)
![NLP](https://img.shields.io/badge/NLP-spaCy%20%7C%20scikit--learn-green)
![VectorDB](https://img.shields.io/badge/VectorDB-Pinecone%20%7C%20Chroma-orange)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

## 📌 Project Overview
This project implements a scalable Named Entity Recognition (NER) pipeline designed to extract structured entities (People, Organizations, Locations, Dates) from a corpus of fake and real news articles. 

The primary objective is to demonstrate a rigorous, architectural understanding of Natural Language Processing (NLP) by benchmarking classical statistical methods against modern vector-based semantic retrieval systems. By comparing the entity structures of verified news against disinformation, this project also provides analytical value beyond standard text parsing.

## 🏗️ Architecture & Methodology
To rigorously evaluate performance, the project is divided into two distinct modeling phases:

### Phase 1: Foundational Statistical Baseline
Built to establish a performance baseline and showcase classical feature engineering mechanics without relying on "black-box" APIs.
* **Preprocessing:** Tokenization, lemmatization, and POS tagging using `spaCy`.
* **Feature Extraction:** Statistical representation of tokens utilizing **Bag of Words (BoW)**, **N-grams**, and **TF-IDF**.
* **Algorithm:** A Conditional Random Fields (CRF) or Logistic Regression classifier to predict sequence tags based on engineered features.

### Phase 2: Modern Vector-Based Semantic Retrieval
Contrasts the sparse matrix limitations of the baseline by capturing deep semantic meaning and enabling high-speed similarity search.
* **Dense Embeddings:** Replaces TF-IDF matrices with dense vector representations (Word2Vec / Transformer embeddings).
* **Storage & Retrieval:** Integrates a **Vector Database** (e.g., ChromaDB/Pinecone) to store entity embeddings, demonstrating how enterprise systems perform rapid similarity searches on extracted intelligence.

## 📊 Dataset & Citation
This model is trained and evaluated on a Fake and Real News dataset, providing a robust, real-world corpus of unstructured text. 


## 📂 Repository Structure
```text
├── data/                   # Raw and processed datasets (ignored in git)
├── notebooks/              # Jupyter notebooks for initial EDA and model prototyping
├── src/                    # Source code for production pipeline
│   ├── data_loader.py      # Data ingestion and cleaning scripts
│   ├── preprocess.py       # spaCy tokenization and feature engineering
│   ├── baseline_model.py   # TF-IDF and classical ML training scripts
│   └── vector_model.py     # Embedding generation and Vector DB integration
├── requirements.txt        # Project dependencies
└── README.md               # Project documentation
