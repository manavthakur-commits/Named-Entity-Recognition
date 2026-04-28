Enterprise-Grade Named Entity Recognition (NER) Pipeline
An end-to-end Named Entity Recognition project that compares a classical sparse-feature pipeline against a modern vector-based architecture.

Architecture
This repository is split into two phases:

Phase 1: Bag of Words, n-grams, TF-IDF, and a token-level Logistic Regression baseline
Phase 2: Dense embeddings and vector database retrieval
The implemented baseline follows this flow:

Download and normalize CoNLL-2003
Export processed sentence records to JSONL
Convert each token into a local-context training example
Vectorize context text with TF-IDF and n-grams
Train a Logistic Regression classifier on token labels
Evaluate with precision, recall, and F1
Save artifacts for later CLI inference
Repository Structure
.
|-- configs/
|-- data/
|   |-- external/
|   |-- processed/
|   `-- raw/
|-- src/
|   |-- evaluation/
|   |-- features/
|   |-- ingestion/
|   |-- interface/
|   |-- models/
|   |-- preprocessing/
|   |-- utils/
|   `-- vector_store/
|-- tests/
|-- main.py
|-- pytest.ini
|-- requirements.txt
`-- requirements-vector.txt
Setup
Create a virtual environment and install the baseline dependencies:

python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
Optional Phase 2 vector dependencies are separated so the repository stays easier to install on Windows:

python -m pip install -r requirements-vector.txt
CLI Workflow
Inspect the available commands:

python main.py --help
Sanity-check the repository:

python main.py check
Download and export CoNLL-2003:

python main.py ingest-conll2003
Train the Phase 1 baseline:

python main.py train-baseline
Run prediction on raw text:

python main.py predict-text "Microsoft opened a new office in Seattle"
Optional Phase 2 vector indexing:

python main.py build-vector-index
python main.py query-similar "Microsoft"
CoNLL-2003 Processed Outputs
The ingestion command writes:

data/processed/train.jsonl
data/processed/validation.jsonl
data/processed/test.jsonl
data/processed/manifest.json
The generated dataset files and local cache are ignored by Git so the repository remains clean for upload.

Baseline Modeling Details
The classical baseline uses:

Local token windows with configurable window_size
TF-IDF over contextual token text
Unigram and bigram features
Logistic Regression for token-level BIO tag prediction
Current baseline configuration is stored in configs/model_config.yaml.

Saved Artifacts
Training produces:

models/classical/logreg_ner.joblib
models/classical/logreg_ner_metadata.json
outputs/metrics/validation_metrics.json
outputs/metrics/test_metrics.json
Current Results
Latest measured baseline metrics on CoNLL-2003:

Validation
Precision: 0.7941
Recall: 0.6463
F1: 0.7086
Test
Precision: 0.7157
Recall: 0.5697
F1: 0.6282
These values come from the saved evaluation artifacts in outputs/metrics/.

Example Prediction
Input:

Microsoft opened a new office in Seattle
Predicted entities:

Microsoft -> ORG
Seattle -> LOC
Testing
Run the test suite with:

pytest -q
Dependency Notes
requirements.txt contains the baseline stack for ingestion, preprocessing, testing, training, and inference.

requirements-vector.txt contains optional Phase 2 packages. On some Windows environments, chromadb may require native build tools.

The Phase 2 commands are implemented with lazy imports and clear error messages, so the baseline pipeline remains usable even when optional vector dependencies are not installed.

Dataset Citation
Tjong Kim Sang, E. F., and De Meulder, F. (2003). Introduction to the CoNLL-2003 shared task: Language-independent named entity recognition. In Proceedings of CoNLL-2003.
