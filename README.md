# Amazon Movies & TV — PySpark Recommendation System

Collaborative filtering recommendation system built with PySpark ALS on the [Amazon Reviews 2023](https://amazon-reviews-2023.github.io/) dataset (Movies & TV category).

## Dataset

- 17.3M ratings · 6.5M users · 747K products
- After 5-core filtering: 667K users · 200K products · 7.5M interactions
- Matrix sparsity: 99.99%

Download the data files and place them in `data/`:
- `reviews_part*.jsonl` — split from `Movies_and_TV.jsonl` (>5GB, split into 5 parts)
- `meta_Movies_and_TV.jsonl` — product metadata

## Notebooks

| Notebook | Description |
|---|---|
| `01_eda_pyspark.ipynb` | Exploratory data analysis — rating distribution, activity distribution, reviews over time, 5-core filtering, matrix sparsity |
| `02_als_pyspark.ipynb` | ALS model training — dense_rank indexing, train/test split, similar movies (cosine similarity), user recommendations |
| `03_evaluation_pyspark.ipynb` | Model evaluation — RMSE/MAE vs baselines, Precision@K / Recall@K, effect of ALS rank on RMSE |

## Key Results

| Model | RMSE | MAE |
|---|---|---|
| Global Mean | 1.1913 | 0.9373 |
| Popularity | 1.0726 | 0.7841 |
| ALS (rank=50) | 1.1266 | 0.8729 |

Rank sweep shows rank=50 is the sweet spot — beyond that, compute cost grows faster than accuracy improves.

## Key Findings

- Collaborative filtering learns **user behavior overlap**, not content similarity — "similar to Inception" can return an Algebra tutor DVD if the same users reviewed both
- Popularity baseline is hard to beat due to severe rating bias (users only rate what they love)
- 80%+ of users have fewer than 5 reviews — cold start is a major real-world challenge

## Setup

```bash
pip install pyspark pandas matplotlib seaborn
```

Run on **Databricks** (recommended) or locally with Java 11+:

```python
# Local mode — add to first cell
import os
os.environ["JAVA_HOME"] = r"C:\path\to\jdk"
os.environ["HADOOP_HOME"] = r"C:\hadoop"

from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .master("local[*]") \
    .config("spark.driver.memory", "16g") \
    .config("spark.driver.host", "127.0.0.1") \
    .config("spark.driver.bindAddress", "127.0.0.1") \
    .getOrCreate()
```

## Tech Stack

- PySpark 3.5 · Databricks Serverless
- ALS (Alternating Least Squares) · dense_rank() indexing
- Matplotlib · Seaborn · Pandas
