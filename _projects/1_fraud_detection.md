---
layout: page
title: Real-Time Fraud Detection System
description: Sub-100ms fraud risk scoring with async prediction logging via Redis Stream and horizontal scaling
img: assets/img/1.jpg
importance: 1
category: work
---

**Problem:** Credit card fraud requires real-time decisions — batch scoring is too slow. But logging predictions to a database on the hot serving path adds latency that compounds under load.

**Key design decisions:**

- **Async prediction logging via Redis Stream** — the serving path returns a fraud score immediately; the DB write is decoupled to a background consumer. This prevents database write latency from appearing in the user-facing response time.
- **Horizontally scalable serving layer** — the scoring service is stateless and containerized (Docker), so it can scale out to handle traffic spikes without architectural changes.
- **End-to-end MLOps** — experiments tracked in MLflow, data versioned with DVC, pipelines orchestrated with Prefect.

**Stack:** Python · FastAPI · Redis · Docker · MLflow · DVC · Prefect · scikit-learn

[View on GitHub](https://github.com/div-ops123/real-time-fraud-detection-system)
