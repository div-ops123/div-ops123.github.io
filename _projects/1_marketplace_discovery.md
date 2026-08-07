---
layout: page
title: Personalized Marketplace Discovery
description: A two-stage (retrieval → ranking) recommendation engine powering personalized "Similar Items" recommendations on marketplace product pages
img: assets/img/5.jpg
importance: 1
category: work
---

**Problem:** Product discovery breaks down when a marketplace catalogue is large. Users miss items they'd buy; generic "popular items" lists don't personalize.

**How it works** — "Similar Items" recommendations on the product page, powered by a two-stage pipeline:

- **Retrieval**: given the item a shopper is viewing, a Siamese sentence-embedding encoder (PyTorch) generates an embedding, and a FAISS index returns its nearest neighbors — items that are semantically similar, not just frequently co-purchased.

- **Ranking**: a LightGBM model re-scores those candidates using item and user features, ordering them by purchase likelihood personalized to that shopper.

**Why two stages?** Running a heavy ranking model over the full catalogue is computationally infeasible. Retrieval narrows thousands of items down to a couple hundred candidates cheaply; ranking then applies a more expensive, more accurate model to just that shortlist.

**Stack:** Python · PyTorch · LightGBM · FAISS · Apache Airflow · MLflow · FastAPI · Docker

[View on GitHub](https://github.com/div-ops123/Personalized-Marketplace-Discovery)
