# AquaInsight — Master Interview Prep (Quick Read)

> First-person, defend-yourself version. Short on purpose — scan this once before the interview.

---

## 1. Explain your project / Why this project?

"AquaInsight is an AI-powered marine data platform I built for research workflows similar to CMLRE. Researchers and field scientists upload marine datasets (CSV), and CMLRE staff review, approve, or reject them. I chose it because marine research data — INCOIS feeds, eDNA survey data — is large, messy, and fragmented across sources, and manual review doesn't scale. I wanted a project that combined data preprocessing, embeddings/AI, and a real full-stack app instead of just a model in a notebook."

**Why not something simpler?** "I wanted end-to-end ownership — data cleaning, semantic search via embeddings, AI summarization, and a working product with auth and role-based review — not just an isolated ML script."

---

## 2. Complete Workflow (end-to-end)

```
User signs up → Firebase Auth → Role assigned (Researcher / CMLRE Staff)
   → Researcher uploads CSV + description
   → Validate file type, schema, required fields, empty values
   → Clean & preprocess data (dedupe, missing values, type fixes, normalization)
   → Generate embeddings on structured data → enables semantic search
   → Dataset metadata stored in Firebase Realtime Database
   → AI summarization flow (Genkit + Gemini) generates human-readable summary
   → CMLRE Staff reviews → Approve / Reject
   → Approved data → Dashboard (Recharts viz) + Search/Filter/Download
   → Rejected/deleted → Archive (soft delete) before permanent removal
```

**One-liner:** "Upload → clean/validate → embed → AI summarize → human review → visualize."

---

## 3. Tech Stack — What & Why (with alternatives)

| Layer | Used | Why I chose it | Alternative | Why not that |
|---|---|---|---|---|
| Frontend | Next.js 15 + TypeScript | Routing, server actions, SSR, one framework instead of stitching libraries | React + Vite | More manual setup, no built-in backend layer |
| Auth/DB | Firebase Auth + Realtime DB | Fast to ship, real-time updates, tight frontend integration for an MVP | PostgreSQL + custom auth | Slower to set up; better long-term but overkill for MVP timeline |
| AI orchestration | Google Genkit + Gemini | Structured, reusable "flows" for prompts instead of scattering API calls everywhere | Direct Gemini SDK / LangChain | Gets messy to organize as flows grow; Genkit keeps AI logic server-side & structured |
| Search | Embeddings (semantic search) | Keyword search misses fuzzy/biological terminology; embeddings find records by meaning | Plain SQL/keyword filter | Fails on synonyms, taxonomic naming variance |
| Styling | Tailwind + shadcn/Radix | Fast, consistent, accessible components out of the box | Plain CSS / Bootstrap | Slower custom UI work |
| Validation | Zod + React Hook Form | Type-safe validation that matches TS types automatically | Yup / manual checks | More boilerplate, weaker TS integration |
| Charts | Recharts | React-native, simple for dashboard-style charts | D3 | More powerful but overkill for standard charts |
| Deployment | Firebase App Hosting | Already in the Firebase ecosystem, minimal config | Vercel / AWS | Extra setup since rest of stack is Firebase-based |

**Defend Firebase vs SQL directly:** "Firebase gave me real-time sync and fast auth for an MVP. For production scale with complex relational queries across datasets, reviews, and users, I'd move metadata to PostgreSQL and keep files in object storage — Firebase doesn't handle complex joins well."

---

## 4. Database Design

```
users/{id}         → name, email, role, createdAt
datasets/{id}      → title, description, fileUrl, uploadedBy, status,
                      summary, rowCount, embeddingId, createdAt, updatedAt
reviews/{id}        → datasetId, reviewerId, decision, remarks, reviewedAt
notifications/{id}  → recipientId, message, datasetId, isRead
archive/{id}        → deletedBy, deletedAt, originalData
```

**Why split files from metadata?** "Large CSVs go to object storage; the DB only holds lightweight metadata (title, status, summary, URL) — keeps reads/writes fast."

**RBAC (Role-Based Access Control):** Users upload + view approved data. CMLRE Staff review/approve/reject/archive. "Auth confirms who you are; RBAC controls what you're allowed to do."

---

## 5. APIs / Modules

