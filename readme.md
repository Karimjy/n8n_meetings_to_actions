# Meeting-to-Actions Extractor

**workflow N8N** that converts raw meeting notes or transcripts into structured decisions, action items, and follow-up tasks using n8n, Airtable, and LLMs.

---

## 🎯 Project Overview

This workflow automates post-meeting admin work by:
- Extracting action items with owners and due dates
- Identifying key decisions made during the meeting
- Capturing open questions and risks/blockers
- Saving structured data to Airtable or in database

---


**Tech Stack**:
- **Workflow Engine**: n8n (self-hosted on Render free tier)
- **Database**: Airtable (free tier)
- **AI Model**: OpenRouter / any compatible LLM
- **Hosting**: Render.com

---

## 🛠️ Setup Instructions

### 1. GitHub Repository

Ensure your repo contains:
- `render.yaml` (Render blueprint)
- `Meeting_AI_workflow.json` (n8n workflow export)
- `meetings_eval_set.csv` (eval test set)
- `README.md` (this file)

### 2. Deploy on Render

1. Go to [Render.com](https://render.com) and create an account
2. Click **+ New > Blueprint**
3. Connect your GitHub account and select the repo
4. Click **Deploy Blueprint**

Render will automatically:
- Build the Docker image
- Create the n8n web service
- Start the service with environment variables

### 3. Environment Variables

In Render Dashboard → your service → **Environment** → **Environment Variables**, add:

```env
# n8n Configuration
N8N_HOST=meeting-to-actions-n8n.onrender.com
N8N_PROTOCOL=https
WEBHOOK_URL=[url from render]
N8N_EDITOR_BASE_URL=[url from render]

# Timezone
GENERIC_TIMEZONE=Europe/Paris
TZ=Europe/Paris

# Security (generate random 32-char strings)
N8N_ENCRYPTION_KEY=<32-char-random-string>
N8N_USER_MANAGEMENT_JWT_SECRET=<32-char-random-string>

```

---

## 🧪 Running Evals

### 1. Test Set

The project includes `meetings_eval_set.csv.csv` with 10 realistic meeting examples covering:
- Short and long meetings
- Ambiguous action items
- Missing owners/due dates
- Messy transcripts

---