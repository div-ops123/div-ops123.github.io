---
layout: page
title: Personalized Marketplace Discovery
description: 3-stage personalized recommendations (retrieval → ranking → filtering) plus semantic "Similar Items" for marketplace product discovery
img: assets/img/5.jpg
importance: 1
category: work
---

**Problem:** Product discovery breaks down when a marketplace catalogue is large. Users miss items they'd buy; generic "popular items" lists don't personalize.

**Two discovery surfaces:**

1. **"Recommended for You" (homepage)** — personalized recommendations using a 3-stage pipeline:
   - *Retrieval*: candidate generation from a large catalogue (fast, approximate)
   - *Ranking*: a learned model scores candidates against the user's history
   - *Filtering*: business rules applied last (out-of-stock removal, diversity constraints, promotion slots)

2. **"Similar Items" (product page)** — semantic similarity using PyTorch embeddings, so recommendations reflect actual product meaning, not just co-purchase history.

**Why 3 stages?** Applying a heavy ranking model to the full catalogue is computationally infeasible. The retrieval stage narrows thousands of items to hundreds; the ranker scores those accurately; filtering applies non-ML business constraints without polluting model training.

**Stack:** Python · PyTorch · Prefect · MLflow · DVC · Docker · scikit-learn

[View on GitHub](https://github.com/div-ops123/ecommerce-recommendation-system)
