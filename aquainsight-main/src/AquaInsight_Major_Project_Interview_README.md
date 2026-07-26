# AquaInsight — Major Project Interview Master README

> This document is designed for interview preparation. It separates:
>
> - **Verified project details** from the uploaded repository files
> - **Your stated contribution**
> - **Metrics that require evidence**
> - **Questions an interviewer may ask**
> - **Safe, technically correct answers**

---

# 1. Project Summary

## 1.1 One-line description

**AquaInsight is an AI-powered marine environmental data management and analytics platform for researchers, students, field scientists, and CMLRE staff.**

It allows users to submit marine datasets, while CMLRE staff can review, approve, reject, manage, search, visualize, and download those datasets.

The uploaded repository confirms the following major features:

- Role-based access for users and CMLRE staff
- CSV dataset submission
- AI-powered dataset summarization
- eDNA matching assistant
- Interactive dashboard
- Firebase Authentication
- Firebase Realtime Database
- Next.js and TypeScript frontend
- Recharts-based visualization
- Google Genkit integration
- Copernicus Marine Python client as an example external integration

---

## 1.2 60-second interview answer

> “AquaInsight is an AI-powered marine environmental data platform designed for research workflows similar to CMLRE. Researchers, students, and field scientists can upload marine datasets, while CMLRE staff can review, approve, reject, archive, and manage those submissions.
>
> The main problem we addressed was that marine datasets can contain hundreds or thousands of rows, making manual review slow and difficult. AquaInsight simplifies this using AI-generated summaries, dashboard visualizations, search, filters, download options, and an eDNA matching assistant.
>
> My direct contribution was primarily in data preprocessing and CNN model experimentation. I worked on cleaning and preparing the data, applying normalization and regularization, evaluating the training-validation gap, and handing over the model workflow to the integration team. I also understood the overall system architecture and how the AI, frontend, Firebase, and data-visualization components worked together.”

---

## 1.3 Why did you choose this project?

> “We selected this project because marine research data is often large, inconsistent, and difficult to review manually. Researchers need a centralized platform where datasets can be submitted, validated, visualized, and reused. The project also gave us an opportunity to combine machine learning, generative AI, cloud services, authentication, data visualization, and full-stack development in one practical system.”

---

## 1.4 Your exact contribution

Use this answer:

> “It was a team project. My direct contribution was data preprocessing and CNN model experimentation. I worked on cleaning the input data, handling inconsistent values, preparing model-ready inputs, applying regularization techniques, monitoring training and validation performance, and handing over the model pipeline to the team for further integration.”

Do not say:

> “I built the complete platform alone.”

Say:

> “I understood the complete architecture, but my hands-on responsibility was preprocessing and CNN-related work.”

---

# 2. Complete Architecture and Workflow

## 2.1 High-level architecture

```text
Researcher / Student / Field Scientist
                |
                v
      Next.js + TypeScript UI
                |
        Firebase Authentication
                |
        Role-Based Dashboard
                |
       Dataset Upload / Search
                |
      Firebase Realtime Database
                |
    Data Parsing and Validation
                |
      AI Summarization Flow
        Google Genkit + Gemini
                |
        CMLRE Staff Review
          /              \
      Approve           Reject
         |
         v
 Recharts Dashboard and Downloads
```

Parallel AI flow:

```text
eDNA Sequence
      |
      v
Input Validation
      |
      v
Known Species Data / Reference Context
      |
      v
Genkit AI Flow
      |
      v
Potential Species + Confidence Explanation
      |
      v
Human Verification
```

---

## 2.2 End-to-end workflow

1. A new user signs up.
2. The user selects a role:
   - Researcher/User
   - CMLRE Staff
3. Firebase Authentication verifies the account.
4. A researcher uploads a CSV dataset with title and description.
5. The system validates:
   - File type
   - Required fields
   - Basic schema
   - Empty values
6. Dataset metadata is stored in Firebase Realtime Database.
7. The AI summarization flow receives:
   - Dataset description
   - Data sample
