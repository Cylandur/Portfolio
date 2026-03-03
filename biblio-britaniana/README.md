# Biblio Britaniana

**A production-ready, cloud-deployable digital library management platform.**

> Built to manage a personal collection of 1,000+ ebooks, then generalized into a fully deployable, multi-user cloud application.

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python)
![Flask](https://img.shields.io/badge/Flask-REST%20API-000000?style=flat&logo=flask)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-336791?style=flat&logo=postgresql)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat&logo=docker)

---

## Overview

Biblio Britaniana is a self-hosted digital library platform for readers with large ebook collections. It provides a web-based interface for browsing, searching, reading, and organizing books — with automatic metadata enrichment and cover art fetching baked in.

---

## Features

**Core Platform**
- Multi-format support: EPUB, PDF, MOBI, CBZ/CBR
- Automated indexing — Python-based library scanner that watches for new files
- Metadata enrichment — auto-fetches titles, authors, descriptions, and cover art via Open Library / Google Books
- Full REST API — CRUD operations for books, authors, tags, and shelves
- Multi-user support — accounts, reading progress, personal shelves

**Reading Experience**
- In-browser reader with font size and theme controls
- Annotation and highlight support
- Cross-device reading progress tracking (resume where you left off)

**Deployment**
- One-click cloud deploy — Render, Railway, Heroku, and Fly.io configs included
- Docker-ready — Dockerfile and docker-compose.yml included
- Demo mode — loads sample library data; safe for public-facing deployments
- Environment-based configuration — all secrets via environment variables, no hardcoding

**macOS Desktop App**
- Standalone app bundle — no Python install required on end user's machine
- Menu bar integration for quick library access
- Local-first option: full functionality with no cloud dependency

---

## Architecture

```
biblio-britaniana/
├── app/
│   ├── api/            # REST API endpoints
│   ├── models/         # SQLAlchemy models (Book, Author, User, Shelf)
│   ├── indexer/        # File watcher + metadata enrichment pipeline
│   ├── reader/         # In-browser reading engine
│   └── templates/      # Jinja2 UI templates
├── migrations/         # Alembic database migrations
├── Dockerfile
├── docker-compose.yml
├── render.yaml         # One-click Render deployment config
├── railway.json        # Railway deployment config
└── requirements.txt
```

---

## Quick Start

**Docker (recommended)**
```bash
git clone https://github.com/shaunreiland/biblio-britaniana
cd biblio-britaniana
docker-compose up -d
# Visit http://localhost:5000
```

**Local Development**
```bash
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
flask db upgrade
flask run
```

**Demo Mode**
```bash
export DEMO_MODE=true
flask run
# Loads with a sample library — no real files needed
```

---

## Environment Variables

| Variable | Description | Required |
|---|---|---|
| `DATABASE_URL` | PostgreSQL connection string | Yes (production) |
| `SECRET_KEY` | Flask session secret | Yes |
| `LIBRARY_PATH` | Path to ebook directory (local deploy) | Local only |
| `DEMO_MODE` | Set to `true` to load sample data | No |
| `COVER_API_KEY` | Open Library / Google Books API key | No (enhances covers) |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3.11+, Flask, SQLAlchemy, Alembic |
| Database | PostgreSQL (production), SQLite (dev / demo) |
| Frontend | Jinja2, vanilla JavaScript, CSS Grid |
| Indexer | Watchdog, ebooklib, PyMuPDF |
| Deployment | Docker, Gunicorn, Render / Railway / Fly.io |

---

## Status

- Fully functional core platform
- Demo mode available
- Cloud deployment configurations tested
- macOS desktop bundle available
