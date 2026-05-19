# Fintech Review Analytics

Customer Experience Analytics for Ethiopian Fintech Apps

## Project Overview

This project analyzes customer reviews from Google Play Store mobile banking applications of major Ethiopian banks:

- Commercial Bank of Ethiopia (CBE)
- Bank of Abyssinia (BOA)
- Dashen Bank

The objective is to transform raw user reviews into actionable business insights using:

- Web scraping
- Natural Language Processing (NLP)
- Sentiment analysis
- Thematic analysis
- PostgreSQL database engineering
- Data visualization

The project helps identify:

- Common customer complaints
- Requested features
- Sentiment trends
- Product quality issues
- Areas for customer experience improvement

---

# Business Problem

Mobile banking adoption in Ethiopia is rapidly increasing. Thousands of users leave feedback on Google Play Store regarding:

- App crashes
- Login issues
- OTP problems
- Slow transfers
- UI/UX concerns
- Feature requests

This project builds a complete analytics pipeline to help banks understand customer pain points and improve their digital banking experience.

---

# Banks Analyzed

| Bank | App ID |
|---|---|
| Commercial Bank of Ethiopia | `com.combanketh.mobilebanking` |
| Bank of Abyssinia | `com.boa.boaMobileBanking` |
| Dashen Bank | `com.dashen.dashensmart` |

---

# Project Structure

```text
fintech-review-analytics/

├── data/
│   └── raw/
│
├── notebooks/
│
├── scripts/
│
├── src/
│
├── tests/
│
├── requirements.txt
└── README.md
```

---

# Features

- Google Play Store review scraping
- Data cleaning and preprocessing
- Sentiment classification
- Keyword and theme extraction
- Complaint clustering
- PostgreSQL database integration
- Visual analytics dashboard
- Unit testing pipeline

---

# Technologies Used

## Programming Language

- Python 3.11+

## Libraries

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- nltk
- spacy
- transformers
- google-play-scraper
- sqlalchemy
- psycopg2
- pytest

## Database

- PostgreSQL
 Overview

This project uses PostgreSQL to store cleaned and processed fintech review data in a structured relational format.

Database Schema

The database consists of two tables:

🏦 Banks Table

Stores metadata about Ethiopian banks.

CREATE TABLE banks (
    bank_id SERIAL PRIMARY KEY,
    bank_name VARCHAR(100) UNIQUE NOT NULL,
    app_name VARCHAR(100)
);


📝 Reviews Table

Stores processed customer reviews with NLP outputs.

CREATE TABLE reviews (
    review_id SERIAL PRIMARY KEY,
    bank_id INTEGER REFERENCES banks(bank_id),

    review_text TEXT NOT NULL,
    rating INTEGER,
    review_date DATE,

    sentiment_label VARCHAR(20),
    sentiment_score FLOAT,

    identified_theme VARCHAR(100),

    source VARCHAR(100)
);

📄 Schema File
The full schema is stored in:
schema.sql
This file allows the database to be recreated easily.

⚙️ How to Set Up Database
1. Create Database
CREATE DATABASE bank_reviews;
2. Run Schema File
psql -U postgres -d bank_reviews -f schema.sql
3. Verify Tables
\dt
Expected output:

banks
reviews


---

# Installation

## 1. Clone Repository

```bash
git clone https://github.com/Redeat-Birhane/fintech-review-analytics.git
```

## 2. Navigate Into Project

```bash
cd fintech-review-analytics
```

## 3. Create Virtual Environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

---

# Install Dependencies

```bash
pip install -r requirements.txt
```

---

# How the Project Works

## Step 1 — Scrape Reviews

Reviews are collected from Google Play Store using:

- App ratings
- Review text
- Review dates
- Bank names

The scraped data is stored inside:

```text
data/raw/
```

---

## Step 2 — Clean & Preprocess Data

The preprocessing pipeline:

- removes duplicates
- handles missing values
- normalizes text
- removes stopwords
- tokenizes reviews

---

## Step 3 — Sentiment Analysis

Reviews are classified into:

- Positive
- Neutral
- Negative

using NLP sentiment models.

---

## Step 4 — Theme Extraction

Key customer concerns and feature requests are extracted using:

- TF-IDF
- keyword extraction
- clustering techniques

Examples:

- login issues
- OTP failures
- transfer delays
- fingerprint login requests

---

## Step 5 — Database Storage

Processed reviews are stored in PostgreSQL for structured querying and analytics.

---

## Step 6 — Visualization & Insights

The final stage produces:

- sentiment charts
- complaint trends
- feature request summaries
- bank comparisons
- actionable recommendations

---

# Example Business Questions

- Which bank receives the most negative reviews?
- Are transfer delays a systemic issue?
- Which features do customers request most?
- What complaints occur repeatedly?
- Which app has the best customer sentiment?

---

# Testing

Run unit tests using:

```bash
pytest
```

---

# Future Improvements

- Real-time review monitoring
- Dashboard deployment
- AI-powered chatbot integration
- Advanced transformer-based sentiment models
- Automated reporting pipeline

