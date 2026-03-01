# 🤖 Job Application Automator

<div align="center">

![Job Automation Banner](https://img.shields.io/badge/Built%20with-n8n-FF6D5A?style=for-the-badge&logo=n8n)
![AI Powered](https://img.shields.io/badge/AI%20Powered-Groq%20LLaMA-00A67E?style=for-the-badge&logo=meta)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=for-the-badge&logo=google-sheets&logoColor=white)
![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=for-the-badge&logo=gmail&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

**Stop spending hours on job hunting. Let AI do it while you sleep. 🚀**

[Features](#-features) • [How It Works](#-how-it-works) • [Tech Stack](#-tech-stack) • [Setup](#-setup-guide) • [Workflow](#-workflow-architecture) • [Demo](#-output-example)

</div>

---

## 🎯 What Is This?

> *"Job hunting is exhausting. So I automated it."*

**Job Application Automator** is a fully automated n8n workflow that wakes up every morning at 9 AM, scrapes 15 fresh job postings from Indeed, uses AI to analyze each job against your resume, generates personalized cover letters and tailored resume summaries — then emails you a complete Excel report. All while you sleep. 😴

### ⏱️ Time Saved
| Task | Manual | Automated |
|------|--------|-----------|
| Job searching | 1-2 hours | 0 minutes |
| Reading job descriptions | 30-60 mins | 0 minutes |
| Writing cover letters | 1-2 hours | 0 minutes |
| Tailoring resume | 30-60 mins | 0 minutes |
| **Total Daily** | **3-4 hours** | **~3 minutes** |

---

## ✨ Features

- 🔍 **Auto Job Scraping** — Fetches 15 fresh jobs from Indeed every morning
- 🧠 **AI Resume Matching** — Scores each job 0–100 based on your actual resume
- 📊 **Skills Gap Analysis** — Identifies exactly what skills you have vs. what's needed
- ✉️ **Cover Letter Generator** — Writes a personalized 3-paragraph cover letter per job
- 📄 **Resume Tailoring** — Rewrites your resume summary for each specific role
- 📧 **Daily Email Report** — Sends one email with everything as an Excel attachment
- 🗂️ **Google Sheets Tracking** — Auto-saves all jobs with analysis for easy review
- 🔄 **Daily Auto-Clear** — Resets the sheet every night ready for fresh jobs tomorrow
- 💰 **100% Free** — Built entirely on free tiers of all services

---

## 🏗️ How It Works

```
⏰ 9:00 AM Every Day
       │
       ▼
📄 Download Resume PDF (Google Drive)
       │
       ▼
🔍 Scrape 15 Jobs (Indeed via RapidAPI)
       │
       ▼
🔀 Split into 15 Individual Jobs
       │
       ▼
┌──────────────────────────────────────┐
│  For Each Job (×15):                 │
│                                      │
│  🤖 AI Agent 1 — Analysis            │
│     → Match Score (0-100)            │
│     → Required Skills                │
│     → Missing Skills                 │
│     → Job Analysis                   │
│                                      │
│  🤖 AI Agent 2 — Cover Letter        │
│     → Personalized 3-paragraph       │
│       cover letter                   │
│                                      │
│  🤖 AI Agent 3 — Resume Tailoring    │
│     → Job-specific resume summary    │
└──────────────────────────────────────┘
       │
       ▼
💾 Save All to Google Sheets
       │
       ▼
📧 Email Excel Report to You
       │
       ▼
🧹 Clear Sheet for Tomorrow
```

---

## 🛠️ Tech Stack

| Tool | Purpose | Cost |
|------|---------|------|
| **n8n** (Self-Hosted) | Workflow automation engine | Free |
| **Groq API** (LLaMA 3.1 8B) | AI analysis, cover letters, resume | Free tier |
| **RapidAPI** (Indeed Scraper) | Job data scraping | Free tier |
| **Google Drive** | Resume PDF storage | Free |
| **Google Sheets** | Job tracking database | Free |
| **Gmail API** | Daily email delivery | Free |

---

## 📋 Workflow Architecture

```
Node 1  → Schedule Trigger         (9 AM daily)
Node 2  → Google Drive             (download resume PDF)
Node 3  → Extract from File        (parse PDF to text)
Node 4  → HTTP Request             (scrape 15 jobs from Indeed)
Node 5  → Split Out                (split into individual jobs)
Node 6  → Edit Fields 1st          (extract job fields)
Node 7  → AI Agent (Analysis)      (score + skills analysis)
Node 8  → Edit Fields 2nd          (parse AI response)
Node 9  → AI Agent (Cover Letter)  (generate cover letter)
Node 10 → Edit Fields 3rd          (extract cover letter)
Node 11 → AI Agent (Resume)        (tailor resume summary)
Node 12 → Edit Fields 4th          (assemble final data)
Node 13 → Google Sheets Write      (save all 15 jobs)
Node 14 → Aggregate                (combine into 1 item)
Node 15 → Google Drive Download    (export as xlsx)
Node 16 → Gmail                    (send report email)
Node 17 → Google Sheets Clear      (reset for tomorrow)
```

---

## 📊 AI Scoring System

Each job is scored using a **weighted matching algorithm**:

```
┌─────────────────────────┬────────┐
│ Category                │ Weight │
├─────────────────────────┼────────┤
│ Skills & Tools Match    │  40%   │
│ Experience Depth        │  25%   │
│ Responsibilities Match  │  15%   │
│ Education               │  15%   │
│ Logistics (location)    │   5%   │
└─────────────────────────┴────────┘
```

**Score Guide:**
- 🟢 **80-100** — Excellent match, apply immediately
- 🟡 **60-79** — Good match, worth applying
- 🔴 **Below 60** — Skill gap, consider skipping

---

## 📁 Google Sheet Output

Every job is saved with these columns:

| Column | Description |
|--------|-------------|
| `Job_Title` | Position name |
| `Company` | Company name |
| `Job_URL` | Direct link to apply |
| `Match_Score` | AI score 0-100 |
| `Required_Skills` | Skills the job needs |
| `Missing_Skills` | Skills you lack |
| `Tailored_Resume` | Job-specific resume summary |
| `Cover_Letter` | Ready-to-use cover letter |
| `Applied_Date` | Date analyzed |
| `Status` | To Review / Applied / Interview |
| `Analysis` | Detailed AI notes |

---

## 🔧 Setup Guide

### Prerequisites
- Node.js installed
- n8n running locally (`npx n8n`)
- Google account
- Groq API key (free)
- RapidAPI key (free)

---

### Step 1: Install n8n
```bash
npx n8n
```
Open: `http://localhost:5678`

---

### Step 2: Get API Keys

#### Groq API (AI Engine) — Free
1. Go to [console.groq.com](https://console.groq.com)
2. Sign up → API Keys → Create Key
3. Copy key starting with `gsk_...`

#### RapidAPI Indeed Scraper — Free Tier
1. Go to [rapidapi.com](https://rapidapi.com)
2. Search: `indeed-scraper-api`
3. Subscribe to free tier
4. Copy your API key

#### Google APIs (Drive + Sheets + Gmail)
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create project: `n8n-job-automation`
3. Enable these APIs:
   - Google Drive API
   - Google Sheets API
   - Gmail API
4. Create OAuth2 credentials
5. Add redirect URI: `http://localhost:5678/rest/oauth2-credential/callback`
6. Add yourself as test user in OAuth consent screen

---

### Step 3: Set Up Google Sheet

Create a Google Sheet named **"Job Applications Tracker"** with these headers in Row 1:

```
Job_Title | Company | Job_URL | Match_Score | Required_Skills | Missing_Skills | Tailored_Resume | Cover_Letter | Applied_Date | Status | Analysis
```

---

### Step 4: Upload Your Resume

Upload your resume PDF to Google Drive and name it `Master_Resume.pdf`

---

### Step 5: Import the Workflow

1. Open n8n
2. Click **"Import from file"**
3. Import the workflow JSON
4. Connect your credentials to each node
5. Update the Indeed scraper query with your job title

---

### Step 6: Configure AI Prompts

In each AI Agent node, the prompts reference your resume via:
```
{{ $('Extract from File').item.json.text }}
```

This automatically uses your actual resume PDF — no hardcoding needed!

---

### Step 7: Activate

1. Click **"Save"**
2. Toggle workflow from **Inactive → Active**
3. It will run automatically every morning at 9 AM! ✅

---

## 📧 Daily Email Example

Every morning you'll receive:

```
Subject: Daily Jobs Report - 01/03/2026

Hi Umair,

Please find today's job analysis report attached!

📎 Job_Applications_Report_01032026.xlsx
```

Open the Excel file, sort by **Match_Score** descending, and start applying to the top matches with your ready-made cover letters!

---

## 🐛 Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| `Rate limit exceeded` | Too many Groq requests/min | Add Wait node (3s) before each AI Agent |
| `403 Forbidden (Google)` | API not enabled | Enable API in Google Cloud Console |
| `URL parameter undefined` | Wrong field name | Check field name in previous node output |
| `210 items instead of 15` | Old Sheets node connected | Disconnect Google Sheets Read node |
| `Binary file not found` | Gmail attachment issue | Add Aggregate node before Gmail |
| `JSON parse error` | AI returned bad JSON | Check AI Agent prompt format |

---

## 🚀 Future Roadmap

- [ ] LinkedIn job scraping support
- [ ] Telegram/WhatsApp notifications
- [ ] Multi-city job search
- [ ] Salary filter (exclude low-paying jobs)
- [ ] Auto-apply for Easy Apply jobs
- [ ] Interview scheduler integration
- [ ] Application success rate dashboard
- [ ] Skills learning plan generator

---

## 📁 Project Structure

```
job-application-automator/
│
├── workflow/
│   └── Job_Application_Automator.json    # n8n workflow export
│
├── docs/
│   └── Job_Application_Automator_Documentation.docx
│
├── assets/
│   └── workflow_screenshot.png
│
└── README.md
```

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

---

## 📄 License

This project is licensed under the MIT License.

---

## 👤 Author

**Umair Elahi**

- 📧 Email: [uelahi502@gmail.com](mailto:uelahi502@gmail.com)
- 💼 LinkedIn: [linkedin.com/in/umair-elahi-972b65250](https://linkedin.com/in/umair-elahi-972b65250)
- 🐙 GitHub: [github.com/Umairelahi](https://github.com/Umairelahi)

---

<div align="center">

**⭐ If this project helped you, give it a star!**

*Built with ❤️ by Umair Elahi — AI Engineer*

</div>