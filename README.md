# Yelp Business Reviews Analysis

Dataset: https://business.yelp.com/data/resources/open-dataset/

## Pipeline
```
Yelp JSON (5GB) → split into 10 files → AWS S3 → Snowflake (COPY INTO)
→ SQL transformation → Sentiment UDF → Business SQL queries
→ ML: Star Rating Prediction
```

## ML Extension: Star Rating Prediction

Predicted review star ratings (1–5) from review text + metadata using TF-IDF (5,000 features) and engineered features (sentiment polarity, word count, exclamation count). Trained on ~200K stratified-sampled reviews.

**Results:**
| Model | Weighted F1 |
|---|---|
| Logistic Regression | 0.55 |
| Random Forest | 0.51 |
| **XGBoost (best)** | **0.56** |

**Key findings:**
- Errors mostly confused *adjacent* ratings (3★↔2★/4★); extreme misclassifications (1★↔5★) were rare (<3%) — model reliably captures sentiment direction.
- `sentiment_polarity` was the top predictive feature, validating the original NLP pipeline.
- Used prediction gaps to flag businesses for review; top-flagged case showed mixed-but-positive reviews (specific complaints + high overall satisfaction) rather than manipulation — a useful finding on the limits of text-only sentiment scoring.

**Stack:** Python · scikit-learn · XGBoost · TF-IDF · Pandas
