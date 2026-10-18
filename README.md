# Autonomous Job Search & Auto-Apply AI Agent

A fully autonomous, **policy-constrained** multi-agent system that searches jobs, personalizes applications, and applies at scale, safely and truthfully.

🏆 **1st Place Solution** of AI Summit 2026 Hackathon

🌐 **Live demo:** https://ai-frontend-nine-vert.vercel.app/


🖥️ **Frontend repo:** https://github.com/Mayank2305Mishra/AI-Frontend


📄 **Project write-up:** [`Fully-Autonomous-Job-Search-Auto-Apply-AI-Agent-for-Students.pdf`](./Fully-Autonomous-Job-Search-Auto-Apply-AI-Agent-for-Students.pdf)



*<img width="1250" height="641" alt="image" src="https://github.com/user-attachments/assets/21193ff7-b063-4031-bed6-ac057282f69a" />*


## The Problem

Applying for internships and jobs is repetitive, slow, and easy to get wrong. Students send the same resume everywhere, skim hundreds of listings, and write cover notes by hand. The obvious fix, "let an LLM do it," creates a new problem: models happily **fabricate** skills, experience, and credentials, and unconstrained automation can spam applications nobody reviewed.


## Our Approach

We built a hands-free job application agent for students where **autonomy is enforced in code, not in prompts**. Every step is grounded in verified evidence about the student, and every automated action passes through hard safety gates.

- Builds a **facts-only artifact pack** from the student's own resume, GitHub, LinkedIn, and portfolio
- **Matches and ranks** relevant jobs using semantic matching and skill-overlap scoring
- Generates **grounded, job-specific personalization**, with no invented credentials
- **Automatically submits** applications inside a sandbox
- **Tracks** successes, failures, and retries

**No fabricated credentials. No uncontrolled automation.**

---

## How It Works

```
 Resume · GitHub · LinkedIn · Portfolio
                  │
                  ▼
      ┌───────────────────────┐
      │  1. Artifact Pack     │   /analyze
      │     Generator         │   single source of truth
      └───────────┬───────────┘
                  ▼
      ┌───────────────────────┐
      │  2. Job Matching &    │   /match-jobs-ai
      │     Ranking           │   semantic match + skill overlap
      └───────────┬───────────┘
                  ▼
      ┌───────────────────────┐
      │  3. Auto-              │   /generate-short-notes-from-queue
      │     Personalization   │   notes grounded in student evidence
      └───────────┬───────────┘
                  ▼
      ┌───────────────────────┐
      │  4. Sandbox           │   /sandbox-apply-batch
      │     Auto-Apply        │   safety gates + outcome tracking
      └───────────────────────┘
```

### Core Components

| # | Component | Endpoint | What it does |
|---|-----------|----------|--------------|
| 1 | **Artifact Pack Generator** | `/analyze` | Ingests resume, GitHub, LinkedIn, and portfolio into a single, facts-only source of truth about the student. |
| 2 | **Job Matching & Ranking** | `/match-jobs-ai` | AI-based semantic matching, skill-overlap scoring, and filtering for jobs that can be safely automated. |
| 3 | **Auto-Personalization** | `/generate-short-notes-from-queue` | Writes short recruiter notes for each job, grounded strictly in the student's evidence. |
| 4 | **Sandbox Auto-Apply** | `/sandbox-apply-batch` | Submits applications autonomously with safety gates, retries, and outcome tracking. |

---

## Safety & Autonomy

Guardrails live in application logic, so the model cannot talk its way past them:

- 🔒 **`automation_allowed` hard gate**: a job is only applied to if it is explicitly marked as automatable
- 📊 **Match-score thresholds**: low-fit jobs are never auto-submitted
- 🧾 **Grounded personalization only**: generated notes may only reference facts present in the artifact pack
- 🔁 **Failure handling & retries**: failed submissions are logged, retried, and surfaced rather than silently dropped

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | FastAPI (Python), Pydantic |
| LLM | Gemini API |
| Agent orchestration | LangChain, LangGraph |
| Job environment | JSON-based job sandbox |
| Frontend | Next.js |
| Deployment | Vercel (frontend), Render (backend) |

---

## Project Structure

```
.
├── backend/        # FastAPI service: agents, matching, personalization, sandbox apply
├── nextjs-app/     # Next.js client
├── Fully-Autonomous-Job-Search-Auto-Apply-AI-Agent-for-Students.pdf
└── README.md
```

---

## Getting Started

### Prerequisites

- Python 3.10+
- Node.js 18+
- A [Gemini API key](https://aistudio.google.com/) (optional)

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Create a .env file
echo "GEMINI_API_KEY=your_key_here" > .env

uvicorn main:app --reload         # replace `main:app` if your entry point differs
```

The API will be available at `http://localhost:8000`, with interactive docs at `http://localhost:8000/docs`.

### Frontend

```bash
cd nextjs-app
npm install
npm run dev
```

Open `http://localhost:3000`.

---

## Example Flow

1. Upload a resume and link GitHub / LinkedIn → `POST /analyze`
2. Get ranked, automatable jobs → `POST /match-jobs-ai`
3. Generate grounded notes for the queue → `POST /generate-short-notes-from-queue`
4. Submit the batch in the sandbox → `POST /sandbox-apply-batch`

---

## Team

Built in the AI Summit 2026 Hackathon by:

| Name | Role |
|------|------|
| **Sourish Kumar Dutta** | Team Lead |
| **Mayank Mishra** | Team Member |
| **Satyaroop Chattopadhyay** | Team Member |

---

## Roadmap

- Move from the JSON sandbox to real job-board integrations, with explicit user consent per platform
- Human-in-the-loop review mode before submission
- Richer evaluation of match quality and personalization faithfulness

---
