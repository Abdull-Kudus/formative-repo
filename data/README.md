# Data Directory

This directory stores the datasets required for the project notebooks.

## Required Datasets

| File | Part | Source | Description |
|---|---|---|---|
| `GaltonFamilies.csv` | Part 1 (EM Algorithm) | [Kaggle: Galton Height Data](https://www.kaggle.com/datasets/jacopoferretti/parents-heights-vs-children-heights-galton-data) | 934 children, 205 families; heights in inches. |
| `IMDB_Dataset.csv.gz` | Part 2 (Bayesian Sentiment) | [Kaggle: IMDb 50K Movie Reviews](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews) | 50,000 labeled reviews (25k positive, 25k negative). Stored gzip-compressed (`.csv.gz`) to stay within GitHub file size limits. |

> **Note:**
> If you have the uncompressed `IMDB Dataset.csv` (approx. 66 MB), compress it using gzip before committing:
> ```bash
> gzip -c "IMDB Dataset.csv" > IMDB_Dataset.csv.gz
> ```
