# AquaInsight — Quick Interview Notes

## 1. Project in 30 Seconds

**AquaInsight** is a marine data analytics platform created for a **CMLRE research workflow**. It uses marine data collected from **INCOIS** and eDNA datasets. My contribution was mainly in **data collection, preprocessing, validation, standardization, and preparing structured data for AI summaries and dashboard analysis**.

> **Important:** The current repository contains Genkit-based summarization and an eDNA assistant, but it does not contain a separate embedding model implementation. In the interview, say **“prepared data for semantic analysis”** unless you can show actual embedding code.

---

# 2. My Role

> “It was a team project. My main responsibility was collecting marine data from INCOIS and eDNA files, understanding their schemas, cleaning and standardizing the records, validating important fields, and preparing structured datasets for analysis, AI-assisted summaries, and visualization. After preparing the data, I shared the processed output with the integration team.”

## My workflow

```text
INCOIS and eDNA data
        ↓
Understand columns and schema
        ↓
Check missing and duplicate values
        ↓
Correct data types and formats
        ↓
Standardize column names
        ↓
Prepare structured data
        ↓
AI summary and dashboard analysis
```

---

# 3. Resume Lines and Their Justification

## Line 1

> **Collected and processed 45,000+ marine data records from INCOIS and eDNA datasets for a CMLRE research workflow, performing data cleaning, preprocessing, and preparation for analysis.**

### How to defend it

> “The combined oceanographic dataset contained more than 45,000 rows. I worked on collecting, checking, cleaning, and organizing those records before they were used for analysis.”

### What preprocessing means here

- Checked missing values
- Checked duplicate records
- Standardized column names
- Converted incorrect data types
- Made numerical and date formats consistent
- Selected useful fields for analysis

### Metric proof

```text
Total records = Number of rows after combining the source files
```

Be ready to answer:

- Data source: INCOIS and eDNA files
- Main parameters: latitude, longitude, temperature, salinity, and eDNA-related fields
- Exact record count: keep the actual file/row count ready

---

## Line 2

> **Prepared structured marine datasets for AI-assisted summarization and semantic analysis, reducing estimated initial review effort by ~40% during internal testing.**

### How to defend it

> “Large files were difficult to understand row by row. I prepared clean data, useful metadata, and representative samples so the AI summary could provide reviewers with a quick overview.”

### How to justify 40%

Use it only as an **estimated internal result**.

Example:

| Review method | Time |
|---|---:|
| Manual first review | 25 minutes |
| Summary-assisted review | 15 minutes |

```text
(25 − 15) ÷ 25 × 100 = 40%
```

Say:

> “It was an internal estimate for first-pass review time, not a formally audited CMLRE metric.”

### Embeddings caution

The uploaded code does not show an embedding implementation. Use this safer wording:

> **Prepared structured marine data for AI-assisted summarization and future semantic analysis.**

Only keep “using embeddings” if you can explain:

- What data was embedded
- Which embedding model was used
- Where vectors were stored
- How similarity was calculated

---

## Line 3

> **Cleaned and standardized marine data to improve analysis and visualization workflows.**

### How to defend it

> “I made the data consistent so charts and filters could work without errors caused by different column names, missing values, or incorrect formats.”

---

# 4. Tech Stack Used and Why

| Technology | Why it was used | Your level of explanation |
|---|---|---|
| Python | Data collection, cleaning, and preprocessing | Explain confidently |
| Firebase | Authentication and application data storage | Basic explanation |
| Google Genkit | Organizing AI summary and eDNA flows | Basic explanation |
| Gemini/Google AI | Generating dataset summaries | Basic explanation |
| Next.js/TypeScript | Application interface and server-side actions | Say team-level understanding |
| Recharts | Dashboard visualizations | Basic explanation |

## Why Python?

> “Python was suitable because it has simple libraries for reading, cleaning, validating, and transforming CSV and Excel data.”

### Alternatives

- Excel/Power Query
- R
- Java

### Why not alternatives?

> “Excel is useful for manual inspection but less suitable for repeatable processing. Python made the workflow reusable and easier to automate.”

---

## Why Firebase?

> “Firebase was selected because it provides authentication, real-time updates, and quick application setup.”

### Alternatives

- PostgreSQL
- MySQL
- MongoDB

### Why not alternatives?

> “For the initial project, Firebase required less backend setup. PostgreSQL would be a better future option for complex analytical queries and larger structured data.”

---

## Why Genkit?

> “Genkit organized the prompt, input validation, model call, and structured output as a reusable AI flow.”

### Alternatives

- Direct Gemini API
- LangChain
- Custom backend flow

### Why not alternatives?

