<div align="center">

# Hi, I'm Mitul Jodhani 👋

### Backend Developer specializing in scalable, event-driven Node.js systems

I design backends the way real production systems are built — async by default, tested,
containerized, and wired into CI/CD from day one. Below are three connected projects that
show that end-to-end: an AI-powered ATS, a multi-seller e-commerce backend, and an
event-driven notification service that the two talk to.

📍 Surat, Gujarat, India · 📧 mituljodhani078@gmail.com

</div>

---

### 🛠️ Tech Stack

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)
![BullMQ](https://img.shields.io/badge/BullMQ-FF6600?style=flat)
![Socket.io](https://img.shields.io/badge/Socket.io-010101?style=flat&logo=socketdotio&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat&logo=nginx&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![Jest](https://img.shields.io/badge/Jest-C21325?style=flat&logo=jest&logoColor=white)

**Languages & Runtime:** JavaScript, Node.js
**Databases & Caching:** MongoDB, Redis
**Messaging & Real-time:** BullMQ, Socket.io
**Cloud & DevOps:** Docker, Nginx, GitHub Actions (CI/CD), Render, AWS S3
**APIs & Auth:** REST, JWT (access/refresh rotation), Zod validation

---

## 🚀 Featured Projects

### 🤖 [ATS — AI-Powered Resume Screening Platform](https://github.com/mitul078/ats-project)
`Node.js` `Express` `MongoDB` `Redis` `BullMQ` `Groq AI` `Docker` `Nginx` `GitHub Actions`

Recruiters post jobs, candidates apply with a resume, and AI does the screening — async,
cached, and retry-safe.

- Async resume-processing pipeline via **BullMQ**, decoupling slow AI calls from the
  request/response cycle, with a job-level status state machine and exponential-backoff retries
- **Groq AI** integration for resume parsing and job-fit scoring, backed by a **two-tier Redis
  cache** (by resume hash, and by resume+job pair) to cut redundant AI calls
- **Horizontally scaled** API and worker as independent Docker images, load-balanced across
  replicas with **Nginx** — verified with live round-robin distribution testing
- Full **CI/CD**: GitHub Actions gates every PR with lint + tests, and publishes versioned
  Docker images to GHCR on merge to `main`
- Deployed to **Render**, benchmarked under concurrent load with **Autocannon**

---

### 🛋️ [Seller Dashboard — Multi-Seller E-Commerce Backend](https://github.com/mitul078/seller-project)
`Node.js` `Express` `MongoDB` `Redis` `BullMQ` `Sharp` `Jest`

A modular-monolith backend for a multi-seller marketplace, built with strict layering so
each domain can be extracted into its own service later.

- **JWT auth with rotating refresh tokens and family-based reuse detection** — a stolen or
  replayed refresh token auto-revokes the entire session family, not just itself
- Signup secured with **bcrypt** hashing and **OTP email verification** queued via BullMQ
- Ownership-scoped product catalog with **cursor-based pagination** and a
  draft → published lifecycle
- Async image pipeline: **Sharp** resizes into three sizes **in parallel**, converts to
  **WebP**, processed off the request cycle via a dedicated BullMQ worker
- **40+ Jest unit tests** across auth and product modules, using mocked dependencies —
  no test database required

---

### 🔔 [Notification Service — Event-Driven, Multi-Channel Delivery](https://github.com/mitul078/notify-project)
`Node.js` `Express` `MongoDB` `Redis` `BullMQ` `Socket.io` `Handlebars` `Nodemailer`

A standalone service other backends call to notify users — in-app and email today,
designed to add channels without touching delivery logic.

- **Event-driven architecture**: producer services (like ATS) publish events over an
  authenticated internal HTTP endpoint; each runs its **own** MongoDB and Redis — no shared
  database between services
- **Real-time in-app delivery** via Socket.io, using the Redis adapter/emitter so the API
  server and the background worker (separate processes) can both reach a connected client
- **Retry-safe by design**: a compound idempotency key on `(event, channel)` plus a
  pre-send status check means a retried BullMQ job can never create or send a duplicate
  notification — proven by deliberately re-publishing the same event and confirming it's
  skipped, not resent
- **Templates stored as data** (Handlebars, in MongoDB) — a new event type is a database
  insert, not a code change
- Per-user, per-event **notification preferences**, with sane defaults for users who've
  never configured any

---

### 🔗 How the projects connect

```
ATS worker scores a resume
        │
        ▼
POST /internal/events  (authenticated, service-to-service)
        │
        ▼
Notification service → resolves preferences → renders template → delivers
                                                     │
                                    ┌────────────────┼────────────────┐
                                    ▼                                 ▼
                            Socket.io (in-app, live)          BullMQ → Nodemailer (email)
```

Two independently deployable services, each with its own database and Redis, talking only
through a defined HTTP contract — the same shape as how real backend teams isolate
services they own from services they don't.

---

### 📫 Let's Connect

[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:mituljodhani078@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/mitul078)

</div>
