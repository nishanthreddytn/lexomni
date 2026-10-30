# LexOmni: The National Legal & Judicial Operating System
## Master Product Specification & Engineering Architecture

> **Document Type**: Ground-Up Greenfield Engineering Specification  
> **System Scope**: Enterprise Legal Practice ERP + High-Stakes Litigation Cognitive Intelligence + Judicial Bench Automation  
> **Target Deployments**: Tier-1 Law Firms, High-Stakes Litigators, Corporate General Counsels, and Court Benches  

---

## 1. Executive Mission & Thesis

Current legal technology treats law firms and courts as users of generic chat widgets or isolated document search boxes. This fails because law is a **high-liability, procedural, deadline-governed domain**. A mistake of 24 hours in filing results in dismissal under the Limitation Act; a mistake in citing an overruled precedent causes humiliation before a judge; an oversight in custody calculation results in illegal detention.

**LexOmni** is architected as the **National Legal Infrastructure (NLI) Operating System**. It unifies:
1. **The Operational Practice ERP**: Conflict checks, e-filing defect clearance, limitation clocks, cause-list sync, and time billing.
2. **The Cognitive Intelligence Suite**: Evidentiary contradiction matrices, IPC-to-BNS statutory bridging, precedent validity graphs, and custody bail auditing.
3. **The Judicial Bench Operating Suite**: Automated 2-page pre-hearing Bench Memos, courtroom stenography transcription, and automated daily order drafting.

---

## 2. The 3 Primary Workspaces

```
                                  ┌────────────────────────────────────────────────────────┐
                                  │               LEXOMNI MASTER WORKSPACE                 │
                                  └───────────────────────────┬────────────────────────────┘
                                                              │
         ┌────────────────────────────────────────────────────┼────────────────────────────────────────────────────┐
         │                                                    │                                                    │
         ▼                                                    ▼                                                    ▼
┌───────────────────────────────────┐        ┌───────────────────────────────────┐        ┌───────────────────────────────────┐
│     WORKSPACE 1: LITIGATION CRM   │        │     WORKSPACE 2: COGNITIVE RADAR  │        │     WORKSPACE 3: THE BENCH        │
│    (Partners & Litigators)        │        │   (Researchers & Trial Counsel)   │        │      (Judges & Law Clerks)        │
├───────────────────────────────────┤        ├───────────────────────────────────┤        ├───────────────────────────────────┤
│ • Matter Docket & Vault           │        │ • Multi-Doc Contradiction Matrix  │        │ • 2-Page Pre-Hearing Bench Memos  │
│ • Limitation Clock (Deadlines)    │        │ • IPC ➔ BNS / BNSS Statute Bridge │        │ • Daily Court Order Sheet Drafter │
│ • e-Filing Defect Clearance       │        │ • Precedent Overruling Graph      │        │ • Live Steno & Argument Note-Taker│
│ • Conflict of Interest Radar      │        │ • Sec 479 BNSS Custody Bail Clock │        │ • Case Delay & Backlog Diagnostics│
│ • Senior Counsel Brief Dossier    │        │ • Evidence Timeline Reconstruction│        │ • Procedural Violation Radar      │
│ • Billable Hours & Court Ledger   │        │ • Ratio Decidendi Deep Retrieval  │        │ • Bail Roster Management          │
└───────────────────────────────────┘        └───────────────────────────────────┘        └───────────────────────────────────┘
```

---

## 3. Modular Engine Specifications

### Engine 1: The Limitation Act Deadline Hard-Stop Engine
* **Purpose**: Prevents procedural dismissal under the **Limitation Act, 1963**.
* **Algorithm**:
  1. Ingests Impugned Order Date, Certified Copy Application Date, and Certified Copy Delivery Date.
  2. Computes the statutory limitation window according to Schedule 1 (e.g., 30 days for High Court criminal appeals, 90 days for civil appeals, 3 years for commercial recovery).
  3. Excludes statutory holidays and High Court summer/winter vacations under Section 4.
  4. Generates automated calendar events with cascading partner alerts at T-14d, T-7d, T-48h, and T-2h.

### Engine 2: The E-Filing Defect Scrutiny Engine
* **Purpose**: Simulates the scrutiny counter of the High Court and Supreme Court registries to ensure zero-defect first-pass e-filing.
* **Audit Rules**:
  1. *Typography & Margins*: Validates 1.5-inch left margin, double-spacing, Bookman Old Style font.
  2. *True-Typing Verification*: Verifies that dim or handwritten annexures have accompanying typed copies.
  3. *Electronic Evidence Certificate*: Audits mandatory certificate compliance under Section 65B of the Indian Evidence Act / Section 63 of the Bharatiya Sakshya Adhiniyam (BSA).
  4. *Court Fee & Stamping Schedule*: Computes ad-valorem court fees per jurisdiction.

