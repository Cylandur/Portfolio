# Job Hunter Dashboard

**AI-powered job search platform — live listings, tailored resumes, and ATS scoring in one click.**

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python)
![Flask](https://img.shields.io/badge/Flask-Backend-000000?style=flat&logo=flask)
![Claude AI](https://img.shields.io/badge/Claude_AI-Powered-D97757?style=flat)
![Dice](https://img.shields.io/badge/Dice.com-Job%20Listings-FF6B35?style=flat)

---

## Overview

Job Hunter is a self-hostable job search dashboard that aggregates live Dice.com listings and uses the Anthropic Claude API to generate fully tailored application materials — resume, cover letter, and ATS analysis — matched to each individual job description.

Stop sending generic resumes. Job Hunter reads the posting and writes materials that speak directly to it.

---

## Features

**Job Search**
- Live Dice.com listing proxy with real-time search and keyword filtering
- Full job details panel: description, requirements, salary, company info
- Bookmarking and application status tracking

**AI-Generated Application Materials**
- One-click tailored resume generation, matched to the job description
- Cover letter writing tuned to company culture and role tone
- ATS compatibility scoring with specific keyword gap analysis and fix recommendations
- Exportable PDF output for each complete application package

**Deployment**
- Demo mode with mock job listings — safe for public-facing deployment
- Environment-based API key configuration — no hardcoded secrets
- One-click PaaS deploy: Render, Railway, Heroku, or Fly.io
- Full engineering rebuild prompt included for reproducible AI-assisted redevelopment

---

## Quick Start

**Local**
```bash
git clone https://github.com/shaunreiland/job-hunter
cd job-hunter
pip install -r requirements.txt
export ANTHROPIC_API_KEY=your_key_here
export DEMO_MODE=false
flask run
# Visit http://localhost:5000
```

**Docker**
```bash
docker-compose up -d
```

**Demo Mode** (no API keys needed)
```bash
export DEMO_MODE=true
flask run
# Runs with mock job listings and sample AI outputs
```

---

## Environment Variables

| Variable | Description | Required |
|---|---|---|
| `ANTHROPIC_API_KEY` | Your Anthropic API key | Yes (live mode) |
| `DICE_API_KEY` | Dice.com API key | No (scraper fallback included) |
| `DEMO_MODE` | `true` for mock data, `false` for live | No |
| `SECRET_KEY` | Flask session secret | Yes |
| `DATABASE_URL` | PostgreSQL URL (for application tracking) | No (SQLite default) |

---

## Architecture

```
job-hunter/
├── app/
│   ├── api/             # Dice proxy + Anthropic Claude endpoints
│   ├── models/          # Job, Application, User models
│   ├── ai/              # Resume, cover letter, ATS prompt templates
│   └── templates/       # Dashboard UI (HTML/CSS/JS)
├── demo/                # Mock job data for demo mode
├── Dockerfile
├── docker-compose.yml
├── render.yaml
├── railway.json
└── requirements.txt
```

---

## How the AI Generation Works

Each application package is generated in three sequential Claude API calls:

1. **Resume tailoring** — Claude reads your base resume and the job description, then rewrites and reorders sections to maximize relevance and keyword alignment.
2. **Cover letter** — Claude analyzes the company and role tone, then writes a cover letter that mirrors the job posting's language and priorities.
3. **ATS scoring** — Claude compares the generated resume against the job description and returns a match score with specific gaps identified and rewrite suggestions.

All prompts are stored in `app/ai/` and are fully editable.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3.11+, Flask |
| AI | Anthropic Claude API |
| Job Data | Dice.com API / scraper proxy |
| Frontend | HTML, CSS, vanilla JavaScript |
| PDF Export | WeasyPrint |
| Deployment | Docker, Gunicorn, Render / Railway |
