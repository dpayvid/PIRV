# PIRV Quick Reference Guide

**Quick Navigation for Unified PIRV Ecosystem**

---

## 🚀 Quick Start (5 Minutes)

```bash
# Clone repository
git clone https://github.com/dpayvid/PIRV.git
cd PIRV

# Choose your component and install
pip install -r requirements-pirv-agricircle.txt  # Portfolio engine
# OR
pip install -r requirements-spaces-config.txt     # Knowledge config
# OR
pip install -r requirements-waste-matrix-api.txt  # Waste API

# Run tests
pytest pirv-agricircle/tests/ -v

# View documentation
cat README.md
```

---

## 📂 Component Quick Links

### 📊 PIRV AgriCircle
**Portfolio Scoring & Automation Engine**
- Location: `/pirv-agricircle/`
- Purpose: 31-module portfolio management
- Key Files:
  - `README.md` — Main documentation
  - `automation/` — 30+ core scripts
  - `.github/workflows/` — 18 automated workflows
  - `requirements.txt` — Dependencies
- Quick Command: `cd pirv-agricircle && pytest tests/ -v`

### 🌐 PIRV Spaces Config
**Knowledge Architecture (54 Spaces)**
- Location: `/pirv-spaces-config/`
- Purpose: Perplexity Spaces management
- Key Files:
  - `README.md` — Space architecture
  - `master-index.yaml` — Space index
  - `scripts/audit_spaces.py` — Validation
  - `link-graph.json` — Dependencies
- Quick Command: `cd pirv-spaces-config && python scripts/audit_spaces.py`

### 🗑️ Waste Matrix API
**FastAPI Backend for Waste Metrics**
- Location: `/agricircle-waste-matrix-api/`
- Purpose: State-level waste rankings
- Key Files:
  - `README.md` — API documentation
  - `main.py` — FastAPI application
  - `docker-compose.yml` — Local setup
  - `requirements.txt` — Dependencies
- Quick Command: `cd agricircle-waste-matrix-api && uvicorn main:app --reload`

### 📚 PIRV Spaces
**Curated Knowledge Collection**
- Location: `/pirv-spaces/`
- Purpose: Strategic & operational knowledge
- Key Files:
  - `01-vision-and-strategy/` — Master concepts
  - `02-business-models/` — Unit economics
  - `03-projects-and-dprs/` — Project docs
  - `04-research/` — Research summaries
- Quick Command: `cat pirv-spaces/README.md`

---

## ⚙️ Common Tasks

### Run All Tests
```bash
cd pirv-agricircle
pip install -r ../requirements-pirv-agricircle.txt
pytest tests/ -v --tb=short
```

### Start Waste API
```bash
cd agricircle-waste-matrix-api
pip install -r ../requirements-waste-matrix-api.txt
uvicorn main:app --reload
# Open: http://localhost:8000/docs
```

### Validate Spaces Config
```bash
cd pirv-spaces-config
pip install -r ../requirements-spaces-config.txt
python scripts/audit_spaces.py --validate
```

### Run Compliance Bot
```bash
cd pirv-agricircle
python automation/compliance_bot.py
```

### Generate Portfolio Report
```bash
cd pirv-agricircle
python automation/evidence-weighting/evidence_weighted_scoring.py
```

---

## 🔄 Workflow Triggers

### GitHub Actions Dashboard
**URL:** https://github.com/dpayvid/PIRV/actions

### Manual Workflow Runs
1. Go to Actions tab
2. Select workflow (e.g., "Tests", "Data Acquisition")
3. Click "Run workflow"
4. Monitor execution

### Scheduled Workflows
- **Daily 01:00 UTC** — Data Acquisition
- **Daily 06:00 UTC** — Autonomous Data Pipeline
- **Mon 06:00 UTC** — Compliance Bot
- **Fri 18:00 UTC** — Spaces Audit
- **Sun 20:00 UTC** — Master Synthesis

---

## 🔑 Configuration

### GitHub Secrets (Required)
Go to: **Settings → Secrets → Actions**

Required secrets:
- `PERPLEXITY_WEBHOOK_URL` — Notifications webhook
- `PERPLEXITY_API_KEY` — API access
- `PIRV_NOTIFICATION_EMAIL` — Alert email