### Engine 3: Evidentiary Contradiction & Cross-Examination Matrix
* **Purpose**: Analyzes criminal police bundles (FIR, Section 161 witness statements, Section 164 statements, Panchnama, Seizure memo, and Medical/Post-Mortem reports).
* **Output**:
  - A chronological incident timeline.
  - A structured **Contradiction Matrix** flagging discrepancies in time, weapon, injury, and presence.
  - Direct deep-links to the exact page and line of the scanned PDF exhibits.
  - Automated cross-examination prompts for defense counsel.

### Engine 4: The Dynamic Statute Transition Engine (IPC ➔ BNS / BNSS / BSA)
* **Purpose**: Seamlessly bridges 70 years of Indian case law across the July 1, 2024 criminal code transition.
* **Output**:
  - Bidirectional section mapping (IPC ➔ BNS, CrPC ➔ BNSS, IEA ➔ BSA).
  - Highlighting textual and penalty deltas (e.g., introduction of community service, changed custody timelines under Section 187 BNSS).
  - Precedent continuity flags showing whether Supreme Court rulings decided under the old statute remain valid or are legally narrowed.

### Engine 5: Precedent Overruling & Bench Strength Knowledge Graph
* **Purpose**: Negative citator (Shepardizing) engine for Indian case law.
* **Logic**:
  - Traverses the precedent citation tree.
  - Applies constitutional bench weighting: a 5-Judge Constitution Bench decision overrules any 2-Judge or 3-Judge Division Bench decision.
  - Emits real-time visual alerts: *Overruled*, *Distinguished*, *Doubted*, or *Affirmed*.

### Engine 6: Procedural Compliance & Custody Clock Auditor
* **Purpose**: Human rights auditing and elimination of illegal detention.
* **Logic**:
  - **Section 167(2) CrPC / Section 187 BNSS Default Bail Clock**: Flags the exact day (Day 61 or Day 91) an inmate becomes entitled to non-discretionary default bail.
  - **Section 479 BNSS Half-Time Rule**: Flags when an under-trial prisoner has served 1/3rd (first-time offender) or 1/2 (repeat offender) of the maximum statutory term.
  - Generates a ready-to-file statutory bail petition with a single click.

### Engine 7: The Senior Counsel Briefing Generator (Solicitor-to-Senior Pipeline)
* **Purpose**: Automates the 48-hour overnight briefing preparation for Senior Advocates.
* **Output**: A standardized 4-part dossier:
  1. *Chronological List of Dates and Events*.
  2. *Point of Law (The Single Substantial Legal Question)*.
  3. *Adverse Findings in Impugned Order*.
  4. *The 3 Primary Winning Authorities with Highlighted Paragraphs*.

### Engine 8: The Judicial Bench Workspace & Order Drafter
* **Purpose**: Cognitive decision support for judges hearing 60+ matters per day.
* **Output**:
  - **Automated 2-Page Pre-Hearing Bench Memo**: Summary of procedural stage, admitted vs. contested facts, and core statutory questions.
  - **Daily Order Sheet Drafter**: Instant templates for adjournment orders, notice orders, and reasoned interim bail/injunction orders.

---

## 4. Greenfield Technical Architecture

### Backend Stack
* **Language**: Python 3.12+
* **API Framework**: FastAPI (Async event loops, native Pydantic v2 schemas, OpenAPI specs)
* **Database Layer**: SQLite (development) / PostgreSQL with pgvector (production)
* **Deterministic Computation**: Pure Python math/datetime engines for limitation, custody clocks, and fee calculations.
* **Document Parsing**: PyMuPDF + Docling for layout-aware legal parsing.
* **Search & Vectors**: Sentence-Transformers + BM25 hybrid fusion + Qdrant/pgvector.
* **Graph Engine**: NetworkX for precedent citation graphs and bench hierarchy traversal.

### Frontend Stack
* **Framework**: React 18 + Vite
* **Design Philosophy**: High-density, institutional dark/light workstation (Bloomberg terminal aesthetics tailored for high-stakes legal operations).
* **Components**: Multi-panel split document viewer, interactive contradiction matrix, live calendar cause-list board, and instant export to court-ready PDF and DOCX.

---

## 5. Implementation Roadmap

1. **Sprint 1: The Master Workstation Navigation**: Implement the React 18 multi-workspace interface (**Litigation CRM**, **Cognitive Evidence Radar**, **The Judicial Bench**).
2. **Sprint 2: Deterministic Legal Engines**: Implement the **Limitation Act Engine**, **Custody & Bail Clock**, and **IPC ➔ BNS Statute Bridge** in FastAPI.
3. **Sprint 3: The Evidentiary Contradiction Engine**: Build multi-document entity extraction and interactive conflict matrix.
4. **Sprint 4: Precedent Overruling & Citator Graph**: Build the negative citator and bench strength hierarchy analyzer.
5. **Sprint 5: Automated Dossier & Bench Memo Exporters**: Add 1-click generation of Senior Counsel Briefs and Judicial Bench Memos.
