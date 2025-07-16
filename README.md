
# 🏥 Pulse Check - Healthcare AI News Sentiment Analysis using Microsoft Fabric

> An end-to-end data engineering project using Microsoft Fabric that analyzes public sentiment on healthcare-related AI news articles — from ingestion to insights.

---

## 📌 Architecture

![Architecture](https://github.com/GopalSinghRajput/Pulse-Check---A-Microsoft-Fabric-Data-engineering-project/blob/1ca71a2fc2443cd43006b4f5e01f5f63d0b711c5/file_2025-07-16_16.49.57.png)

**Tools Used:**
- SerpApi (REST API)
- Microsoft Fabric (Pipeline, Lakehouse, Notebooks)
- Synapse + PySpark
- VADER Sentiment Analysis
- Power BI Online

---

## 🛠 Workflow — End-to-End Pipeline in Microsoft Fabric

This project implements a complete pipeline to extract, process, and analyze sentiment in healthcare AI news articles using Microsoft Fabric.

---

### 🔄 Step-by-Step Pipeline

#### 1. 🔍 **Data Ingestion — News from SerpApi**
- **Tool**: SerpApi (REST API)
- **Action**: Search queries like `Healthcare AI`, `AI in hospitals`, etc. fetch news results in JSON format.
- **Data**: Titles, snippets, links, sources, etc.

#### 2. 📥 **Landing Zone — JSON to Lakehouse**
- **Tool**: Microsoft Fabric Data Pipeline
- **Action**: Raw JSON is loaded into a Lakehouse as a structured Delta table.

#### 3. 🧹 **Data Transformation — PySpark Notebook**
- **Tool**: Synapse Notebook (Fabric)
- **Action**:
  - Clean and normalize article metadata
  - Extract relevant fields like `title`, `snippet`, `source`
  - Drop nulls and prepare for NLP

#### 4. 🧠 **Sentiment Analysis — VADER (NLTK)**
- **Logic**:
  - Calculate `compound_score` from snippets
  - Classify each article into:
    - 😊 Positive
    - 😡 Negative
    - 😐 Neutral
    - 😌 Mixed

#### 5. ♻️ **Incremental Loading — Type 1 SCD Merge**
- **Tool**: PySpark SQL with `MERGE`
- **Logic**:
  - If `link` exists and content differs → update
  - Else → insert
- **Result**: Final table `serpapi_sentiment_scored` with no duplicates

#### 6. 📊 **Visualization — Power BI Online**
- **Report Elements**:
  - Emoji-based sentiment cards
  - Histogram of compound scores
  - Source-wise sentiment distribution
  - Interactive table with search filter

#### 7. ⚡ **Optional Trigger — Data Activator + Teams**
- **Action**: Sends alert when positive sentiment exceeds a threshold.

---

### ✅ Visual Summary

```text
SerpApi → Data Pipeline → Lakehouse → Notebook (ETL + VADER)
→ Type 1 SCD Merge → Final Table → Power BI → (Optional Alert)
```

---

## 📊 Power BI Dashboard

![Dashboard](assets/dashboard.png)

### Features:
- % Sentiment Cards (Positive, Negative, Neutral, Mixed)
- Histogram of Compound Scores
- Source vs. Sentiment Chart
- Searchable Article Viewer

---

## 🧪 Tools & Technologies

| Category         | Tool                                |
|------------------|-------------------------------------|
| Ingestion        | SerpApi REST API                    |
| Storage          | Microsoft Fabric Lakehouse          |
| Transformation   | Synapse Notebook (PySpark)          |
| Sentiment Engine | NLTK VADER                          |
| Incremental Load | Type 1 SCD using `MERGE` in SQL     |
| Visualization    | Power BI Online                     |
| Alerting         | Microsoft Data Activator + Teams    |

---

## 🧾 Folder Structure

```
📂 Healthcare-AI-Sentiment
│
├── 📸 assets/
│   ├── architecture-diagram.png
│   ├── dashboard.png
│
├── 📓 notebooks/
│   └── sentiment_pipeline.ipynb
│
├── 📈 powerbi/
│   └── report.pbix
│
└── README.md
```

---

## ✍️ Author

**Gopal Singh**  
BTech CSE (AI/ML), VIT  
LinkedIn: [linkedin.com/in/your-profile](#)

---

## 📜 License

MIT License © 2025 Gopal Singh