### Environment Variables (Local Development)
Create `.env` file:
```bash
PERPLEXITY_WEBHOOK_URL=https://webhook.example.com
PERPLEXITY_API_KEY=pplx_...
PIRV_NOTIFICATION_EMAIL=email@example.com
```

---

## 📊 Portfolio Metrics

### Key Numbers
| Metric | Value |
|--------|-------|
| Portfolio Modules | 31 (C01–C31) |
| Perplexity Spaces | 54+ |
| Automation Scripts | 30+ |
| GitHub Workflows | 18+ |
| DSCR Floor | ≥ 1.25 |
| IRR Floor | ≥ 18% |
| Max Payback | 7 years |

### Financial Gates
```
DSCR Gate:     ≥ 1.25  ✅
IRR Gate:      ≥ 18%   ✅
Payback Gate:  ≤ 7y    ✅
```

---

## 📖 Documentation Index

### Essential Reading (Start Here)
1. [README.md](README.md) — Main overview
2. [CONSOLIDATION_GUIDE.md](CONSOLIDATION_GUIDE.md) — How it's organized
3. This Quick Reference — Common tasks

### Component Documentation
- [pirv-agricircle/README.md](pirv-agricircle/README.md)
- [pirv-spaces-config/README.md](pirv-spaces-config/README.md)
- [agricircle-waste-matrix-api/README.md](agricircle-waste-matrix-api/README.md)
- [pirv-spaces/README.md](pirv-spaces/README.md)

### Development Guides
- [pirv-agricircle/CONTRIBUTING.md](pirv-agricircle/CONTRIBUTING.md)
- [pirv-agricircle/MASTER_STATUS.md](pirv-agricircle/MASTER_STATUS.md)
- [pirv-agricircle/CHANGELOG.md](pirv-agricircle/CHANGELOG.md)

---

## 🆘 Troubleshooting

### Python Import Errors
```bash
# Set PYTHONPATH
cd pirv-agricircle
export PYTHONPATH="${PYTHONPATH}:$(pwd)"
python automation/script.py
```

### Workflow Failures
1. Check GitHub Actions logs
2. Verify secrets are configured
3. Ensure Python >= 3.10
4. Run `pip install -r requirements-*.txt`

### API Won't Start
```bash
cd agricircle-waste-matrix-api
# Verify Excel file exists
ls -la data/*.xlsx
# Check port availability
lsof -i :8000
# Install dependencies
pip install -r ../requirements-waste-matrix-api.txt
```

### Git Issues
```bash
# Update submodules
git submodule update --init --recursive

# Reset local changes
git reset --hard HEAD

# Pull latest
git pull origin main
```

---

## 🎯 Common Developer Tasks

### Adding Evidence
1. Edit: `pirv-agricircle/evidence-ingestion/evidence-registry.csv`
2. Commit with ticket reference
3. Trigger: Full Pipeline → `stage: scoring`

### Updating Financials
1. Edit: `pirv-agricircle/financials/unit-economics/C{NN}-financials.csv`
2. Update: `PORTFOLIO-MASTER-FINANCIALS.csv`
3. Trigger: DSCR Gate Monitor workflow

### Adding New Script
1. Create: `pirv-agricircle/automation/new_feature/script.py`
2. Add dependencies to: `requirements-pirv-agricircle.txt`
3. Add tests to: `pirv-agricircle/tests/test_script.py`
4. Document in: `CHANGELOG.md`

### Deploying API
```bash
cd agricircle-waste-matrix-api

# Docker build
docker build -t pirv-waste-api:latest .

# Or use docker-compose
docker-compose up -d

# Kubernetes (if available)
kubectl apply -f k8s/
```

---

## 📞 Support

**Questions?** Check:
- README.md — Overall documentation
- Component-specific README.md files
- GitHub Issues — For bug reports
- GitHub Discussions — For Q&A

**Repository:** https://github.com/dpayvid/PIRV  
**Lead:** Divya Payvid (@dpayvid)  
**Status:** ✅ Operational

---

*Last Updated: June 7, 2026*