8. Google Genkit calls the generative model.
9. A concise human-readable summary is generated.
10. CMLRE staff review the dataset.
11. Staff approve or reject the submission.
12. Approved datasets appear in dashboard visualizations.
13. Users can search, filter, inspect, and download data.
14. Deleted datasets can first move to archive before permanent deletion.

---

## 2.3 Main modules

| Module | Purpose |
|---|---|
| Authentication | Login, registration, session handling |
| Role management | Separate permissions for staff and users |
| Dataset submission | Upload CSV files and metadata |
| Dataset review | Approve, reject, archive, delete |
| AI summary | Convert large dataset context into readable summary |
| eDNA assistant | Suggest possible species matches |
| Dashboard | Show trends, distributions, recent submissions |
| Search and filters | Find relevant datasets |
| Export | Download CSV or Excel |
| Notifications | Inform staff about new submissions |
| Profile management | Update name, image, settings |
| Deployment | Firebase App Hosting |

---

# 3. Technology Stack and “Why This, Not Alternatives?”

The uploaded project uses:

- Next.js 15
- React 18
- TypeScript
- Firebase
- Google Genkit
- Google AI
- Recharts
- React Hook Form
- Zod
- Tailwind CSS
- shadcn/Radix UI
- xlsx
- D3 shape utilities

## 3.1 Tech-stack justification

| Technology | Why used | Alternative | Why not alternative |
|---|---|---|---|
| Next.js | Routing, server-side logic, App Router, deployment structure | React + Vite | More separate setup needed |
| TypeScript | Type safety and maintainability | JavaScript | More runtime bugs possible |
| Firebase Auth | Fast authentication setup | Custom JWT/Auth0 | More implementation and security effort |
| Firebase Realtime Database | Real-time updates and rapid MVP development | PostgreSQL/Firestore | More backend/schema setup |
| Genkit | Structured AI workflows | Direct Gemini SDK/LangChain | Direct API becomes harder to organize as flows grow |
| Gemini | Summarization and natural-language output | OpenAI/Claude/local LLM | Google ecosystem integration was simpler |
| Recharts | React-friendly dashboard charts | Chart.js/D3 | D3 is more complex for common charts |
| Zod | Runtime validation with TypeScript | Joi/Yup/manual checks | Zod integrates naturally with TypeScript |
| React Hook Form | Efficient form handling | Formik/manual state | Less boilerplate and fewer re-renders |
| xlsx | Excel import/export | CSV-only approach | Excel is common for researchers |
| Tailwind CSS | Fast responsive styling | Plain CSS/Bootstrap | Faster custom UI development |
| Firebase App Hosting | Easy Firebase deployment | Vercel/AWS | Selected stack was already Firebase-based |

---

## 3.2 Why Firebase instead of SQL?

> “Firebase was selected because it allowed rapid development, real-time updates, authentication integration, and direct frontend connectivity. PostgreSQL would be better for complex relational queries, transactions, and large analytical workloads, but Firebase was more practical for the MVP.”

Production answer:

> “For a large production scientific platform, I would consider PostgreSQL for metadata and relationships, object storage for files, and a separate analytics layer.”

---

## 3.3 Why Next.js instead of plain React?

> “Next.js provided built-in routing, server actions, API support, structured project organization, and deployment compatibility. Plain React would require separate libraries and backend setup.”

---

## 3.4 Why TypeScript?

> “TypeScript helped catch incorrect data shapes and API mismatches during development. Since the project had forms, Firebase objects, AI responses, and dashboard data, type safety improved maintainability.”

---

## 3.5 Why Genkit?

> “Genkit helped us define AI logic as reusable server-side flows. It made prompt handling, model calls, input validation, and structured outputs more organized than directly calling the model from multiple components.”

---

# 4. Database Design

## 4.1 Logical Firebase structure

