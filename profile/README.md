<div align="center">

<img src="https://img.shields.io/badge/ExamGuard-AI-2563EB?style=for-the-badge&logo=shield&logoColor=white" alt="ExamGuard AI" height="40"/>

# ExamGuard AI

### Intelligent Assessment Platform with RAG-Powered Question Generation & Multi-Agent Cheating Detection

[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/Status-In%20Development-F59E0B?style=flat-square)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-22C55E?style=flat-square)](CONTRIBUTING.md)
[![Made with Love](https://img.shields.io/badge/Made%20with-❤️-DC2626?style=flat-square)]()

> **Smarter Exams. Honest Results.**
>
> ExamGuard AI is a dual-purpose academic platform that automatically generates high-quality, discipline-specific exam questions from course materials using RAG, and monitors exam integrity through privacy-conscious multi-agent proctoring that analyzes behavior patterns — reducing false positive rates from the industry standard of 71% to under 5%.

[Features](#-features) · [Tech Stack](#-tech-stack) · [Architecture](#-architecture) · [Repositories](#-repositories) · [Team](#-team) · [Getting Started](#-getting-started)

</div>

---

## 🎯 The Problem

Online education faces a dual crisis:

- **Professors** spend **10–15 hours** creating each exam while struggling to generate high-quality, varied questions
- **68%** of students admit to cheating on online exams
- Existing proctoring tools (e.g., Proctorio) have a **71% false positive rate**, causing student anxiety and unfair accusations

---

## 💡 The Solution

ExamGuard AI addresses both sides of the problem simultaneously:

1. **AI Exam Generation** — Upload course materials (PDFs, slides, syllabi) and let the RAG pipeline generate 50 exam questions across 4 cognitive levels in minutes
2. **Multi-Agent Proctoring** — Real-time behavioral monitoring with probabilistic reasoning that is bias-aware, explainable, and always human-reviewed before any action is taken

---

## ✨ Features

### 👨‍🏫 For Professors

- **RAG-Powered Question Generation** — Upload any course material and get exam-ready questions instantly, mapped to Bloom's Taxonomy cognitive levels (Recall 20% / Application 30% / Analysis 30% / Synthesis 20%)
- **AI Exam Builder** — Drag-and-drop question editor with cognitive level distribution visualization, difficulty tuning, and question bank management
- **Live Proctoring Monitor** — Real-time dashboard showing all active students, integrity scores, and a live alert feed for flagged events
- **Incident Review System** — Timestamped event timeline, student rebuttal panel, and one-click escalation workflow
- **Results & Analytics** — Score distributions, per-student integrity breakdowns, and exportable reports
- **Course & Material Management** — Organize uploads by course, semester, and subject for reusable question banks

### 👨‍🎓 For Students

- **Distraction-Free Exam Mode** — Fullscreen-enforced, focused exam interface with real-time timer
- **System Pre-Check** — Camera, microphone, and fullscreen verification before every exam session
- **Transparent Integrity Reports** — If flagged, students receive a full explainable report with the exact event, timestamp, and confidence score
- **Rebuttal Submission** — Students can submit contextual explanations (e.g., accommodation needs) before a professor reviews any incident
- **Exam History & Results** — Full history of past exams, scores, and integrity statuses

### 🛡️ For Administrators

- **Platform-Wide Oversight** — Manage all professors, students, exams, and escalated violations from a single admin console
- **Bias Audit Reports** — Demographic and accessibility accuracy reports to ensure equitable treatment across all student populations
- **System Health Monitoring** — Real-time logs, agent performance metrics, and uptime tracking
- **Sensitivity Configuration** — Institution-wide proctoring threshold controls (Strict / Balanced / Lenient)

### 🤖 AI & Proctoring Agents

| Agent | Role | Technology |
|---|---|---|
| **Content Analyzer** | Extracts key concepts from uploaded materials | Gemini Pro + LangChain.js |
| **Question Generator** | Creates questions with plausible distractors | Gemini Pro + RAG |
| **Gaze Pattern Agent** | Detects sustained off-screen gaze (>15s) | TensorFlow.js + MediaPipe |
| **Audio Anomaly Agent** | Identifies multiple speakers / conversation | Web Audio API |
| **Tab Monitor Agent** | Catches focus loss and app switches | Visibility API |
| **Coordinator Agent** | Synthesizes all signals into an integrity score (0–100) | LangChain.js |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT (Browser)                          │
│                                                                  │
│   React 19 + TypeScript + Vite                                  │
│   ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐ │
│   │  Exam Builder│  │  Exam Taking │  │  Live Monitor        │ │
│   │  (Professor) │  │  (Student)   │  │  (Professor)         │ │
│   └──────────────┘  └──────┬───────┘  └──────────────────────┘ │
│                             │                                    │
│   ┌─────────────────────────▼──────────────────────────────┐   │
│   │              Proctoring Agents (In-Browser)            │   │
│   │  TensorFlow.js (Gaze) · Web Audio API · Visibility API │   │
│   └─────────────────────────┬──────────────────────────────┘   │
└─────────────────────────────┼───────────────────────────────────┘
                              │ REST + WebSocket (Socket.io)
┌─────────────────────────────▼───────────────────────────────────┐
│                        SERVER (NestJS)                           │
│                                                                  │
│   ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐ │
│   │  Auth Module │  │  Exam Module │  │  Proctoring Module   │ │
│   │  (JWT/Guards)│  │  (CRUD+AI)   │  │  (Events+Scoring)    │ │
│   └──────────────┘  └──────┬───────┘  └──────────────────────┘ │
│                             │                                    │
│   ┌─────────────────────────▼──────────────────────────────┐   │
│   │              AI Orchestration (LangChain.js)           │   │
│   │         Gemini Pro 3 · Multi-Agent Pipeline · RAG      │   │
│   └─────────────────────────┬──────────────────────────────┘   │
└─────────────────────────────┼───────────────────────────────────┘
                              │
┌─────────────────────────────▼───────────────────────────────────┐
│                          DATA LAYER                              │
│                                                                  │
│   MongoDB (Documents)  ·  ChromaDB (Vectors)  ·  Redis (Cache)  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| React | 19 | Core UI framework |
| TypeScript | 5.x | Type safety |
| Vite | 5.x | Build tool & dev server |
| React Router | v6 | Client-side routing |
| TanStack Query | v5 | Server state & caching |
| React Hook Form | v7 | Performant form management |
| Zod | v3 | Schema validation |
| Axios | v1 | HTTP client |
| Zustand | v4 | Global client state (exam session) |
| shadcn/ui | latest | Component primitives (Radix UI) |
| Tailwind CSS | v3 | Utility-first styling |
| React Hot Toast | v2 | Toast notifications |
| TanStack Table | v8 | Headless data tables |
| Recharts | v2 | Analytics & score charts |
| React Webcam | latest | Camera feed for proctoring |
| TensorFlow.js | v4 | In-browser gaze detection |
| MediaPipe | latest | Face landmark detection |
| Screenfull | v6 | Fullscreen enforcement |
| React Dropzone | v14 | File upload (course materials) |
| date-fns | v3 | Date formatting & exam timers |

### Backend
| Technology | Version | Purpose |
|---|---|---|
| NestJS | v10 | Server framework (modular, TypeScript-first) |
| Node.js | v20 LTS | Runtime |
| Socket.io | v4 | Real-time proctoring event streaming |
| LangChain.js | latest | Multi-agent AI orchestration |
| Google Gemini Pro | 3 | LLM for question generation & coordination |
| Passport.js | latest | Authentication strategies |
| JWT | — | Stateless auth tokens |
| class-validator | latest | DTO validation |
| Multer | latest | File upload handling |

### Databases
| Technology | Purpose |
|---|---|
| MongoDB | Users, exams, questions, responses, incidents |
| ChromaDB | Vector store for RAG knowledge bases |
| Redis | Session storage, job queues, real-time caching |

### DevOps & Tooling
| Technology | Purpose |
|---|---|
| pnpm | Fast, efficient package management |
| ESLint + Prettier | Code quality & formatting |
| Husky + lint-staged | Pre-commit hooks |
| Docker + Docker Compose | Containerized local development |
| GitHub Actions | CI/CD pipeline |
| Conventional Commits | Standardized commit messages |

---

## 📁 Repositories

This GitHub organization contains the following repositories:

| Repository | Description | Status |
|---|---|---|
| [`examguard-frontend`](.) | React 19 + Vite client application | 🚧 In Development |
| [`examguard-backend`](.) | NestJS REST API & WebSocket server | 🚧 In Development |
| [`examguard-ai`](.) | LangChain.js agents & RAG pipeline | 📋 Planned |
| [`examguard-docs`](.) | Architecture docs & API reference | 📋 Planned |

---

## 📄 Pages & Routes

The platform covers **39 screens** across 4 user contexts:

<details>
<summary><strong>🔓 Public / Auth (6 pages)</strong></summary>

| Page | Route |
|---|---|
| Landing / Marketing | `/` |
| Login | `/login` |
| Register | `/register` |
| Forgot Password | `/forgot-password` |
| Reset Password | `/reset-password/:token` |
| Email Verification | `/verify-email/:token` |

</details>

<details>
<summary><strong>👨‍🏫 Professor (13 pages)</strong></summary>

| Page | Route |
|---|---|
| Dashboard | `/professor/dashboard` |
| Exam List | `/professor/exams` |
| Create Exam — Upload Materials | `/professor/exams/create/upload` |
| Create Exam — AI Generation | `/professor/exams/create/generate` |
| Create Exam — Review & Configure | `/professor/exams/create/review` |
| Exam Detail / Edit | `/professor/exams/:examId` |
| Question Bank | `/professor/question-bank` |
| Live Proctoring Monitor | `/professor/exams/:examId/monitor` |
| Exam Results & Analytics | `/professor/exams/:examId/results` |
| Flag / Incident Review | `/professor/exams/:examId/flags/:studentId` |
| Student Management | `/professor/students` |
| Course Management | `/professor/courses` |
| Settings | `/professor/settings` |

</details>

<details>
<summary><strong>👨‍🎓 Student (11 pages)</strong></summary>

| Page | Route |
|---|---|
| Dashboard | `/student/dashboard` |
| Upcoming Exams | `/student/exams` |
| Exam Lobby | `/student/exams/:examId/lobby` |
| System Check | `/student/exams/:examId/system-check` |
| Exam Taking (fullscreen) | `/student/exams/:examId/take` |
| Exam Submitted | `/student/exams/:examId/submitted` |
| My Results | `/student/results` |
| Result Detail | `/student/results/:examId` |
| Integrity Reports | `/student/flags` |
| Submit Rebuttal | `/student/flags/:flagId/rebuttal` |
| Profile & Settings | `/student/settings` |

</details>

<details>
<summary><strong>🛡️ Admin (6 pages)</strong></summary>

| Page | Route |
|---|---|
| Admin Dashboard | `/admin/dashboard` |
| User Management | `/admin/users` |
| All Exams Overview | `/admin/exams` |
| Escalated Violations | `/admin/violations` |
| System Health / Logs | `/admin/system` |
| Bias Audit Reports | `/admin/bias-audit` |

</details>

<details>
<summary><strong>⚠️ Utility (3 pages)</strong></summary>

| Page | Route |
|---|---|
| 404 Not Found | `*` |
| 403 Unauthorized | `/403` |
| Maintenance | `/maintenance` |

</details>

---

## 🚀 Getting Started

### Prerequisites

- Node.js v20 LTS
- pnpm v9+
- Docker & Docker Compose
- MongoDB, Redis (or use the provided `docker-compose.yml`)

### Clone the Organization Repos

```bash
# Frontend
git clone https://github.com/examguard-ai/examguard-frontend.git

# Backend
git clone https://github.com/examguard-ai/examguard-backend.git
```

### Start with Docker (Recommended)

```bash
# From the root of any repo
docker-compose up -d
```

### Manual Setup — Frontend

```bash
cd examguard-frontend
pnpm install
cp .env.example .env.local
pnpm dev
```

### Manual Setup — Backend

```bash
cd examguard-backend
pnpm install
cp .env.example .env
pnpm start:dev
```

### Environment Variables

```bash
# Frontend (.env.local)
VITE_API_URL=http://localhost:3000
VITE_WS_URL=ws://localhost:3000
VITE_APP_ENV=development

# Backend (.env)
PORT=3000
MONGODB_URI=mongodb://localhost:27017/examguard
REDIS_URL=redis://localhost:6379
CHROMA_URL=http://localhost:8000
JWT_SECRET=your-secret-here
JWT_EXPIRES_IN=7d
GEMINI_API_KEY=your-gemini-key-here
```

---

## 👥 Team

| Name | Role | GitHub |
|---|---|---|
| **Mahmoud Abdelhalim Ahmed Isa** | Team Lead & Full-Stack | [@mahmoud-isa](https://github.com) |
| **Mahmoud Ismael Mohamed Elfiky** | Backend & AI Pipeline | [@mahmoud-elfiky](https://github.com) |
| **Mohamed Fouad Mohamed Nassar** | Frontend & UI/UX | [@mohamed-nassar](https://github.com) |
| **Mostafa Safwat Mohamed Soliman** | Proctoring Agents & ML | [@mostafa-safwat](https://github.com) |
| **Amir Ahmed Said Soliman** | DevOps & Database | [@amir-soliman](https://github.com) |

---

## 🗺️ Roadmap

- [x] Project planning & architecture design
- [x] UI/UX design system (Stitch + shadcn/ui)
- [ ] Frontend scaffolding (React 19 + Vite + TypeScript)
- [ ] Auth module (NestJS + JWT + Passport)
- [ ] Exam CRUD & builder (Frontend + Backend)
- [ ] RAG pipeline (ChromaDB + LangChain.js + Gemini)
- [ ] AI question generation agents
- [ ] In-browser proctoring agents (TensorFlow.js + MediaPipe)
- [ ] Real-time WebSocket proctoring monitor (Socket.io)
- [ ] Integrity scoring & incident reporting
- [ ] Student rebuttal system
- [ ] Analytics & reporting dashboard
- [ ] Bias audit & accessibility testing (100-student validation study)
- [ ] Production deployment

---

## ⚠️ Ethical Commitments

ExamGuard AI is built with fairness and transparency as first-class requirements:

- **No Punitive Automation** — The AI never makes punitive decisions. All flags are reviewed by a human professor before any action is taken
- **Personalized Baselines** — Each student's behavior is calibrated individually during the first 5 minutes of an exam, not compared to a global average
- **Explainable Flags** — Every flagged incident includes the exact timestamp, event type, and confidence score, written in plain language
- **Rebuttal System** — Students always have the opportunity to submit context before a professor reviews any incident
- **Bias Auditing** — Continuous demographic and accessibility stress tests on all ML models to ensure equitable accuracy across diverse student populations
- **Disability Accommodations** — Professors can disable specific proctoring signals (e.g., gaze tracking) for students with documented accessibility needs

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

Built with ❤️ by the ExamGuard AI Team · Faculty of Computer Science · 2025

</div>
