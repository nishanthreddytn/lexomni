# LexOmni: The National Legal & Judicial Operating System

LexOmni is a unified workstation for Indian courts and law firms. It combines three things that are normally spread across six to eight separate tools:

1. **Litigation practice ERP**: limitation clocks, e-filing defect checks, conflict checks, cause-list and diary management, client CRM.
2. **Cognitive evidence and research tools**: OCR of scanned court records, cross-document contradiction detection, IPC to BNS statute bridging, precedent citation graphs, custody and default-bail clocks.
3. **Judicial bench suite**: pre-hearing bench memos, order-sheet drafting, live courtroom transcription, delay diagnostics.


---

## Why it exists

Law is a deadline-governed, high-liability domain. Typical failure modes LexOmni targets:

| Failure | Consequence | LexOmni answer |
| :--- | :--- | :--- |
| Appeal filed one day late | Dismissed under the Limitation Act, 1963 | Deterministic limitation engine |
| Petition formatting or fee defects | Registry rejection, weeks of delay | E-filing pre-scrutiny engine |
| Citing an overruled precedent | Loss of credibility before the bench | Precedent overruling graph |
| Missed default-bail day | Illegal continued detention | Custody clock auditor |
| Contradictions buried in 500-page bundles | Missed impeachment opportunities | Contradiction matrix |
| Confusion across the 1 July 2024 criminal-code change | Wrong sections cited | IPC to BNS / BNSS / BSA bridge |

---

## Three workspaces

| Workspace | Audience | Main capabilities |
| :--- | :--- | :--- |
| **Litigation CRM** | Partners, litigators, chamber admins | Matter docket and vault, limitation clock, e-filing defect clearance, conflict radar, senior counsel brief dossier, billing |
| **Cognitive Radar** | Researchers, trial counsel | Contradiction matrix, IPC to BNS/BNSS bridge, precedent overruling graph, Section 479 BNSS custody clock, evidence timeline, ratio decidendi retrieval |
| **The Bench** | Judges, law clerks | 2-page pre-hearing bench memos, daily order drafter, live steno and argument notes, backlog diagnostics, procedural violation radar, bail roster |

The specified UI has a global shell (top bar with coram status and `Ctrl/Cmd+K` precedent search, sidebar, floating context-aware AI assistant drawer) and **14 pages**: authentication and role switcher, executive dashboard, my cases and cause list, court diary, limitation engine, e-filing scrutinizer, client CRM, senior counsel briefing studio, document vault with OCR, contradiction radar, legal research and statute bridge, precedent graph, custody and bail clocks, and the judicial bench cockpit.

---

## Core engines

1. **Limitation Hard-Stop Engine**: takes order date, certified-copy application date and delivery date; computes the statutory window, excludes certified-copy time (Section 12) and applies Section 4 holiday and vacation adjustments; schedules cascading alerts at T-14d, T-7d, T-48h and T-2h. Includes an audit trace of the arithmetic.
2. **E-Filing Defect Scrutiny Engine**: checks margins, font and spacing, typed copies of handwritten annexures, Section 65B / Section 63 BSA electronic-evidence certificates, court fee and stamping, CNR format, DSC confirmation.
3. **Contradiction and Cross-Examination Matrix**: reads FIR, Section 161 and 164 statements, panchnama, seizure memo and medical reports; builds a timeline and a discrepancy table (time, weapon, injury, presence) with page-level source links and cross-examination prompts.
4. **Statute Transition Engine (IPC to BNS / BNSS / BSA)**: bidirectional section mapping, textual and penalty deltas, precedent-continuity flags.
5. **Precedent Overruling and Bench-Strength Graph**: negative citator that weights bench size and flags *Overruled*, *Distinguished*, *Doubted* or *Affirmed*.
6. **Custody Clock Auditor**: default-bail day under Section 187 BNSS / 167(2) CrPC (60 or 90 days) and the Section 479 BNSS half-time / one-third rule, with one-click bail application drafting.
7. **Senior Counsel Briefing Generator**: 4-part dossier (chronology, point of law, adverse findings in the impugned order, three winning authorities).
8. **Judicial Bench Workspace and Order Drafter**: 2-page bench memo, order templates (notice, adjournment, interim bail or injunction), live transcription.

The requirements spec extends this to 13 modules, adding Digital Munshi (summons and postal tracking), judge behaviour analytics, post-judgment execution under Order 21 CPC, and a corporate contract redliner and compliance auditor.

---

## Safety principles

1. **Source grounding**: every AI claim must pin to a page, paragraph and line, and clicking it opens the highlighted source.
2. **Deterministic math barrier**: generative models never count days or compute fees. Limitation, custody and court-fee logic run on plain Python `datetime` and arithmetic.
3. **Human in the loop**: the system never gives final legal advice or files anything autonomously; it briefs the licensed advocate or judge.

---

## Architecture

```
React 18 + Vite workstation  ──HTTPS/WSS──▶  FastAPI async backend  ──▶  PostgreSQL + pgvector (SQLite in dev)
                                                    │                    Vector index (Qdrant / pgvector)
                                                    │                    Graph engine (NetworkX)
                                                    ▼
                                      Celery + Redis workers (OCR, cause-list scrapers, postal tracking)
```