> “The summarization workflow was simple, so Genkit was sufficient. LangChain would be more useful for complex retrieval or multi-step AI workflows.”

---

# 5. Challenges and Solutions

| Challenge | What I did |
|---|---|
| Different file formats | Converted data into a common structure |
| Inconsistent column names | Standardized the column names |
| Missing or incorrect values | Validated and handled them based on the field |
| Large number of rows | Prepared representative samples and summaries |
| Different data types | Converted fields to the correct numeric/text/date type |
| Data suitable for charts | Selected and structured required parameters |
| AI may generate unsupported details | Kept human review and used dataset samples as context |

### Best challenge answer

> “The main challenge was that the source files had different structures and formats. I first identified common fields, standardized the column names and data types, and prepared one consistent structure for analysis.”

---

# 6. Concurrency Scenario

## Question

> “What if two staff members update the same dataset at the same time?”

## Answer

> “I would use a Firebase transaction or a version/status check. The update should succeed only if the dataset still has the expected status. If another reviewer has already changed it, the second user should receive a conflict message and the latest record should be loaded.”

Example:

```text
Reviewer A reads: PENDING, version 2
Reviewer B reads: PENDING, version 2

Reviewer A approves:
APPROVED, version 3

Reviewer B tries to reject using version 2:
Update rejected because the record is outdated
```

---

# 7. Alternatives as Future Scope

Use alternatives as future improvements instead of saying the current technology was wrong.

## Database

> “Firebase was sufficient for the prototype. In future, I would evaluate PostgreSQL for complex relationships, reporting, and larger structured datasets.”

## Search

> “The current search can be improved by comparing keyword search, TF-IDF, and embedding-based semantic search.”

## AI workflow

> “The current Genkit flow is simple. In future, I would compare direct Gemini calls and LangChain for retrieval-based workflows.”

## Data pipeline

> “In future, preprocessing can be automated using scheduled validation pipelines instead of running it manually for every new file.”

## Visualization

> “The dashboard can be extended with an interactive GIS map for location-based marine analysis.”

## eDNA

> “The current eDNA assistant is an AI prototype. In future, I would ground it using a curated species database and a real sequence-matching method.”

---

# 8. Common Interview Questions

## Explain your project.

> “AquaInsight is a marine data analytics platform for CMLRE research workflows. Researchers upload marine data, and staff can review and analyze it. My role was collecting INCOIS and eDNA data, cleaning and standardizing it, and preparing it for AI summaries and visualization.”

## Why did you choose this project?

> “Marine datasets are large and often have different formats. The project aimed to make them easier to organize, review, and analyze.”

## What exactly did you do?

> “I mainly handled data collection, schema understanding, cleaning, standardization, validation, and structured data preparation.”

## Why was preprocessing needed?

> “Without preprocessing, inconsistent formats and missing values can cause incorrect analysis and chart errors.”

## Why AI summary?

> “It helps reviewers understand a large file without reading every row during the first review.”

## Did you develop the whole project?

> “No. It was a team project. My direct contribution was the data-preparation side, while I understood the complete workflow.”

## Did embeddings reduce review effort?

> “The AI summary reduced estimated first-pass review effort. Embeddings, if used, support semantic representation; they should not be presented as the reason for the 40% result without separate testing.”

## Was the 40% result officially audited?

> “No. It was an internal timing estimate for initial review.”

---

# 9. Recommended Resume Version

## Safer version

**AquaInsight — AI Data Analytics Platform**  
*(Python, Firebase, Google Genkit)*

- Collected and processed **45,000+ marine data records** from INCOIS and eDNA datasets for a CMLRE research workflow, performing data cleaning and preparation for analysis.
- Prepared structured marine datasets for **AI-assisted summarization**, reducing estimated first-pass review effort by **~40%** during internal testing.
- Cleaned and standardized marine data to support analysis and visualization workflows.

## Version with semantic analysis

Use this only if you can explain embeddings:

- Prepared structured marine datasets for AI-assisted summarization and **embedding-based semantic analysis**, reducing estimated first-pass review effort by **~40%** during internal testing.

---

# 10. Final 60-Second Answer

> “AquaInsight is a marine data analytics platform designed for a CMLRE research workflow. My contribution was mainly related to the data. I collected oceanographic data from INCOIS and worked with eDNA files containing more than 45,000 combined records. I studied the schemas, checked missing and duplicate values, standardized column names and formats, and prepared the datasets for analysis and visualization.
>
> I also prepared structured samples and metadata for the AI summary workflow. This allowed reviewers to understand large submissions more quickly. During internal testing, we estimated around a 40% reduction in first-pass review effort. The project used Python for data preparation, Firebase for application data and authentication, and Google Genkit for the AI summary flow.”
