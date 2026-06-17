# MLOps Portfolio — 10-Project Series

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue)](https://www.python.org/)
[![MLflow](https://img.shields.io/badge/MLflow-3.13-orange)](https://mlflow.org/)
[![Airflow](https://img.shields.io/badge/Airflow-2.9-red)](https://airflow.apache.org/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-ready-326CE5)](https://kubernetes.io/)
[![Docker](https://img.shields.io/badge/Docker-ready-2496ED)](https://www.docker.com/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688)](https://fastapi.tiangolo.com/)
[![Optuna](https://img.shields.io/badge/Optuna-3.6-purple)](https://optuna.org/)
[![DVC](https://img.shields.io/badge/DVC-3.50-945DD6)](https://dvc.org/)
[![License](https://img.shields.io/badge/License-MIT-lightgrey)](LICENSE)

**CI Status**

[![MLOps Tournament CI/CD](https://github.com/jumma786/mlops-model-tournament/actions/workflows/tournament.yml/badge.svg)](https://github.com/jumma786/mlops-model-tournament/actions)
[![Retraining Pipeline CI/CD](https://github.com/jumma786/mlops-retraining-pipeline/actions/workflows/ci.yml/badge.svg)](https://github.com/jumma786/mlops-retraining-pipeline/actions)
[![Feature Pipeline CI/CD](https://github.com/jumma786/mlops-feature-pipeline/actions/workflows/feature_pipeline.yml/badge.svg)](https://github.com/jumma786/mlops-feature-pipeline/actions)
[![Hyperparameter Tuning CI/CD](https://github.com/jumma786/mlops-hyperparameter-tuning/actions/workflows/tuning.yml/badge.svg)](https://github.com/jumma786/mlops-hyperparameter-tuning/actions)
[![Model Serving CI/CD](https://github.com/jumma786/mlops-model-serving/actions/workflows/serving.yml/badge.svg)](https://github.com/jumma786/mlops-model-serving/actions)
[![Feature Store CI/CD](https://github.com/jumma786/mlops-feature-store/actions/workflows/feature_store.yml/badge.svg)](https://github.com/jumma786/mlops-feature-store/actions)
[![Model Monitoring CI/CD](https://github.com/jumma786/mlops-model-monitoring/actions/workflows/monitoring.yml/badge.svg)](https://github.com/jumma786/mlops-model-monitoring/actions)
[![A/B Testing CI/CD](https://github.com/jumma786/mlops-ab-testing/actions/workflows/ab_testing.yml/badge.svg)](https://github.com/jumma786/mlops-ab-testing/actions)
[![Airflow Pipeline CI/CD](https://github.com/jumma786/mlops-airflow-pipeline/actions/workflows/pipeline.yml/badge.svg)](https://github.com/jumma786/mlops-airflow-pipeline/actions)
[![K8s Platform CI/CD](https://github.com/jumma786/mlops-k8s-platform/actions/workflows/k8s.yml/badge.svg)](https://github.com/jumma786/mlops-k8s-platform/actions)

**[Explore the Interactive Architecture Dashboard](https://mlops-portfolio-dashboard.vercel.app)** — 396 nodes, 437 edges, 8 architectural layers, 12-step guided tour

> End-to-end MLOps pipeline built across 10 standalone projects — from automated model selection through hyperparameter search, containerised serving, feature stores, drift monitoring, A/B testing, Airflow orchestration, and Kubernetes deployment. Every project has GitHub Actions CI/CD and pytest coverage.
>
> **Champion model:** XGBoost on UCI Bank Marketing — 0.82 AUC, 41,188 rows, 19 features.

---

## Portfolio at a Glance

| # | Project | Key Problem Solved | Core Tech | Repo |
|---|---|---|---|---|
| 1 | [Multi-Model Tournament](#1--multi-model-tournament) | Which model wins? Automate the decision | MLflow, XGBoost, LightGBM, CatBoost | [→](https://github.com/jumma786/mlops-model-tournament) |
| 2 | [Scheduled Retraining](#2--scheduled-retraining-pipeline) | Models go stale — retrain on new data automatically | DVC, MLflow, champion gate | [→](https://github.com/jumma786/mlops-retraining-pipeline) |
| 3 | [Feature Engineering Pipeline](#3--feature-engineering-pipeline) | Changing features shouldn't require retraining the model | sklearn transformers, MLflow artifacts | [→](https://github.com/jumma786/mlops-feature-pipeline) |
| 4 | [Hyperparameter Tuning](#4--hyperparameter-tuning) | Default params leave performance on the table | Optuna, MLflow nested runs | [→](https://github.com/jumma786/mlops-hyperparameter-tuning) |
| 5 | [Model Serving](#5--model-serving) | Put the champion model in front of real users | FastAPI, Docker, Cloud Run | [→](https://github.com/jumma786/mlops-model-serving) |
| 6 | [Feature Store](#6--feature-store) | Training and serving use different feature logic | Parquet offline store, FastAPI | [→](https://github.com/jumma786/mlops-feature-store) |
| 7 | [Model Monitoring](#7--model-monitoring) | Know when the model is drifting before users notice | PSI, KS-test, Chi-squared | [→](https://github.com/jumma786/mlops-model-monitoring) |
| 8 | [A/B Testing](#8--ab-testing-framework) | Replace the champion only when statistically justified | Z-test, Cohen's h, FastAPI router | [→](https://github.com/jumma786/mlops-ab-testing) |
| 9 | [Airflow Orchestration](#9--airflow-ml-pipeline) | Coordinate all pipeline steps with dependencies and retries | Apache Airflow, XCom | [→](https://github.com/jumma786/mlops-airflow-pipeline) |
| 10 | [Kubernetes Platform](#10--kubernetes-ml-platform) | Run the serving API at production scale with autoscaling | K8s, Helm, Prometheus, HPA | [→](https://github.com/jumma786/mlops-k8s-platform) |

---

## End-to-End Pipeline

```
┌─────────────────────────────────────────────────────────────────────┐
│                        DATA LAYER                                    │
│   UCI Bank Marketing (41,188 rows)   UCI Online Retail II (1M+ rows)│
└──────────────────────┬──────────────────────────────────────────────┘
                       │
          ┌────────────▼────────────┐
          │  Project 1              │
          │  MODEL TOURNAMENT       │  5 models → champion selection
          │  RandomForest wins      │  MLflow experiment tracking
          └────────────┬────────────┘
                       │
          ┌────────────▼────────────┐     ┌─────────────────────────┐
          │  Project 2              │     │  Project 3               │
          │  SCHEDULED RETRAINING   │     │  FEATURE PIPELINE        │
          │  DVC versioning         │     │  5 custom transformers   │
          │  Champion/challenger    │     │  Decoupled from model    │
          └────────────┬────────────┘     └────────────┬────────────┘
                       │                               │
          ┌────────────▼────────────────────────────────▼────────────┐
          │  Project 4 — HYPERPARAMETER TUNING                        │
          │  Optuna TPE · 30+ trials · each = MLflow child run        │
          │  XGBoost beats RandomForest baseline (0.8176 AUC)         │
          └────────────────────────────┬──────────────────────────────┘
                                       │
               ┌───────────────────────▼─────────────────────────┐
               │  Project 5 — MODEL SERVING                        │
               │  FastAPI REST API · Docker · Cloud Run            │
               │  /predict · /predict-batch · /health              │
               └───────────────┬──────────────────────────────────┘
                               │
      ┌────────────────────────┼────────────────────────┐
      │                        │                        │
┌─────▼──────────┐   ┌─────────▼───────┐   ┌──────────▼─────────┐
│  Project 6      │   │  Project 7       │   │  Project 8          │
│  FEATURE STORE  │   │  MONITORING      │   │  A/B TESTING        │
│  RFM features   │   │  PSI · KS · χ²  │   │  50/50 split        │
│  Parquet+FastAPI│   │  3 prod windows  │   │  Z-test + Cohen's h │
└─────────────────┘   └─────────────────┘   └────────────────────┘
                                       │
               ┌───────────────────────▼─────────────────────────┐
               │  Project 9 — AIRFLOW ORCHESTRATION               │
               │  Full DAG · ingest → features → train → validate │
               │  XCom state · weekly schedule · retry logic      │
               └───────────────┬──────────────────────────────────┘
                               │
               ┌───────────────▼──────────────────────────────────┐
               │  Project 10 — KUBERNETES PLATFORM                 │
               │  Deployment · HPA (2→10 pods) · Prometheus        │
               │  Helm chart · rolling updates · zero downtime     │
               └──────────────────────────────────────────────────┘
```

---

## Project Details

### 1 · Multi-Model Tournament

**Repo:** [mlops-model-tournament](https://github.com/jumma786/mlops-model-tournament)

Trains 5 models simultaneously, logs every run to MLflow, auto-selects the champion by AUC, and gates promotion to the registry. No human needed in the decision loop.

| Metric | Value |
|---|---|
| Models evaluated | LogisticRegression, RandomForest, XGBoost, LightGBM, CatBoost |
| Champion | RandomForest — AUC 0.8174 |
| Dataset | UCI Bank Marketing, 41,188 rows |
| Tests | 13 passing |
| CI trigger | Push to `main` + weekly cron (Mon 06:00 UTC) |

**MLOps concepts:** experiment tracking, model versioning, champion/challenger, CI/CD for ML, leakage discipline (`duration` dropped), class imbalance (`class_weight="balanced"`).

---

### 2 · Scheduled Retraining Pipeline

**Repo:** [mlops-retraining-pipeline](https://github.com/jumma786/mlops-retraining-pipeline)

Solves model decay: datasets are versioned with DVC (MD5 hash per batch), retraining runs weekly on new data, and a champion gate only promotes if AUC improves.

| Data Batch | Rows | AUC | Promoted |
|---|---|---|---|
| v1 — Q1 (Jan–Mar) | 546 | 0.6397 | YES — first run |
| v2 — Q2 (Apr–Jun) | 21,719 | 0.7719 | YES (+0.13) |
| v3 — Q3 (Jul–Sep) | 13,922 | 0.7828 | YES (+0.01) |

**MLOps concepts:** data versioning (DVC), audit trail (JSONL), Change Data Capture (MD5), scheduled retraining, champion/challenger gating.

---

### 3 · Feature Engineering Pipeline

**Repo:** [mlops-feature-pipeline](https://github.com/jumma786/mlops-feature-pipeline)

Packages feature engineering as 5 versioned sklearn transformers, logs the fitted pipeline as a separate MLflow artifact, and decouples it from the model — either can be updated independently.

| Transformer | What it does |
|---|---|
| `DurationDropper` | Removes leakage feature |
| `CategoricalEncoder` | Label-encodes all object columns |
| `EconomicFeatureEngineer` | Creates euribor × emp.var.rate interaction |
| `CampaignIntensityEncoder` | Customer fatigue signal from campaign count |
| `ContactRecencyEncoder` | Recency bucket from `pdays` |

Input: 20 features → Output: 22 features. Tests: 17 passing.

**MLOps concepts:** versioned feature pipelines, feature/model decoupling, custom `BaseEstimator`+`TransformerMixin` pattern.

---

### 4 · Hyperparameter Tuning

**Repo:** [mlops-hyperparameter-tuning](https://github.com/jumma786/mlops-hyperparameter-tuning)

Replaces grid search with Optuna's Bayesian (TPE) sampler. Every trial is logged as an MLflow child run under a parent experiment. Champion only registers if it beats the Project 1 baseline.

| Model | Trials | Best CV AUC | Test AUC | vs Baseline |
|---|---|---|---|---|
| XGBoost | 30 | 0.7975 | 0.8176 | +0.0002 |

**MLOps concepts:** Bayesian hyperparameter search, MLflow nested runs (parent/child), champion gating vs baseline, reproducibility (fixed seeds + full param logging).

---

### 5 · Model Serving

**Repo:** [mlops-model-serving](https://github.com/jumma786/mlops-model-serving)

Deploys the XGBoost champion as a production FastAPI service — containerised with a multi-stage Docker build, non-root user, health check, and Cloud Run-ready.

| Endpoint | Method | Purpose |
|---|---|---|
| `/health` | GET | Health check + model metadata |
| `/model-info` | GET | Full model provenance |
| `/predict` | POST | Single customer prediction |
| `/predict-batch` | POST | High-throughput batch inference |

Returns: `{ prediction, probability, label, confidence, model_version }`. Tests: 11 passing.

**MLOps concepts:** REST API serving, Pydantic input validation, Docker multi-stage build, CI trains → tests → builds → tests container.

---

### 6 · Feature Store

**Repo:** [mlops-feature-store](https://github.com/jumma786/mlops-feature-store)

Built on UCI Online Retail II (1M+ rows). Computes RFM features and customer stats, stores them as Parquet snapshots (offline store), and serves live lookups via FastAPI (online store).

| Metric | Value |
|---|---|
| Dataset | UCI Online Retail II — 1,067,371 rows, Dec 2009–Dec 2011 |
| Unique customers | 5,877 |
| Features computed | 19 (RFM quintile scores, behavioural stats) |
| Segments | Champions (~22%), Loyal (~25%), At Risk (~27%), Lost (~26%) |
| Champions avg spend | £3,200+ |

**MLOps concepts:** offline/online store pattern, point-in-time correctness (snapshot dates prevent leakage), RFM segmentation, feature reuse (no training/serving skew).

---

### 7 · Model Monitoring

**Repo:** [mlops-model-monitoring](https://github.com/jumma786/mlops-model-monitoring)

Monitors the XGBoost champion for distribution shift across 3 simulated production windows using three complementary statistical tests.

| Test | Features | Alert Threshold |
|---|---|---|
| PSI | 9 numerical | > 0.25 = significant drift |
| KS-test | 9 numerical | p < 0.05 |
| Chi-squared | 10 categorical | p < 0.05 |

| Window | Key Change | Alert Level |
|---|---|---|
| Baseline (Jan–Mar) | Training distribution | None |
| Mild Drift (Apr–Jun) | Contact method shift | Moderate |
| Strong Drift (Jul–Sep) | Euribor drops 5.1 → 0.6 | **Significant** |

Tests: 16 passing.

**MLOps concepts:** PSI, KS-test, chi-squared drift detection, prediction drift vs feature drift, JSON monitoring reports.

---

### 8 · A/B Testing Framework

**Repo:** [mlops-ab-testing](https://github.com/jumma786/mlops-ab-testing)

Routes live prediction traffic 50/50 between the Control (LogisticRegression, ~0.77 AUC) and Challenger (XGBoost, ~0.82 AUC). Tracks conversions and runs significance tests on demand.

| Variant | Model | AUC |
|---|---|---|
| Control (A) | Logistic Regression | ~0.77 |
| Challenger (B) | XGBoost | ~0.82 |

Promotion decision requires: p < 0.05 (Z-test) **and** lift > 1% (Cohen's h) **and** challenger AUC > control AUC.

**MLOps concepts:** traffic splitting, Z-test, Cohen's h, conversion tracking, champion promotion gate.

---

### 9 · Airflow ML Pipeline

**Repo:** [mlops-airflow-pipeline](https://github.com/jumma786/mlops-airflow-pipeline)

Orchestrates the full training pipeline as an Airflow DAG with proper dependency handling, XCom state passing between tasks, retry logic, and a weekly schedule.

```
start → ingest_data → engineer_features → train_model → validate_model → notify → end
```

| Task | Output | XCom Key |
|---|---|---|
| `ingest_data` | Parquet file | `data_path`, `n_rows` |
| `engineer_features` | Feature matrix | `feature_path`, `n_features` |
| `train_model` | Saved model + AUC | `model_path`, `auc` |
| `validate_model` | Pass/fail vs 0.75 threshold | `validated` |

**MLOps concepts:** DAG orchestration, XCom state passing, retry logic, validation gating, standalone + full Airflow run modes.

---

### 10 · Kubernetes ML Platform

**Repo:** [mlops-k8s-platform](https://github.com/jumma786/mlops-k8s-platform)

Deploys the XGBoost prediction API as a production Kubernetes workload with horizontal autoscaling, Prometheus metrics, and a parameterised Helm chart.

| Component | Detail |
|---|---|
| Autoscaling | HPA: 2→10 pods on CPU/memory |
| Observability | Prometheus counter, histogram, gauge, latency |
| Probes | Liveness, readiness, startup on separate endpoints |
| Deployment | Rolling update — zero downtime |
| Packaging | Helm chart for environment parameterisation |

Prometheus metrics: `prediction_requests_total`, `prediction_latency_seconds`, `positive_predictions_total`, `model_auc`.

**MLOps concepts:** K8s manifests, Helm chart, HPA autoscaling, Prometheus instrumentation, rolling deployment.

---

## Technology Map

| Category | Tools |
|---|---|
| **ML frameworks** | XGBoost, LightGBM, CatBoost, scikit-learn |
| **Experiment tracking** | MLflow 3.13 (nested runs, Model Registry, artifacts) |
| **Data versioning** | DVC 3.50 |
| **Hyperparameter search** | Optuna 3.6 (TPE Bayesian sampler) |
| **Serving** | FastAPI 0.111, Pydantic, Uvicorn |
| **Containerisation** | Docker (multi-stage build) |
| **Orchestration** | Apache Airflow 2.9.1 (DAG, XCom, sensors) |
| **Kubernetes** | K8s manifests, Helm 3, HPA |
| **Observability** | Prometheus, Grafana-ready metrics |
| **Statistical tests** | SciPy (PSI, KS-test, Chi-squared, Z-test, Cohen's h) |
| **CI/CD** | GitHub Actions (push + weekly cron on every repo) |
| **Storage** | Parquet (offline feature store), JSONL (audit trail) |
| **Language** | Python 3.11+ |

---

## Datasets

| Dataset | Size | Used In |
|---|---|---|
| [UCI Bank Marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing) | 41,188 rows, 20 features | Projects 1–5, 7–9 |
| [UCI Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii) | 1,067,371 rows | Project 6 |

Both datasets are **not included** in the repo. Download instructions are in each project's README.

---

## MLOps Skills Demonstrated

| Skill | Projects |
|---|---|
| Experiment tracking & model registry | 1, 2, 4 |
| Data versioning & audit trail | 2 |
| Feature pipeline versioning | 3 |
| Bayesian hyperparameter search | 4 |
| REST API serving & Docker | 5, 8 |
| Offline + online feature store | 6 |
| Drift detection (numerical + categorical) | 7 |
| A/B testing & statistical significance | 8 |
| DAG orchestration & task dependencies | 9 |
| Kubernetes, HPA, Prometheus, Helm | 10 |
| CI/CD for ML (test → train → gate → artifact) | All |
| Leakage discipline | 1, 3, 5 |
| Champion/challenger gating | 1, 2, 4 |
| Class imbalance handling | 1, 2, 4, 5 |

---

## Quick Start

Each project is self-contained. All follow the same pattern:

```bash
git clone https://github.com/jumma786/<project-name>.git
cd <project-name>
pip install -r requirements.txt
make test       # run pytest
make run        # or: python src/<main>.py
```

See each project's `README.md` for dataset download commands, MLflow UI instructions, and Docker/K8s deployment steps.

---

## Local Layout

```
MLOps-Portfolio/
├── mlops-model-tournament/       # Project 1 — 5-model tournament
├── mlops-retraining-pipeline/    # Project 2 — DVC + scheduled retrain
├── mlops-feature-pipeline/       # Project 3 — versioned transformers
├── mlops-hyperparameter-tuning/  # Project 4 — Optuna Bayesian search
├── mlops-model-serving/          # Project 5 — FastAPI + Docker
├── mlops-feature-store/          # Project 6 — RFM Parquet store
├── mlops-model-monitoring/       # Project 7 — drift detection
├── mlops-ab-testing/             # Project 8 — A/B router + significance
├── mlops-airflow-pipeline/       # Project 9 — Airflow DAG
└── mlops-k8s-platform/           # Project 10 — Kubernetes + Prometheus
```

---

## Author

**Jumma Mohammad Teli** — Data Analyst & ML Engineer  
Birmingham, UK  
[jummamohammad477@gmail.com](mailto:jummamohammad477@gmail.com) · [LinkedIn](https://linkedin.com/in/jumma-mohammad) · [GitHub](https://github.com/jumma786)
