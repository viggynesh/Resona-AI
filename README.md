<p align="center">
  <h1 align="center">🧠 Resona AI</h1>
  <p align="center"><strong>Adaptive Memory Reinforcement for Dementia Patients</strong></p>
  <p align="center">
    Clinically-grounded reminiscence therapy powered by AI — personalized, adaptive, and measurable.
  </p>
</p>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#tech-stack">Tech Stack</a> •
  <a href="#setup-instructions">Setup</a> •
  <a href="#how-to-run">How to Run</a> •
  <a href="#project-structure">Structure</a> •
  <a href="#screenshots">Screenshots</a> •
  <a href="#license">License</a>
</p>

---

## Overview

Resona AI delivers personalized reminiscence therapy to dementia patients through an adaptive conversational AI companion. Caregivers build structured memory profiles, patients engage in guided therapy sessions with real-time emotion monitoring, and clinicians get longitudinal cognitive analytics — all in one platform.

---

## Features

### 🏠 Caregiver Portal
- Build structured **memory graphs** across life domains (childhood, family, career, milestones)
- Tag memories by emotional significance and time period
- Flag **sensitive topics** to avoid (deceased loved ones, traumatic events)
- Define **safe anchor memories** for distress de-escalation

### 🗣️ Patient Therapy Sessions
- Conversational AI memory companion guided by the patient's memory graph
- **Real-time emotion detection** via webcam (facial expression classification)
- **Automatic distress pivots** — AI redirects to safe anchor memories when negative emotion is sustained
- **Spaced repetition engine** — memory cues are reintroduced across sessions at increasing intervals
- Voice-based interaction via speech-to-text and text-to-speech

### 📊 Clinician Dashboard
- Per-session emotional response timelines
- Memory domain engagement heatmaps
- Distress event logs with AI pivot analysis
- **Longitudinal cognitive trend tracking** across sessions
- Exportable PDF reports for care planning

---

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | Next.js, Tailwind CSS | UI across all three portal views |
| **Conversational AI** | Claude API (Anthropic) | Memory-grounded therapy conversation engine |
| **Emotion Detection** | face-api.js | Client-side facial expression classification via webcam |
| **Speech-to-Text** | Deepgram | Real-time transcription of patient speech |
| **Text-to-Speech** | ElevenLabs | Natural voice output for the AI companion |
| **Backend** | FastAPI (Python) | Session orchestration, spaced repetition scheduler, analytics |
| **Database** | Supabase (PostgreSQL) | Auth, patient profiles, session logs, memory graphs |

---

## Setup Instructions

### Prerequisites

- **Node.js** >= 18.x
- **Python** >= 3.10
- **pnpm** (or npm/yarn)
- API keys for the following services:
  - [Anthropic (Claude API)](https://console.anthropic.com/)
  - [Deepgram](https://developers.deepgram.com/)
  - [ElevenLabs](https://elevenlabs.io/)
  - [Supabase](https://supabase.com/)

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/resona-ai.git
cd resona-ai
```

### 2. Set Up the Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Create a `.env` file in `/backend`:

```env
ANTHROPIC_API_KEY=your_anthropic_api_key
DEEPGRAM_API_KEY=your_deepgram_api_key
ELEVENLABS_API_KEY=your_elevenlabs_api_key
SUPABASE_URL=your_supabase_project_url
SUPABASE_KEY=your_supabase_anon_key
```

### 3. Set Up the Frontend

```bash
cd ../frontend
pnpm install
```

Create a `.env.local` file in `/frontend`:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### 4. Set Up Supabase

Run the SQL migrations to create the required tables:

```bash
cd ../supabase
# Apply migrations via Supabase CLI or manually in the Supabase SQL editor
supabase db push
```

---

## How to Run

### Start the Backend

```bash
cd backend
source venv/bin/activate
uvicorn main:app --reload --port 8000
```

### Start the Frontend

```bash
cd frontend
pnpm dev
```

The app will be available at **http://localhost:3000**

| Route | Description |
|-------|-------------|
| `/` | Landing page |
| `/caregiver` | Caregiver portal — memory graph builder |
| `/session` | Patient therapy session — voice + webcam |
| `/dashboard` | Clinician analytics dashboard |

---

## Project Structure

```
resona-ai/
├── frontend/
│   ├── app/
│   │   ├── page.tsx                # Landing page
│   │   ├── caregiver/
│   │   │   └── page.tsx            # Memory graph builder
│   │   ├── session/
│   │   │   └── page.tsx            # Patient therapy session
│   │   └── dashboard/
│   │       └── page.tsx            # Clinician analytics
│   ├── components/
│   │   ├── EmotionDetector.tsx     # face-api.js webcam integration
│   │   ├── VoiceInterface.tsx      # Deepgram + ElevenLabs pipeline
│   │   ├── MemoryGraphEditor.tsx   # Caregiver memory input UI
│   │   └── CognitiveChart.tsx      # Recharts-based trend visualizations
│   ├── lib/
│   │   ├── supabase.ts             # Supabase client
│   │   └── api.ts                  # Backend API helpers
│   └── ...
├── backend/
│   ├── main.py                     # FastAPI entrypoint
│   ├── routers/
│   │   ├── sessions.py             # Session CRUD + orchestration
│   │   ├── memory.py               # Memory graph endpoints
│   │   └── analytics.py            # Dashboard data endpoints
│   ├── services/
│   │   ├── claude.py               # Claude API integration + prompt engine
│   │   ├── emotion.py              # Emotion signal processing
│   │   ├── spaced_repetition.py    # SM-2 algorithm implementation
│   │   └── speech.py               # Deepgram + ElevenLabs wrappers
│   ├── models/
│   │   └── schemas.py              # Pydantic models
│   └── requirements.txt
├── supabase/
│   └── migrations/                 # SQL table definitions
└── README.md
```

---

## Screenshots

> *Screenshots will be added after the hackathon demo.*

| View | Description |
|------|-------------|
| **Caregiver Portal** | Memory graph builder with domain tagging and sensitive topic flags |
| **Therapy Session** | Live conversation view with emotion detection overlay |
| **Clinician Dashboard** | Cognitive trend charts and session history timeline |

---

## Environment Variables Reference

| Variable | Location | Description |
|----------|----------|-------------|
| `ANTHROPIC_API_KEY` | Backend | Claude API key for conversation engine |
| `DEEPGRAM_API_KEY` | Backend | Speech-to-text transcription |
| `ELEVENLABS_API_KEY` | Backend | Text-to-speech voice output |
| `SUPABASE_URL` | Both | Supabase project URL |
| `SUPABASE_KEY` | Backend | Supabase service role key |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Frontend | Supabase anonymous key |
| `NEXT_PUBLIC_API_URL` | Frontend | Backend API base URL |

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

<p align="center">
  Built with ❤️ for the Caretech Healthcare x AI Hackathon
</p>
