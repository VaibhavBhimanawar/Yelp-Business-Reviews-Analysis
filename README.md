# Yelp-Business-Reviews-Analysis
Link to downlaod the dataset: https://business.yelp.com/data/resources/open-dataset/
Project Flow
Yelp JSON Dataset (5GB)
        ↓
  Python: split into 10 smaller files
        ↓
  Upload to AWS S3
        ↓
  COPY INTO Snowflake (raw variant tables)
        ↓
  SQL transformation → structured tables
        ↓
  Sentiment UDF applied to review text
        ↓
  SQL queries to answer business questions
