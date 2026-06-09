# MLOps Portfolio Series

![Python](https://img.shields.io/badge/Python-3.11%2B-blue)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

> **10 production-style ML projects** — from model selection through serving, monitoring, orchestration, and Kubernetes deployment.  
> Built by **Jumma Mohammad Teli** around real datasets (UCI Bank Marketing, Online Retail II) with CI/CD on every repo.

---

## Portfolio Overview

| # | Project | Key Tech | Repo |
|---|---|---|---|
| 1 | Multi-Model Tournament | MLflow, XGBoost, LightGBM, CatBoost | [mlops-model-tournament](https://github.com/jumma786/mlops-model-tournament) |
| 2 | Scheduled Retraining | DVC, MLflow, champion gate | [mlops-retraining-pipeline](https://github.com/jumma786/mlops-retraining-pipeline) |
| 3 | Feature Engineering | sklearn pipelines, MLflow artifacts | [mlops-feature-pipeline](https://github.com/jumma786/mlops-feature-pipeline) |
| 4 | Hyperparameter Tuning | Optuna, MLflow, Bayesian search | [mlops-hyperparameter-tuning](https://github.com/jumma786/mlops-hyperparameter-tuning) |
| 5 | Model Serving | FastAPI, Docker, Cloud Run | [mlops-model-serving](https://github.com/jumma786/mlops-model-serving) |
| 6 | Feature Store | Parquet offline store, RFM features | [mlops-feature-store](https://github.com/jumma786/mlops-feature-store) |
| 7 | Model Monitoring | PSI, KS-test, chi-squared drift | [mlops-model-monitoring](https://github.com/jumma786/mlops-model-monitoring) |
| 8 | A/B Testing | Z-test, Cohen's h, FastAPI router | [mlops-ab-testing](https://github.com/jumma786/mlops-ab-testing) |
| 9 | Airflow Pipeline | DAG, XCom, validation gate | [mlops-airflow-pipeline](https://github.com/jumma786/mlops-airflow-pipeline) |
| 10 | Kubernetes Platform | K8s, Helm, Prometheus, HPA | [mlops-k8s-platform](https://github.com/jumma786/mlops-k8s-platform) |

**Status:** All 10 projects complete.

---

## Pipeline Flow

```
Tournament → Retraining → Features → Tuning → Serving
                                              ↓
                    Feature Store → Monitoring → A/B Testing
                                              ↓
                              Airflow → Kubernetes
```

**Champion model:** XGBoost on UCI Bank Marketing (~0.81 AUC, 19 features, duration excluded for leakage).

---

## Local Layout

Each project is an independent git repository:

```
MLOps-Portfolio/
├── mlops-model-tournament/
├── mlops-retraining-pipeline/
├── mlops-feature-pipeline/
├── mlops-hyperparameter-tuning/
├── mlops-model-serving/
├── mlops-feature-store/
├── mlops-model-monitoring/
├── mlops-ab-testing/
├── mlops-airflow-pipeline/
└── mlops-k8s-platform/
```

Clone individual repos from GitHub, or work from this monorepo-style folder locally.

---

## Quick Start (any project)

```bash
cd mlops-model-serving   # or any project folder
pip install -r requirements.txt
make test
```

See each project's `README.md` for train, serve, and deploy commands.

---

## Author

**Jumma Mohammad Teli** — Data Analyst & ML Engineer  
Birmingham, UK  
[jummamohammad477@gmail.com](mailto:jummamohammad477@gmail.com) · [LinkedIn](https://linkedin.com/in/jumma-mohammad) · [GitHub](https://github.com/jumma786)