```text
users/
  userId/
    name
    email
    role
    profileImage
    createdAt

datasets/
  datasetId/
    title
    description
    fileUrl
    uploadedBy
    status
    summary
    rowCount
    createdAt
    updatedAt

reviews/
  reviewId/
    datasetId
    reviewerId
    decision
    remarks
    reviewedAt

notifications/
  notificationId/
    recipientId
    message
    datasetId
    isRead
    createdAt

archive/
  datasetId/
    deletedBy
    deletedAt
    originalData
```

---

## 4.2 Why store files separately from metadata?

> “Large CSV or Excel files should be stored in object storage, while the database should store metadata such as title, owner, file URL, status, summary, and timestamps. This keeps database operations lightweight.”

---

## 4.3 What is RBAC?

RBAC means Role-Based Access Control.

| Role | Permissions |
|---|---|
| User | Upload datasets, view status, browse approved data |
| CMLRE Staff | Review, approve, reject, archive, permanently delete |
| Admin if added | Manage users, roles, and system-wide policies |

Answer:

> “Authentication identifies the user, while authorization checks what that user is allowed to do.”

---

# 5. Dataset Processing and Preprocessing

## 5.1 What preprocessing did you perform?

Use this only if it matches your actual work:

| Problem | Action |
|---|---|
| Missing values | Removed or imputed depending on the column |
| Duplicate records | Removed duplicates |
| Inconsistent labels | Standardized category names |
| Different date formats | Converted to one standard format |
| Numeric columns stored as text | Converted to numeric types |
| Outliers | Investigated and handled using domain rules |
| Different scales | Applied normalization or standardization |
| Categorical values | Encoded into numerical form |
| Unusable columns | Removed irrelevant fields |
| Model preparation | Reshaped data and created train/validation/test splits |

Interview answer:

> “I first inspected the schema and data quality. Then I handled missing values, duplicates, inconsistent labels, type conversion, normalization, and train-validation-test preparation. The goal was to make the data consistent and model-ready.”

---

## 5.2 Why preprocessing matters

> “Machine-learning models learn patterns from the input. If the data contains duplicates, missing values, wrong types, or inconsistent labels, the model may learn incorrect patterns. Preprocessing improves reliability and reproducibility.”

---

## 5.3 Normalization vs standardization

| Normalization | Standardization |
|---|---|
| Usually scales values to 0–1 | Converts to mean 0 and standard deviation 1 |
| Common for neural networks | Common for many statistical models |
| Useful when bounded range matters | Useful when values have different distributions |

Answer:

> “We used normalization because neural networks usually train more stably when features are on a comparable scale.”

---

# 6. CNN Explanation

Important: the uploaded project files confirm the web platform and AI flows, but no CNN notebook, model file, or training logs were included in this upload. Therefore, exact CNN architecture and metrics cannot be verified from these files.

Use the following only if it matches your real CNN implementation.

## 6.1 How was CNN used?

> “The input data was first cleaned and converted into a numerical or image-like representation. The CNN then learned local patterns through convolution layers. ReLU introduced non-linearity, pooling reduced dimensionality, dropout controlled overfitting, and the final output layer generated the predicted class.”

Generic flow:

```text
Input
  |
  v
Preprocessing
  |
  v
Convolution Layer
  |
  v
ReLU
  |
  v
Pooling
  |
  v
Dropout
  |
  v
Dense Layer
  |
  v
Prediction
```

---

## 6.2 Why CNN?

> “CNN was selected because it can automatically learn local patterns and features without requiring extensive manual feature engineering. It is more parameter-efficient than a fully connected network for spatial or locally structured inputs.”

---

## 6.3 CNN alternatives

| Alternative | Benefit | Why CNN was preferred |
|---|---|---|
| Random Forest | Strong on tabular data | Requires manual feature engineering |
| SVM | Effective for small datasets | Expensive for high-dimensional inputs |
| MLP | Simple neural network | Does not preserve local spatial relationships well |
| LSTM | Good for sequential dependencies | Slower sequential processing |
| Transformer | Strong long-range modeling | More data, compute, and tuning needed |
| Transfer learning | Strong with limited image data | Larger pretrained models and more complexity |