| Endpoint | Purpose |
|---|---|
| `POST /api/datasets` | Submit dataset |
| `GET /api/datasets` | List datasets |
| `PATCH /api/datasets/:id/status` | Approve/reject |
| `PATCH /api/datasets/:id/archive` | Archive |
| `POST /api/ai/summary` | Generate AI summary |
| `POST /api/ai/search` | Embedding-based semantic search |
| `GET /api/notifications` | Fetch notifications |

**Why server actions for AI calls?** "Keeps API keys and model logic server-side — calling Gemini directly from the browser would expose credentials."

---

## 6. Challenges & Bug Fixes

| Challenge | Fix |
|---|---|
| Inconsistent CSV schemas from different sources | Schema validation + field mapping before ingest |
| Missing/duplicate records | Cleaning pipeline: dedupe, impute/drop nulls |
| Large datasets exceeding LLM token limits | Send computed stats + representative sample, not the whole file |
| AI hallucination in summaries | Ground prompt in real computed stats; human review stays in the loop |
| Concurrent staff actions on same dataset | Optimistic concurrency (version field) — stale writes get rejected |
| Slow dashboard with large data | Pagination + server-side filtering |

---

## 7. Concurrency Scenario (rehearse this one — commonly asked)

**Q: "Two CMLRE staff approve/reject the same dataset at once — what happens?"**

"I'd use optimistic concurrency with a version field. Both read status=PENDING, version=3. First approval writes version=4. The second request still holds version=3, so the system detects a stale write and rejects it, forcing a reload of the latest state instead of silently overwriting. Firebase transactions can enforce this atomically."

---

## 8. Metrics — How I'd Defend Them

- **"45,000+ marine records"** → be ready to say whether this means rows/records processed across files, not 45,000 separate datasets. If asked for proof, describe your cleaning pipeline (source count, row count via `pandas`/`len(df)`).
- **"~40% reduction in manual review effort"** → frame as an internal timing comparison: average review time before AI summary vs. after. `(before - after) / before × 100`. Don't claim it as an audited CMLRE metric — say "internal comparison."
- If pushed on exact numbers you don't have memorized: "That was measured in an internal before/after timing test — I don't have the exact log in front of me, but the methodology was straightforward time comparison per submission."

---

## 9. Deployment

Firebase App Hosting, `maxInstances: 1` (fine for demo, not production).

**Production improvements I'd make:** autoscaling, monitoring/error tracking, re-enable TypeScript/ESLint build checks (currently ignored in `next.config.ts`), stricter Firebase security rules, rate limiting, audit logs, pagination, DB indexes.

---

## 10. Future Scope (with reasoning — "why this next")

| Feature | Why it's next |
|---|---|
| Move metadata to PostgreSQL | Firebase struggles with complex relational queries at scale — needed once dataset/review relationships grow |
| Live Copernicus Marine integration | Currently just a Python example script, not wired in — real-time ocean data would replace static uploads |
| Dataset quality scoring | Prioritize flawed submissions for review automatically instead of manual triage |
| Model/embedding monitoring | Detect drift in search quality over time |
| Async processing for large uploads | Avoid blocking the UI on big CSV/eDNA files |
| Audit trail | Full accountability on every approve/reject/delete action |
| Multilingual support | CMLRE-style platforms serve non-English-first researchers too |

**Why not built now?** "MVP timeline — I prioritized proving the core loop (upload → clean → embed → summarize → review) over scaling infrastructure."

---

## 11. Fast Answers to the 5 "Common Questions" Slide

1. **Explain your project / why chosen** → See §1.
2. **Complete workflow** → See §2 diagram.
3. **Database design, tech, APIs** → See §3–5.
4. **Challenges/bugs, future scope** → See §6, §10.
5. **Concurrency scenario** → See §7 — memorize this one, it's a classic trap question.

---

## 12. Things to NOT say

- ❌ "I built the entire platform alone" → ✅ "It was a team effort; I owned [preprocessing/embeddings/AI summarization] and understood the full architecture."
- ❌ Claiming exact accuracy/percentage numbers you can't reproduce on the spot → ✅ Describe the *method* you used to measure them.
- ❌ "The AI/Gemini proves the eDNA species match" → ✅ "It suggests candidate matches for a human researcher to verify — it's not a certified identification."
