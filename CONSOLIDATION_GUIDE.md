# PIRV Repository Consolidation Guide

**Status:** ✅ COMPLETE  
**Date Consolidated:** June 7, 2026  
**Owner:** dpayvid

---

## What Was Consolidated

Four independent repositories merged into unified `dpayvid/PIRV`:

### 1. pirv-agricircle → `/pirv-agricircle/`
**Portfolio scoring & automation engine**
- 31 circular bio-economy modules (C01–C31)
- Evidence-weighted scoring system
- Financial gating & portfolio health
- Investor memos & compliance automation
- 18+ GitHub Actions workflows
- Python automation scripts
- Full test suite (pytest)

**Key Files:**
- `requirements-pirv-agricircle.txt` — dependencies
- `CHANGELOG.md` — all 6 development passes documented
- `.github/workflows/` — 18 automated workflows
- `automation/` — 30+ core scripts

### 2. pirv-spaces-config → `/pirv-spaces-config/`
**Knowledge architecture & space management**
- 54+ Perplexity Spaces configuration
- Master index & interconnection maps
- Automated audit & content sync
- Weekly digests & compliance reports
- Space YAML configs (C01–C31 + integrations)

**Key Files:**
- `requirements-spaces-config.txt` — dependencies
- `master-index.yaml` — master space index
- `link-graph.json` — space dependency graph
- `scripts/` — audit, validation, reporting automation

### 3. agricircle-waste-matrix-api → `/agricircle-waste-matrix-api/`
**FastAPI backend for waste metrics**
- India State-Wise Master Waste & Residue Matrix 2026
- REST API with state rankings & Bihar PIRV scores
- Docker & Kubernetes deployment configs
- OpenAPI/Swagger documentation

**Key Files:**
- `requirements-waste-matrix-api.txt` — dependencies
- `main.py` — FastAPI application
- `docker-compose.yml` — local development
- `k8s/` — Kubernetes manifests

### 4. pirv-spaces → `/pirv-spaces/`
**Curated knowledge collection**
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

## How to Use Each Component

### PIRV AgriCircle

```bash
cd pirv-agricircle

# Install dependencies
pip install -r ../requirements-pirv-agricircle.txt

# Run tests
pytest tests/ -v

# Run scoring pipeline
python automation/evidence-weighting/evidence_weighted_scoring.py

# Run compliance check
python automation/compliance_bot.py

# Trigger via GitHub Actions
# Go to: Actions → Full Pipeline → Run workflow
```

### PIRV Spaces Config

```bash
cd pirv-spaces-config

# Install dependencies
pip install -r ../requirements-spaces-config.txt

# Run audit (locally)
python scripts/audit_spaces.py

# Validate secrets
python scripts/validate_secrets.py

# Generate weekly report
python scripts/generate_weekly_report.py
```

### Waste Matrix API

```bash
cd agricircle-waste-matrix-api

# Install dependencies
pip install -r ../requirements-waste-matrix-api.txt

# Run locally
uvicorn main:app --reload

# Access API docs
# http://localhost:8000/docs

# Run tests
pytest tests/ -v

# Run with Docker
docker-compose up -d
```

### Knowledge Collection

```bash
cd pirv-spaces

# Browse documentation
# All markdown files in numbered folders (01–10)
# Start with: 01-vision-and-strategy/README.md
```

---

## Automated Workflows

### PIRV AgriCircle Schedules (UTC)

| Time | Workflow | Purpose |
|------|----------|--------|
| 01:00 daily | Data Acquisition | Fetch commodity prices, weather, carbon data |
| 06:00 daily | Autonomous Data Pipeline | Normalize & process collected data |
| 06:30 daily | Spaces Sync | Sync scores to Perplexity Spaces |
| 07:00 daily | DSCR Gate Monitor | Check financial gates |
| 07:30 daily | Portfolio Health Check | Generate health report |
| Mon 06:00 | Compliance Bot | Audit all 31 modules |
| Mon 08:00 | Evidence Tracker | Update evidence registry |
| Mon 09:00 | Evidence Weighter | Re-score portfolio |
| Fri 18:00 | Spaces Audit | Audit Perplexity Spaces |
| Sun 20:00 | Master Synthesis | Weekly master report |

### PIRV Spaces Config Schedules (UTC)

| Workflow | Schedule | Purpose |
|----------|----------|--------|
| Full Audit | Mon + Wed 02:00 | Scan all configs, validate schema |
| Content Sync | Tue + Fri 03:00 | Roadmaps, instructions, updates |
| Secret Rotation | Every 90 days | Rotation checklist |

---

## Directory Structure Map