Best answer:

> “CNN was selected because it gave a practical balance between automatic feature extraction, computational cost, and project complexity.”

---

## 6.4 Why ReLU?

> “ReLU is computationally simple and reduces the vanishing-gradient problem compared with sigmoid or tanh in hidden layers.”

---

## 6.5 Why max pooling?

> “Max pooling reduces feature-map size while retaining the strongest detected pattern. Average pooling could weaken small but important local features.”

---

## 6.6 Why dropout?

> “The model showed signs of overfitting because training performance was much better than validation performance. Dropout randomly disables some neurons during training, reducing dependency on specific neurons and improving generalization.”

---

## 6.7 Why dropout instead of L1 or L2?

| Method | Main purpose | Why used or not used |
|---|---|---|
| Dropout | Reduce co-adaptation between neurons | Directly useful for neural-network overfitting |
| L1 | Create sparse weights and feature selection | Sparsity was not the main objective |
| L2 | Penalize large weights | Valid alternative; could be compared experimentally |

Answer:

> “L1 was not prioritized because sparse feature selection was not our main objective. L2 was a valid alternative, but dropout was simpler and directly addressed overfitting in the neural network. With more experimentation, dropout and L2 could be compared or combined.”

Do not say:

> “Dropout is always better than L2.”

---

# 7. Resume Metrics — How to Justify Them

Your resume currently says:

> “Analyzed and processed 1000+ marine datasets to generate dashboard insights and support data visualization workflows.”

> “Improved CNN model performance by reducing validation gap by ~20–25% through regularization techniques and AI-driven summarization workflows, reducing manual review effort by ~40%.”

These numbers must be supported carefully.

---

## 7.1 “1000+ marine datasets”

This wording is risky.

“1000 datasets” means 1000 separate dataset files or collections.

You may actually mean:

- 1000+ rows
- 1000+ records
- 1000+ samples
- 1000+ observations
- 1000+ data points

Safer version:

> “Preprocessed and analyzed 1,000+ marine data records/samples to support dashboard insights and visualization workflows.”

Use “datasets” only when you can prove there were more than 1000 separate files.

### Evidence needed

| Evidence | Your actual value |
|---|---|
| Number of files | `________` |
| Total rows | `________` |
| Number of columns | `________` |
| Data source | `________` |
| Main features | `________` |
| Missing values before cleaning | `________` |
| Duplicates removed | `________` |

---

## 7.2 How to justify 1000+

Example:

```python
total_records = len(df)
print(total_records)
```

Multiple files:

```python
from pathlib import Path

files = list(Path("data").glob("**/*.csv"))
print("Number of files:", len(files))
```

Total rows across files:

```python
import pandas as pd
from pathlib import Path

total_rows = 0

for file in Path("data").glob("**/*.csv"):
    total_rows += len(pd.read_csv(file))

print("Total rows:", total_rows)
```

---

## 7.3 “Reduced validation gap by 20–25%”

Validation gap:

```text
Validation gap = Training accuracy - Validation accuracy
```

Example:

| Version | Training accuracy | Validation accuracy | Gap |
|---|---:|---:|---:|
| Before regularization | 94% | 76% | 18 points |
| After regularization | 91% | 77% | 14 points |

Relative gap reduction:

```text
(18 - 14) / 18 × 100
= 22.2%
```

Correct statement:

> “The training-validation accuracy gap decreased from 18 to 14 percentage points, which is a 22.2% relative reduction.”

Wrong statement:

> “Accuracy increased by 22%.”

The example values above are illustrative. Replace them with your real logs.

### Evidence needed

| Metric | Before | After |
|---|---:|---:|
| Training accuracy | `____` | `____` |
| Validation accuracy | `____` | `____` |
| Validation gap | `____` | `____` |
| Validation loss | `____` | `____` |
| Test accuracy | `____` | `____` |
| F1-score | `____` | `____` |

