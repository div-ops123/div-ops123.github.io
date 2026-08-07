---
layout: page
title: KKBox Churn Prediction System
description: Subscription churn prediction that scores 14 days ahead and retrains itself automatically when performance degrades
img: assets/img/3.jpg
importance: 2
category: work
---

**Problem:** KKBox (music streaming) subscription churn labels aren't knowable until roughly a month after a subscription expires — you need a 30-day renewal window to see whether someone actually came back. Naively, that delay tempts a pipeline into leaking future information into training data. On top of that, the business needs predictions early enough to actually act, not just accurate ones.

**Key design decisions:**

- **Label engineering for delayed feedback** — a dedicated monthly labeling pipeline derives churn labels for month M−1 by checking each subscriber's transaction history for a valid renewal within 30 days of expiry, rather than reading a label off a single point-in-time snapshot. Getting this wrong is the easiest way to train on future-leaking or mislabeled targets.
- **14-day prediction horizon** — the serving pipeline scores subscribers exactly 14 days before their subscription expires, sized specifically to leave the retention team a real window to intervene, not just a number to report after the fact.
- **Shared feature module, not a feature store** — training, serving, and monitoring all call the same feature-transformation function, which enforces the point-in-time feature cutoff internally rather than trusting each caller to pass it correctly. Deliberately not a feature store (Feast/Tecton-style) — at this scale a shared module gives the same train/serve consistency guarantee for a fraction of the operational overhead, closing the most common silent failure mode in churn systems: training-serving skew.
- **A closed monitoring loop, not a one-time model** — every serving run chains a PSI-based drift check, anchored to the training distribution, directly onto itself, and a separate monthly performance track automatically triggers a full retrain-and-validate pipeline if AUC-PR drops below threshold. The system catches its own degradation without anyone watching a dashboard.
- **Seven decoupled Prefect pipelines** — labeling, dataset-build, training, validation, retraining, serving, and monitoring are each independently invocable flows, not stages of one monolithic script. Training never decides its own promotion, for example — a separate validation pipeline scores candidate vs. production on a held-out fold neither ever touched during fitting.

**Stack:** Python · Prefect · DuckDB · PostgreSQL · LightGBM · MLflow · FastAPI · Docker

[View on GitHub](https://github.com/div-ops123/kkbox-churn-prediction-system)