```
PIRV/
├── README.md                           # Main repo documentation
├── CONSOLIDATION_GUIDE.md             # This file
├── .gitignore                         # Unified git ignore
├── requirements-pirv-agricircle.txt   # AgriCircle deps
├── requirements-spaces-config.txt     # Spaces deps
├── requirements-waste-matrix-api.txt  # API deps
│
├── pirv-agricircle/                   # Portfolio engine
│   ├── automation/                    # 30+ core scripts
│   ├── companies/C01-C31/             # Module data
│   ├── financials/                    # Economics CSVs
│   ├── evidence-ingestion/            # Evidence registry
│   ├── tests/                         # Pytest suite
│   ├── .github/workflows/             # 18 workflows
│   ├── requirements.txt               # Local deps
│   ├── README.md
│   ├── CHANGELOG.md                   # Pass 1–6 history
│   └── MASTER_STATUS.md               # Inventory
│
├── pirv-spaces-config/                # Knowledge architecture
│   ├── spaces/                        # 54+ YAML configs
│   ├── scripts/                       # Audit, validation
│   ├── roadmaps/                      # Auto blueprints
│   ├── master-index.yaml              # Space index
│   ├── link-graph.json                # Dependencies
│   ├── requirements.txt               # Local deps
│   └── README.md
│
├── agricircle-waste-matrix-api/       # Waste API
│   ├── main.py                        # FastAPI app
│   ├── routers/                       # Endpoints
│   ├── data/                          # Excel matrix
│   ├── k8s/                           # K8s manifests
│   ├── docker-compose.yml
│   ├── Dockerfile
│   ├── requirements.txt               # Local deps
│   └── README.md
│
└── pirv-spaces/                       # Knowledge collection
    ├── 01-vision-and-strategy/
    ├── 02-business-models/
    ├── 03-projects-and-dprs/
    ├── 04-research/
    ├── 05-financial-models/
    ├── 06-policy-and-compliance/
    ├── 07-operations/
    ├── 08-data-and-dashboards/
    ├── 09-partnerships-and-stakeholders/
    ├── 10-brand-and-communications/
    └── README.md
```

---

## Secrets Configuration

### GitHub Actions Secrets

Configure in **Settings → Secrets → Actions**:

**For AgriCircle Workflows:**
- `PERPLEXITY_WEBHOOK_URL` — Webhook for notifications (required)

**For Spaces Config Workflows:**
- `PERPLEXITY_API_KEY` — [Get from Perplexity](https://www.perplexity.ai/settings/api)
- `PIRV_NOTIFICATION_EMAIL` — Alert email address

---

## Development Workflow

### Adding Evidence

1. Edit: `pirv-agricircle/evidence-ingestion/evidence-registry.csv`
2. Follow: `pirv-agricircle/evidence-requirements/` checklists
3. Commit with ticket reference
4. Trigger: Full Pipeline workflow → `stage: scoring`

### Updating Financials

1. Edit: `pirv-agricircle/financials/unit-economics/C{NN}-financials.csv`
2. Update: `pirv-agricircle/financials/PORTFOLIO-MASTER-FINANCIALS.csv`
3. Commit with change summary
4. Trigger: DSCR Gate Monitor workflow

### Adding Automation Scripts

1. Create: `pirv-agricircle/automation/new_feature/new_script.py`
2. Add dependencies to: `requirements-pirv-agricircle.txt`
3. Add tests to: `pirv-agricircle/tests/test_new_script.py`
4. Wire in: `.github/workflows/` (appropriate workflow)
5. Document in: `pirv-agricircle/CHANGELOG.md`

### Space Configuration

1. Edit: `pirv-spaces-config/spaces/` YAML files
2. Update: `pirv-spaces-config/master-index.yaml`
3. Validate: `python pirv-spaces-config/scripts/audit_spaces.py`
4. Commit and workflows auto-run

---

## Troubleshooting

### Workflow Fails

1. Check logs: **Actions → workflow name → failed run → logs**
2. Verify secrets configured: **Settings → Secrets → Actions**
3. Check Python version: `python --version` (3.10+)
4. Verify requirements: `pip install -r requirements-*.txt`

### Import Errors in Scripts

```bash
# From repository root
cd pirv-agricircle
export PYTHONPATH="${PYTHONPATH}:$(pwd)"
python automation/script_name.py
```

### API Won't Start

```bash
cd agricircle-waste-matrix-api
# Verify Excel file exists
ls -la data/India-State-Wise-Master-Waste-Residue-Matrix-2026.xlsx

# Install all deps
pip install -r requirements.txt

# Run with verbose output
uvicorn main:app --reload --log-level debug
```

---

## Next Steps

1. ✅ **Review README.md** — Understand unified structure
2. ✅ **Install dependencies** — Run appropriate requirements file
3. ✅ **Run tests** — Verify everything working
4. ✅ **Configure secrets** — GitHub Actions integration
5. ✅ **Trigger pipelines** — Activate automated workflows

---

## Support

**Questions?** Check:
- `pirv-agricircle/CONTRIBUTING.md` — Contribution guidelines
- `pirv-spaces-config/README.md` — Space architecture details
- `agricircle-waste-matrix-api/README.md` — API documentation

**Project Lead:** Divya Payvid (@dpayvid)  
**Repository:** https://github.com/dpayvid/PIRV  
**Status:** All systems operational ✅