---

## 7.4 “Reduced manual review effort by 40%”

This requires a before-and-after timing experiment.

Example:

| Method | Average first-pass review time |
|---|---:|
| Manual review | 50 minutes |
| AI-summary-assisted review | 30 minutes |

Calculation:

```text
(50 - 30) / 50 × 100
= 40%
```

Safe statement:

> “In an internal timing comparison, AI-generated summaries reduced estimated first-pass review time from approximately 50 minutes to 30 minutes per large submission, giving an estimated 40% reduction.”

The example values above are not verified from the uploaded files. Replace them with your actual timing results.

---

## 7.5 Important correction in your resume sentence

Your current sentence mixes CNN regularization and AI summarization as if both reduced the validation gap.

That is technically confusing.

Better version:

> “Reduced the CNN training-validation gap by approximately 20–25% using regularization techniques, and reduced estimated first-pass dataset review effort by approximately 40% using AI-generated summaries.”

This clearly separates:

- CNN metric
- AI workflow metric

---

## 7.6 Recommended resume bullets

### Evidence-safe version

- Preprocessed and analyzed **1,000+ marine data records/samples**, supporting dashboard insights and visualization workflows.
- Improved CNN generalization through regularization and structured preprocessing, reducing the training-validation performance gap.
- Implemented AI-assisted dataset summaries to help reviewers understand large marine submissions more quickly.

### Metric version, only with real logs

- Reduced the CNN training-validation gap from **18 to 14 percentage points**, a **22.2% relative reduction**, through dropout and related regularization.
- Reduced average first-pass review time from **50 to 30 minutes**, an estimated **40% reduction**, using AI-generated dataset summaries.

---

# 8. AI Summarization

## 8.1 How it works

```text
CSV Upload
   |
   v
Read Description and Sample
   |
   v
Validate Input
   |
   v
Genkit Flow
   |
   v
Gemini Model
   |
   v
Human-Readable Summary
   |
   v
Staff Review
```

---

## 8.2 Why not send the entire dataset to the LLM?

- Token limits
- Higher cost
- More latency
- Privacy concerns
- Large files may be truncated
- Exact calculations may be unreliable

Better design:

> “Exact statistics should be calculated in code. The LLM should receive those statistics and a representative sample only for explanation.”

---

## 8.3 How do you prevent hallucination?

> “We ground the prompt in uploaded dataset metadata and sample values, restrict the model from inventing unsupported facts, validate generated numbers, and keep a human reviewer in the loop.”

---

## 8.4 GenAI vs template-based summary

| GenAI summary | Template summary |
|---|---|
| Natural and flexible | Deterministic |
| Adapts to different data | Limited context |
| Hallucination risk | No hallucination |
| Higher cost and latency | Cheap and fast |

Best approach:

> “Use deterministic code for facts and GenAI for explanation.”

---

# 9. eDNA Matching Assistant

## 9.1 What is eDNA?

Environmental DNA is genetic material left by organisms in water, soil, or air through:

- Skin cells
- Scales
- Mucus
- Waste
- Tissue fragments

---

## 9.2 Correct scientific explanation

> “The eDNA assistant should compare a submitted sequence against known reference sequences or a species database. The generative model should explain the result, but the core match should ideally come from a grounded sequence-matching algorithm or curated reference dataset.”

Do not say:

> “Gemini scientifically proves the species.”

Say:

> “It assists in generating possible matches that require researcher verification.”

---

# 10. External API and Copernicus

The README confirms that a Python Copernicus Marine client is included only as an example and is not currently integrated into the Next.js application.

Safe interview answer:

> “We explored Copernicus Marine as an external data source. The repository includes a Python client example, but it is not directly executed inside Next.js. For real integration, I would deploy the Python client as a FastAPI or Flask service on Cloud Run or another backend and call it from the Next.js application.”

---

# 11. APIs

## 11.1 Possible application APIs

