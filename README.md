# PIRV — Unified Ecosystem Repository

> **India's circular bio-economy backbone consolidated** — All PIRV/AGRICIRCLE modules, spaces configuration, API backend, and knowledge architecture in one unified repository.

## 📦 What's Consolidated Here

This is the **master unified repository** containing all four core PIRV systems:

### 1. **pirv-agricircle/** — Portfolio & Automation Engine
- 31 integrated circular bio-economy modules (C01–C31)
- Evidence-weighted scoring system
- Portfolio health checks & financial gating
- Investor memos & compliance automation
- 18+ GitHub Actions workflows
- 30+ automation scripts

**Key Metrics:**
- Financial gates: DSCR ≥ 1.25, IRR ≥ 18%, Payback ≤ 7 years
- Anchor geography: Bihar, India
- Status: [See MASTER_STATUS.md](pirv-agricircle/MASTER_STATUS.md)

### 2. **pirv-spaces-config/** — Knowledge Architecture
- 54+ Perplexity Spaces configuration (C01–C31 + integrations)
- Master index & space mapping
- Automated audit & content sync workflows
- Interconnection loops & dependency graphs
- Weekly digests & compliance reports

**Structure:**
- C01–C31 Core Modules (31 spaces)
- INT (Integrations): 8 spaces
- CF (Cross-functional): 5 spaces
- ECO (Ecosystem): 4 spaces
- DATA: 4 spaces

### 3. **agricircle-waste-matrix-api/** — Waste & Surplus Data Backend
- FastAPI service for India State-Wise Master Waste & Residue Matrix 2026
- State-level waste metrics & rankings
- Bihar PIRV opportunity scoring
- Docker & Kubernetes deployment configs
- RESTful API with interactive docs

**Key Endpoints:**
- `/health` — Health check
- `/states` — State waste metrics
- `/ranking/states` — State rankings
- `/bihar/pirv-priority` — Bihar PIRV scores

### 4. **pirv-spaces/** — Curated Knowledge Collection
- Vision & Strategy (01)
- Business Models (02)
- Projects & DPRs (03)
- Research (04)
- Financial Models (05)
- Policy & Compliance (06)
- Operations (07)
- Data & Dashboards (08)
- Partnerships (09)
- Brand & Communications (10)

---

## 🗂️ Repository Structure

```
PIRV/
├── pirv-agricircle/                    # Portfolio scoring & automation
│   ├── companies/C01-C31/              # Per-module data
│   ├── financials/                     # Unit economics & portfolio
│   ├── automation/                     # Data, scoring, memos, dashboards
│   ├── evidence-ingestion/             # Evidence registry
│   ├── portfolio-control/              # Rankings & gate status
│   ├── tests/                          # Pytest suite
│   ├── .github/workflows/              # 18 GitHub Actions workflows
│   └── README.md
│
├── pirv-spaces-config/                 # Knowledge architecture
│   ├── spaces/                         # 54+ space YAML configs
│   ├── roadmaps/                       # Auto-generated blueprints
│   ├── instructions/                   # Space instructions
│   ├── interconnections/               # Dependency maps
│   ├── scripts/                        # Audit, validation, reporting
│   ├── master-index.yaml               # Master space index
│   ├── link-graph.json                 # Cross-link graph
│   ├── status-dashboard.json           # Live status
│   └── README.md
│
├── agricircle-waste-matrix-api/        # Waste matrix API
│   ├── main.py                         # FastAPI app
│   ├── routers/                        # API endpoints
│   ├── utils/                          # Helpers
│   ├── data/                           # Excel matrix
│   ├── docker-compose.yml              # Local development
│   ├── Dockerfile                      # Container image
│   ├── k8s/                            # Kubernetes manifests
│   └── README.md
│
├── pirv-spaces/                        # Curated knowledge
│   ├── 01-vision-and-strategy/
│   ├── 02-business-models/
│   ├── 03-projects-and-dprs/
│   ├── 04-research/
│   ├── 05-financial-models/
│   ├── 06-policy-and-compliance/
│   ├── 07-operations/
│   ├── 08-data-and-dashboards/
│   ├── 09-partnerships-and-stakeholders/
│   ├── 10-brand-and-communications/
│   └── README.md
│
└── README.md (this file)
```

---

## 🚀 Quick Start

### Clone & Setup
```bash
git clone https://github.com/dpayvid/PIRV.git
cd PIRV
```

### Run PIRV AgriCircle Pipeline
```bash
cd pirv-agricircle
pip install -r requirements.txt
pytest tests/ -v
python automation/evidence-weighting/evidence_weighted_scoring.py
python automation/portfolio_health_check.py
```

### Run Waste Matrix API
```bash
cd agricircle-waste-matrix-api
pip install -r requirements.txt
uvicorn main:app --reload
# Open: http://localhost:8000/docs
```

### Trigger Full Automation (GitHub Actions)
Go to **Actions → Full Pipeline** and click **Run workflow**

---

## 📊 Automated Schedules

### PIRV AgriCircle
| Time (UTC) | Workflow |
|---|---|
| 01:00 daily | Data Acquisition |
| 06:00 daily | Autonomous Data Pipeline |
| 06:30 daily | Spaces Sync |
| 07:00 daily | DSCR Gate Monitor |
| 07:30 daily | Portfolio Health Check |
| Mon 06:00 | Compliance Bot |
| Mon 08:00 | Evidence Tracker |
| Fri 18:00 | Spaces Audit |

### PIRV Spaces Config
| Workflow | Schedule |
|---|---|
| Full Audit | Mon + Wed 02:00 UTC |
| Content Sync | Tue + Fri 03:00 UTC |
| Secret Rotation | Every 90 days |

---

## 🔐 Secrets Required

Configure in **Settings → Secrets → Actions**:

### PIRV AgriCircle
- `PERPLEXITY_WEBHOOK_URL` — Webhook for notifications (required)
- `GITHUB_TOKEN` — Auto-provided by GitHub Actions

### PIRV Spaces Config
- `PERPLEXITY_API_KEY` — [Get here](https://www.perplexity.ai/settings/api)
- `PIRV_NOTIFICATION_EMAIL` — Alert email

---

## 📖 Documentation

- **[pirv-agricircle/MASTER_STATUS.md](pirv-agricircle/MASTER_STATUS.md)** — Live repo health & checklist
- **[pirv-agricircle/docs/data-dictionary.md](pirv-agricircle/docs/data-dictionary.md)** — All CSV field definitions
- **[pirv-agricircle/docs/spaces-guide.md](pirv-agricircle/docs/spaces-guide.md)** — Perplexity Spaces routing
- **[pirv-spaces-config/README.md](pirv-spaces-config/README.md)** — Space architecture details
- **[agricircle-waste-matrix-api/README.md](agricircle-waste-matrix-api/README.md)** — API documentation

---

## 🤝 Contributing

See **[pirv-agricircle/CONTRIBUTING.md](pirv-agricircle/CONTRIBUTING.md)** for guidelines on:
- Adding evidence to modules
- Updating financial models
- Adding automation scripts
- Creating new DPRs

---

## 📬 Key Contact

**Divya Payvid** (@dpayvid)  
PIRV Project Lead, AGRICIRCLE Circular Bio-Economy Ecosystem  
India 🇮🇳

---

**Last Updated:** June 7, 2026  
**Repository Consolidation:** COMPLETE ✅  
**Unified Status:** All 4 systems operational
