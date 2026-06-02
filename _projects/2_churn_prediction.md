---
layout: page
title: KKBOX Churn Prediction System
description: Business-aware subscription churn prediction with a shared feature store and 14-day intervention window
img: assets/img/3.jpg
importance: 2
category: work
---

**Problem:** KKBOX (music streaming) subscription labels are only available after a 1-month delay — a label engineering problem that breaks naive pipelines. The business also needs predictions early enough to actually intervene.

**Key design decisions:**

- **Label engineering for delayed feedback** — built a labeling pipeline that correctly derives churn labels for month M−1, accounting for the 1-month reporting lag. Without this, a model would be trained on future-leaking or mislabeled targets.
- **14-day prediction horizon** — the scoring pipeline is designed to flag at-risk subscribers 14 days before their subscription expires, giving the retention team a concrete intervention window.
- **Shared feature engineering module** — training and serving use the same feature transformation code, eliminating training-serving skew. This is a common silent failure mode in churn systems.
- **Full pipeline orchestration with Prefect** — training, serving, monitoring, and labeling pipelines are all Prefect flows, making the system auditable and re-runnable.

**Stack:** Python · Prefect · MLflow · DVC · Docker · scikit-learn

[View on GitHub](https://github.com/div-ops123/kkbox-churn-prediction-system)