| API | Method | Purpose |
|---|---|---|
| `/api/datasets` | POST | Submit dataset |
| `/api/datasets` | GET | List datasets |
| `/api/datasets/:id` | GET | View one dataset |
| `/api/datasets/:id/status` | PATCH | Approve or reject |
| `/api/datasets/:id/archive` | PATCH | Archive dataset |
| `/api/datasets/:id` | DELETE | Permanent deletion |
| `/api/ai/summary` | POST | Generate summary |
| `/api/ai/edna-match` | POST | Suggest eDNA matches |
| `/api/notifications` | GET | Fetch notifications |

The exact routes must be confirmed from the real source code.

---

## 11.2 Why server actions for AI?

> “Server actions keep API keys and model logic on the server. Calling Gemini directly from the browser would expose credentials and make authorization harder.”

---

# 12. Concurrency and Consistency

## 12.1 Interview question

> “Two CMLRE staff members approve or reject the same dataset at the same time. What happens?”

Problem:

- Both read `PENDING`
- One approves
- One rejects
- Last write may overwrite the first

Solution:

> “Use a Firebase transaction or version field. The update succeeds only if the status and version are unchanged.”

Example logic:

```text
Read: status=PENDING, version=3
Update request: approve only if version=3
Write: status=APPROVED, version=4

Second request still has version=3
System rejects it as a stale update
```

Answer:

> “I would use atomic transactions and optimistic concurrency. If another reviewer has already changed the record, the second action receives a conflict and reloads the latest state.”

---

## 12.2 Soft delete vs hard delete

| Soft delete | Hard delete |
|---|---|
| Record remains recoverable | Record is permanently removed |
| Supports audit and recovery | Recovery is not possible |
| Safer for accidental deletion | Useful for final cleanup/privacy |

---

# 13. Challenges and Bug Fixes

| Challenge | Cause | Solution |
|---|---|---|
| Inconsistent CSV schemas | Different researcher formats | Schema validation and mapping |
| Missing values | Incomplete field data | Imputation or removal |
| Duplicate records | Repeated uploads | Duplicate detection |
| Overfitting | Model memorized training data | Dropout, early stopping, augmentation |
| Large dataset summaries | Token limits | Sampling plus statistics |
| AI hallucinations | Generative uncertainty | Grounding and human review |
| Concurrent review actions | Multiple staff updates | Transactions/version field |
| Slow dashboard | Too much data fetched | Pagination and server-side filtering |
| Search performance | Linear scanning | Indexed fields and structured filters |
| Unauthorized actions | Weak role checks | Server-side RBAC |
| Build errors hidden | Build config ignores errors | Re-enable TypeScript and ESLint checks |

---

# 14. Deployment

The uploaded configuration confirms Firebase App Hosting with:

```yaml
runConfig:
  maxInstances: 1
```

Interview explanation:

> “The application is configured for Firebase App Hosting. The current maximum instance count is one, which is sufficient for a demo but not ideal for higher traffic. For production, autoscaling, monitoring, caching, and stronger security rules would be needed.”

---

## 14.1 Deployment flow

```text
Developer pushes code
        |
        v
Next.js build
        |
        v
Firebase App Hosting
        |
        v
Firebase Authentication
        |
        v
Realtime Database
        |
        v
Genkit server-side AI flows
```

---

## 14.2 Production improvements

- Increase autoscaling limit
- Add monitoring and error tracking
- Re-enable TypeScript build checks
- Re-enable ESLint during builds
- Add secure Firebase rules
- Add request rate limiting
- Add audit logs
- Add dataset versioning
- Add pagination
- Add database indexes
- Deploy Python services separately
- Store secrets in managed environment variables

---

# 15. Future Scope

