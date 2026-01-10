# AppFaktoryWebsite - Project Guide

**Master Guide**: [../AppFaktory/CLAUDE.md](../AppFaktory/CLAUDE.md) for ecosystem rules, CI/CD patterns, and architecture.

---

## Overview

**Purpose**: Marketing landing page for EasyAgent / AppFaktory
**URL**: https://easyagent.app-faktory.com
**Stack**: Static HTML/CSS/JS, nginx (Docker container)
**Port**: 3003 (via Caddy reverse proxy)

---

## Structure

```
AppFaktoryWebsite/
├── index.html           # Landing page
├── styles.css           # Tailwind-style CSS
├── script.js            # Minimal JS (animations, interactions)
├── assets/              # Images, icons
├── Dockerfile           # nginx-based container
├── nginx.conf           # nginx configuration
└── .github/workflows/
    └── deploy-website.yml  # CI/CD to DigitalOcean
```

---

## Deployment

This repo follows the standard CI/CD pattern defined in the master CLAUDE.md:

1. Push to `main` triggers GitHub Actions
2. Build Docker image → Push to GHCR
3. SSH deploy to DigitalOcean
4. Container runs on port 3003

**Workflow**: `.github/workflows/deploy-website.yml`
**Image**: `ghcr.io/programthat715/appfaktory-website:latest`
**Container**: `appfaktory-website`

---

## Local Development

```bash
# Preview with any static server
npx serve .

# Or with Python
python -m http.server 8080

# Build Docker image locally
docker build -t appfaktory-website .
docker run -p 3003:80 appfaktory-website
```

---

## Health Check

The nginx container serves `/health` endpoint returning "OK":

```bash
curl https://easyagent.app-faktory.com/health
# Returns: OK
```

---

## Rules

**DO**: Keep it simple, optimize images, use semantic HTML, test on mobile
**DON'T**: Add JavaScript frameworks, include tracking without consent, break mobile layout

---

## Domain Notes

- `easyagent.app-faktory.com` → This landing page (DigitalOcean)
- `app-faktory.com` → Redirects to easyagent.app-faktory.com (Caddy)
- `www.app-faktory.com` → Hosted by Wix (not managed here)

---

**See also**: Master guide at [../AppFaktory/CLAUDE.md](../AppFaktory/CLAUDE.md)
