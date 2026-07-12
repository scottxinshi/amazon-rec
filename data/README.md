# Data — Amazon Reviews 2023 (Movies & TV)

## Download

No login or approval required. Download both files directly:

**Reviews (interactions):**
https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/review_categories/Movies_and_TV.jsonl.gz

**Metadata (product names, prices, etc.):**
https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/meta_categories/meta_Movies_and_TV.jsonl.gz

Place both `.jsonl.gz` files in this `data/` folder.
Spark reads `.gz` files natively — no need to decompress.

## Stats

| | |
|---|---|
| Users | 6.5M |
| Products | 747.8K |
| Ratings | 17.3M |
| Timespan | May 1996 – Sep 2023 |
| Rating scale | 1.0 – 5.0 stars |

## Key Fields (Reviews)

| Field | Type | Description |
|---|---|---|
| `user_id` | str | Reviewer ID |
| `parent_asin` | str | Product ID (use this, not `asin`) |
| `rating` | float | Star rating 1.0–5.0 |
| `timestamp` | int | Unix timestamp (ms) |
| `title` | str | Review title |
| `text` | str | Review body |
| `verified_purchase` | bool | Verified purchase flag |

## Key Fields (Metadata)

| Field | Type | Description |
|---|---|---|
| `parent_asin` | str | Product ID |
| `title` | str | Movie/show name |
| `average_rating` | float | Overall rating on Amazon |
| `price` | float | Price in USD |
| `main_category` | str | Category |

## Citation

```
@article{hou2024bridging,
  title={Bridging Language and Items for Retrieval and Recommendation},
  author={Hou, Yupeng and Li, Jiacheng and He, Zhankui and Yan, An and Chen, Xiusi and McAuley, Julian},
  journal={arXiv preprint arXiv:2403.03952},
  year={2024}
}
```