**Planned API surface:** `/api/crm`, `/api/filing`, `/api/evidence`, `/api/statute`, `/api/precedent`, `/api/custody`, `/api/steno`, `/api/briefing`, `/api/bench`.

### Stack

| Layer | Technology |
| :--- | :--- |
| Frontend | React 18, Vite, Tailwind, TanStack Table, React Flow, Zod |
| Backend | Python 3.12 (`.python-version`), FastAPI, Pydantic v2, SQLAlchemy |
| Database | SQLite (development), PostgreSQL with pgvector (production) |
| Documents and OCR | PyMuPDF, Docling, RapidOCR (ONNX, runs locally) |
| Search | Sentence-Transformers (`all-MiniLM-L6-v2`) with BM25 hybrid fusion |
| Speech | Whisper (`whisper-tiny` / `whisper-base`) |
| Legal LLM | Qwen 2.5 / DeepSeek / Mistral class models for memos and briefs |
| Graph | NetworkX (Neo4j as an option) |

### Data model (core tables)

`matters`, `hearings`, `documents`, `document_pages`, `document_chunks` (rhetorical labels: FACT, EVIDENCE, ARGUMENT, RATIO), `limitation_rules`, `statute_mappings`, `sc_judgments`, `precedent_citations`, `audit_logs`.

---

## Roles

Senior Counsel, High Court Judge, Legal Researcher and Chamber Admin. The specified login flow uses a role picker plus OTP. In development or demo mode a static OTP is shown on screen; this must be replaced with real authentication before any production use.

---

## Repository contents

| File | Purpose |
| :--- | :--- |
| `lexomni_master_specification.md` | Product spec: mission, three workspaces, eight engines, stack, five-sprint roadmap |
| `lexomni_master_requirements_spec.md` | SRS: 13 modules with worked examples, market comparison, architecture, safety laws, six-sprint plan |
| `LEXOMNI_EVERY_PAGE_FEATURE_GUIDE.md` | Page-by-page walkthrough: database rationale, AI models, flowcharts, legal-term glossary, user journeys |
| `vercel.json` | Vercel build: installs and builds inside `legal_judgement_system/`, serves `legal_judgement_system/dist`, SPA rewrite to `index.html` |
| `.vercelignore` | Keeps Python backend, ML weights, data and Markdown files out of the frontend deployment |
| `.npmrc` | `legacy-peer-deps=true` |
| `.python-version` | `3.12` |
| `.gitignore` | Ignores `node_modules`, Python caches, env files, databases, logs, archives |

---

## Deployment

The frontend deploys to Vercel using `vercel.json`:

```
installCommand:  cd legal_judgement_system && npm install --legacy-peer-deps
buildCommand:    cd legal_judgement_system && npm run build
outputDirectory: legal_judgement_system/dist
```

The Python backend, model weights and data are excluded from Vercel by `.vercelignore` and are intended to run as a separate service.

### Local development (once the application source is added)

```bash
# frontend
cd legal_judgement_system
npm install --legacy-peer-deps
npm run dev

# backend
python3.12 -m venv .venv && source .venv/bin/activate
pip install -r legal_judgement_system/requirements.txt
```

Copy secrets into a local `.env` (git-ignored). Never commit credentials.

---

## Roadmap

1. **Workstation UI**: multi-workspace React interface.
2. **Deterministic clocks**: limitation engine and Section 187 / 479 BNSS custody clocks in pure Python.
3. **Statute bridge**: IPC to BNS / BNSS / BSA mapping database with deltas and precedent continuity.
4. **Evidentiary contradiction matrix**: multi-document extraction and clickable source pins.
5. **Precedent overruling graph**: negative citator with bench-strength weighting.
6. **Dossier and bench memo exporters**: one-click court-ready PDF/DOCX.

---

## Open items to resolve in the specs

These inconsistencies exist across the current documents and should be settled before implementation:

- **Python version**: `.python-version` says 3.12, the feature guide's architecture diagram says 3.11.
- **Vector store**: Qdrant/Milvus in the specs versus ChromaDB in the guide's diagram.
- **Corpus size**: "34k+ ILDC Supreme Court judgments" in the SRS versus "4.5 million judgments" in the guide.
- **Limitation Act sections**: the specs cite Section 4 (holidays) and Section 12 (certified-copy exclusion); make sure the UI and engine use the same terminology and tests.
- **Default-bail wording**: Day 61 / Day 91 (entitlement day) versus the 60 / 90-day deadline; keep one definition in the clock logic and UI copy.
- **Roadmap length**: five sprints in the master spec versus six in the SRS.
- **Marketing claims**: statistics such as "70% of petitions rejected" and judge-level percentages in the examples are illustrative and need sourcing or removal before any public use.
- **Legal accuracy**: all statutory timelines, fees and section mappings must be verified by a qualified advocate before being encoded.

---

## Disclaimer

LexOmni is a decision-support tool for licensed advocates and judges. It does not provide legal advice and does not file anything on a user's behalf.