| Future feature | Benefit |
|---|---|
| Interactive global map | Spatial exploration of marine data |
| Multilingual AI chatbot | Global researcher accessibility |
| Semantic search | Search by meaning instead of exact text |
| Copernicus live integration | Real-time ocean data |
| Dataset quality score | Prioritize problematic submissions |
| Model monitoring | Detect accuracy degradation |
| Data versioning | Scientific reproducibility |
| PostgreSQL analytics layer | Stronger relational and analytical queries |
| Audit trail | Track every approval and deletion |
| Asynchronous processing | Handle very large uploads |
| Notification service | Email or push alerts |
| Scientific reference database | More reliable eDNA matching |

---

# 16. Common Interview Questions and Answers

## Q1. Explain your project.

> “AquaInsight is an AI-powered platform for submitting, reviewing, managing, and analyzing marine environmental datasets. Researchers upload datasets, while CMLRE staff review and approve them. The platform uses Firebase for authentication and data management, Genkit and Google AI for summarization and eDNA assistance, and Recharts for visualization.”

---

## Q2. What was your role?

> “My main contribution was data preprocessing and CNN experimentation. I worked on cleaning and preparing data, regularization, evaluation, and handover to the integration team.”

---

## Q3. Explain the complete workflow.

> “A user authenticates, uploads a CSV and description, the system validates and stores the submission, Genkit generates a summary, staff review it, and approved data appears in the dashboard.”

---

## Q4. Why did you use CNN?

> “CNN automatically learns local patterns and reduces the need for manual feature engineering. It was a practical model for our input structure and available resources.”

---

## Q5. Why dropout?

> “The training-validation gap showed overfitting. Dropout reduced dependency on particular neurons and improved generalization.”

---

## Q6. Why not L1?

> “L1 is mainly useful when sparsity and feature selection are required. That was not our main objective.”

---

## Q7. Why not L2?

> “L2 was a valid option. We prioritized dropout for the initial experiments, but a larger study should compare dropout, L2, and their combination.”

---

## Q8. How did you calculate the 20–25% improvement?

> “I calculated the training-validation gap before and after regularization, then used relative gap reduction: `(old gap - new gap) / old gap × 100`.”

---

## Q9. How did you calculate the 40% effort reduction?

> “We compared average first-pass review time before and after AI summaries, then used `(old time - new time) / old time × 100`.”

---

## Q10. Why Firebase?

> “It provided authentication, real-time updates, quick frontend integration, and fast MVP development.”

---

## Q11. Why not PostgreSQL?

> “PostgreSQL is better for complex relationships and analytics, but Firebase was faster for the MVP. For production scale, PostgreSQL would be a strong option.”

---

## Q12. How do you prevent hallucination?

> “We calculate facts using code, pass only grounded context to the model, validate outputs, and retain human review.”

---

## Q13. How do you handle two users changing the same dataset?

> “Use Firebase transactions or version-based optimistic concurrency.”

---

## Q14. How do you handle large CSV files?

> “Use size validation, streaming or chunked parsing, asynchronous processing, pagination, and store only metadata in the database.”

---

## Q15. What happens if Genkit or Gemini fails?

> “Dataset submission should still succeed. The summary can be marked pending or failed and retried later. AI should not block the core workflow.”

---

## Q16. What is the biggest weakness of the current project?

> “The current repository does not include verifiable CNN training logs or model artifacts, so the exact performance claims need experiment evidence. The Copernicus client is also only an example and not integrated.”

---

## Q17. What did you learn?

> “I learned that data quality, evaluation, system integration, security, and explainability are as important as model accuracy.”

---

# 17. Trap Questions and Safe Answers

## “Show proof that you processed 1000+ datasets.”

> “I would show the source directory count or total-row calculation. If the number refers to records rather than separate files, I would correct the wording to 1,000+ records or samples.”

---

## “Show proof of the 20–25% validation-gap reduction.”

> “The claim should be supported by training-history logs or before-and-after graphs. Without that artifact, I would describe it as an experiment estimate rather than a verified metric.”

---

## “Did CMLRE officially confirm the 40% reduction?”

> “It was an internal timing comparison for first-pass review, not an organization-wide audited KPI.”

---

