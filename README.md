# BrainLoop — AI-Powered Adaptive Learning Platform

A full-stack adaptive learning platform that uses Google Gemini AI to generate
personalized quizzes, diagnose knowledge gaps, and deliver targeted practice
sessions — helping students master any subject faster.

🌐 **Live:** [brainloop-ten.vercel.app](https://brainloop-ten.vercel.app) · **GitHub:** [github.com/mahimagupta-droid/Matrix-3.0---BrainLoop](https://github.com/mahimagupta-droid/Matrix-3.0---BrainLoop)

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS · React 19 |
| AI | Google Gemini (`@google/genai`) |
| Database | MongoDB Atlas (Mongoose) |
| Auth | Clerk |
| Charts | Recharts |
| Deployment | Vercel |

---

## Features

- **AI Quiz Generation** — Enter any topic and get a custom quiz with
  configurable difficulty (easy/medium/hard/mixed) and question count (5–20)
- **Diagnostic Feedback** — Every question includes a learning insight
  explaining *why* the correct answer is right, not just *what* it is
- **Weak-Area Analysis** — Aggregates quiz history to surface weak topics,
  struggling concepts, and accuracy trends over time
- **Targeted Practice** — One-click generation of a quiz focused exclusively
  on your identified weak areas
- **AI Tutor Chat** — In-app conversational AI tutor with context-aware
  responses
- **Progress Dashboard** — Total quizzes taken, average score, current streak,
  and improvement over time
- **Quiz History** — Expandable sessions showing per-question results, your
  answers, correct answers, and diagnostic insights
- **Authentication** — Clerk sign-in/sign-up with protected routes

---

## How It Works

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  1. Choose   │────▶│  2. Attempt  │────▶│  3. Submit   │
│    Topic     │     │   Questions  │     │    & Score   │
└──────────────┘     └──────────────┘     └──────┬───────┘
                                                 │
                     ┌──────────────┐     ┌──────▼───────┐
                     │ 5. Targeted  │◀────│ 4. Weak-Area │
                     │   Practice   │     │   Analysis   │
                     └──────────────┘     └──────────────┘
```

---

## Getting Started

### Prerequisites
- Node.js ≥ 18
- MongoDB Atlas cluster
- Google Gemini API key — [get one here](https://aistudio.google.com/apikey)
- Clerk application

### Setup

```bash
git clone https://github.com/mahimagupta-droid/Matrix-3.0---BrainLoop.git
cd Matrix-3.0---BrainLoop
npm install
```

Create a `.env.local` file:

```env
MONGODB_CONNECTION_URI=mongodb+srv://<user>:<password>@<cluster>.mongodb.net/
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...
GEMINI_API_KEY=AIza...
```

```bash
npm run dev
```

---

## Project Structure

```
src/
├── app/
│   ├── api/
│   │   ├── generate-questions/          # POST — AI quiz generation
│   │   ├── generate-targeted-questions/ # POST — weak-area quiz
│   │   ├── quiz/
│   │   │   ├── submit/                  # POST — save quiz results
│   │   │   ├── history/                 # GET  — fetch quiz history
│   │   │   └── [id]/                    # GET  — single quiz detail
│   │   ├── stats/                       # GET  — user progress stats
│   │   ├── tutor/                       # POST — AI tutor chat
│   │   └── weak-areas/                  # GET  — weak-area analysis
│   ├── dashboard/                       # Progress dashboard page
│   ├── quiz/                            # Quiz taking page
│   ├── weak-areas/                      # Weak areas analysis page
│   ├── layout.tsx                       # Root layout (Clerk, themes, navbar)
│   └── page.tsx                         # Landing page
└── lib/
    ├── components/
    │   ├── TopicSelector.tsx            # Topic + difficulty picker
    │   ├── WeakAreasAnalysis.tsx        # Weak areas dashboard
    │   ├── QuickStats.tsx               # Stats summary cards
    │   ├── aiTutor.tsx                  # AI tutor chat interface
    │   └── navbar.tsx                   # Navigation bar
    ├── models/
    │   ├── quizResults.ts               # Mongoose schema for quiz results
    │   └── chatMessage.ts               # Mongoose schema for tutor chat
    └── dbConnections/
        └── dbConnection.ts              # MongoDB connection singleton
```

---

## Database Models

**QuizResult** — clerkId, topic, difficulty, score, questions array
`{ question, options, correctAnswer, userAnswer, isCorrect, insight }`

**ChatMessage** — clerkId, role (user/assistant), content, timestamp