## “Was the CNN part of Genkit?”

> “No. CNN training and Genkit summarization are separate workflows. Genkit handled generative AI flows, while CNN was a machine-learning component.”

---

## “Did the AI summary improve CNN accuracy?”

> “No. AI summarization reduced review effort. CNN regularization reduced the validation gap. These are separate outcomes.”

---

## “Did you personally develop every module?”

> “No. It was a team project. I contributed directly to preprocessing and CNN experimentation and understood the complete architecture.”

---

# 18. Critical Resume Correction

Current wording:

> “Improved CNN model performance by reducing validation gap by ~20–25% through regularization techniques and AI-driven summarization workflows, reducing manual review effort by ~40%.”

Problem:

- It incorrectly links AI summarization with CNN validation improvement.

Better wording:

> **“Reduced the CNN training-validation gap by approximately 20–25% using regularization techniques, while AI-generated dataset summaries reduced estimated first-pass review effort by approximately 40%.”**

Better first bullet:

> **“Preprocessed and analyzed 1,000+ marine data records/samples to support dashboard insights and visualization workflows.”**

Use “datasets” only if they were truly 1,000 separate datasets.

---

# 19. Final 90-Second Answer

> “AquaInsight is an AI-powered marine environmental data platform designed for researchers and CMLRE staff. Researchers, students, and field scientists can upload CSV datasets with descriptions, while staff can review, approve, reject, search, archive, and manage those submissions.
>
> The platform uses Next.js and TypeScript for the frontend, Firebase Authentication and Realtime Database for user and data management, Recharts for visualizations, and Google Genkit with Gemini for AI-powered summaries and eDNA assistance.
>
> My direct contribution was data preprocessing and CNN experimentation. I cleaned and standardized the input data, prepared model-ready inputs, applied regularization to reduce overfitting, monitored the training-validation gap, and handed the model pipeline to the integration team.
>
> We used AI-generated summaries because manually reviewing datasets containing hundreds or thousands of rows was time-consuming. The summary flow received the dataset description and a representative sample and returned a concise explanation for staff review.
>
> A major technical lesson was to keep CNN evaluation and AI summarization as separate measurable workflows. CNN improvement should be proven through training logs, while manual-review reduction should be proven through a before-and-after timing study.”

---

# 20. Final Evidence Checklist

Fill this before the interview:

| Item | Your verified answer |
|---|---|
| 1000+ means files, rows, samples, or observations | `________________` |
| Exact data source | `________________` |
| Main dataset columns | `________________` |
| Missing values handled | `________________` |
| Duplicates removed | `________________` |
| Exact CNN input | `________________` |
| Exact CNN output | `________________` |
| CNN type | `________________` |
| Train-validation-test split | `________________` |
| Dropout rate | `________________` |
| Before training accuracy | `________________` |
| Before validation accuracy | `________________` |
| After training accuracy | `________________` |
| After validation accuracy | `________________` |
| Test accuracy | `________________` |
| Precision | `________________` |
| Recall | `________________` |
| F1-score | `________________` |
| Manual review time before AI | `________________` |
| Manual review time after AI | `________________` |
| Team size | `________________` |
| Your exact deliverables | `________________` |

---

# 21. Repository Facts Verified from Uploaded Files

- AquaInsight is described as a marine environmental dataset platform.
- It includes user and CMLRE staff roles.
- It supports CSV submissions.
- It includes AI summarization and eDNA matching flows.
- It uses Firebase Authentication and Realtime Database.
- It uses Next.js, React, TypeScript, Tailwind CSS, Recharts, React Hook Form, Zod, xlsx, and Google Genkit.
- Copernicus Marine integration is only an example and is not integrated into the application.
- Firebase App Hosting is configured with `maxInstances: 1`.
- Next.js configuration currently ignores TypeScript and ESLint build errors.

These repository facts are safe to discuss. CNN architecture, exact model metrics, and the 20–25% and 40% claims still require your real experiment evidence.
