<div align="center">

# 🏛️ Smart Campus Operations Hub

**A unified platform for students, faculty, and administrators to manage campus life.**

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.0.4-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-19.2.4-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&logo=docker&logoColor=white)](https://docs.docker.com/)
[![Java](https://img.shields.io/badge/Java-21-ED8B00?style=flat-square&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![License](https://img.shields.io/badge/Status-Active%20Development-brightgreen?style=flat-square)]()

[Features](#-features) · [Tech Stack](#-tech-stack) · [Quick Start](#-quick-start) · [API Docs](#-api-documentation) · [Team](#-team)

</div>

---

## Overview

Smart Campus Operations Hub is a full-stack web application that streamlines campus operations — from facility bookings and timetables to support tickets and real-time notifications — all in one place.

| Role | Capabilities |
|------|-------------|
| 🎓 **Students** | Book facilities, view timetables, submit appeals, receive notifications |
| 👩‍🏫 **Faculty** | Manage schedules, allocate resources |
| 🛡️ **Admins** | Approve requests, oversee operations, generate analytics |

---

## ✨ Features

| Category | Highlights |
|----------|-----------|
| 🔐 **Auth & Security** | Google/Microsoft SSO (OAuth 2.0), OTP 2FA, JWT, RBAC |
| 📅 **Facility Booking** | Slot management, conflict prevention, admin approval workflow |
| 📊 **Timetable Engine** | Conflict detection, real-time updates, calendar view |
| 🎫 **Ticket System** | Issue reporting, priority queue, automated status notifications |
| 🔔 **Notifications** | Real-time in-app + email alerts with custom preferences |
| 🎯 **Attendance** | QR code check-in, geofencing, automatic attendance recording |
| 📈 **Analytics** | Usage dashboards, facility utilization reports, data export |
| 📝 **Appeals** | Suspension appeal submission, admin review, decision history |
| 📁 **File Management** | Upload/download, auto-generated thumbnails, access control |

---

## 🛠 Tech Stack

### Backend
- **Spring Boot 4.0.4** · Java 21 · Maven
- **Spring Security** · JWT (JJWT 0.11.5) · OAuth 2.0
- **Spring Data JPA** · Hibernate · PostgreSQL 15
- **Springdoc OpenAPI** · Spring Mail

### Frontend
- **React 19.2.4** · Vite 8.0.1 · Tailwind CSS 4.2.2
- **Axios** · React Router DOM 7.9.6 · @react-oauth/google
- **qrcode.react** · react-toastify · jsPDF · html2canvas

### Infrastructure
- **Docker & Docker Compose** · PostgreSQL (named volumes) · MailDev

---

## 🚀 Quick Start

> **Recommended**: Docker setup gets everything running in one command.

### Prerequisites
- Docker Desktop 4.0+ & Docker Compose 1.29+

### Run with Docker

```bash
git clone <repo-url>
cd paf_assignment/infra
docker compose up --build -d
```

⏳ Wait ~30 seconds for backend initialization, then open:

| Service | URL |
|---------|-----|
| 🌐 Frontend | http://localhost:5173 |
| ⚙️ Backend API | http://localhost:8080 |
| 📖 Swagger UI | http://localhost:8080/swagger-ui.html |
| 📧 Mail UI | http://localhost:1080 |

### Stop Services

```bash
docker compose down
```

### Fresh Database Reset

```bash
docker compose down
docker volume rm -f infra_postgres_data
docker compose up --build -d
```

<details>
<summary>Manual Setup (without Docker)</summary>

**1. Database**
```bash
psql -U postgres -c "CREATE DATABASE smartcampus;"
psql -U postgres -c "CREATE USER smartcampus WITH PASSWORD 'smartcampus';"
psql -U postgres -c "GRANT ALL PRIVILEGES ON DATABASE smartcampus TO smartcampus;"
```

**2. Backend**
```bash
cd backend/api
mvn clean install
mvn spring-boot:run
```

**3. Frontend**
```bash
cd frontend
npm install
npm run dev
```

</details>

---

## 🔑 Test Credentials

| Email | Password | Role |
|-------|----------|------|
| `student@smartcampus.edu` | `student123` | Student |
| `staff@smartcampus.edu` | `staff123` | Staff |
| `admin@smartcampus.edu` | `admin123` | Admin |

---

## 📖 API Documentation

Interactive API docs via Swagger UI at [`/swagger-ui.html`](http://localhost:8080/swagger-ui.html).

<details>
<summary>Key Endpoints</summary>

| Domain | Method | Endpoint |
|--------|--------|----------|
| Auth | `POST` | `/api/auth/login` |
| Auth | `POST` | `/api/auth/oauth/google` |
| Bookings | `GET/POST` | `/api/bookings` |
| Bookings | `GET` | `/api/bookings/admin/pending` |
| Facilities | `GET` | `/api/facilities/{id}/availability` |
| Tickets | `GET/POST` | `/api/tickets` |
| Users | `GET/PUT` | `/api/users/profile` |
| Analytics | `GET` | `/api/analytics/dashboard` |

</details>

---

## 📁 Project Structure

```
paf_assignment/
├── backend/api/src/main/java/com/sliitreserve/api/
│   ├── controllers/     # REST endpoints (auth, bookings, tickets…)
│   ├── services/        # Business logic
│   ├── models/          # JPA entities
│   ├── repositories/    # Data access layer
│   ├── dto/             # Data Transfer Objects
│   └── security/        # JWT & auth config
├── frontend/src/
│   ├── components/      # Reusable UI components
│   ├── pages/           # Page components
│   ├── features/        # Feature modules (bookings, auth, tickets…)
│   ├── services/        # API clients
│   └── contexts/        # React context providers
├── infra/
│   └── docker-compose.yml
└── uploads/             # File storage
```

---

## ⚙️ Configuration

Key settings in `backend/api/src/main/resources/application.yaml`:

```yaml
app:
  jwt:
    secret: your-256-char-secret
    expiration: 86400000  # 24h

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/smartcampus
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: ${GOOGLE_CLIENT_ID}
            client-secret: ${GOOGLE_CLIENT_SECRET}
```

Required environment variables: `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `JWT_SECRET`

---

## 🐛 Troubleshooting

```bash
# View logs
docker compose logs backend -f

# Port conflict (8080 or 5173)
lsof -i :8080   # macOS/Linux
netstat -ano | findstr :8080   # Windows

# Rebuild fresh
docker compose down && docker compose build --no-cache && docker compose up -d
```

See [`QUICK_START_CHECKLIST.md`](./QUICK_START_CHECKLIST.md) · [`DB_SETUP_AND_TESTING_GUIDE.md`](./DB_SETUP_AND_TESTING_GUIDE.md) · [`OAUTH_SETUP_GUIDE.md`](./OAUTH_SETUP_GUIDE.md) for more.

---

## 👥 Team

Developed as a group project for the **SLIIT Professional Advancement Framework (PAF)** program.

**Contributing:**
```bash
git checkout -b feature/your-feature
git commit -am 'Add your feature'
git push origin feature/your-feature
# Open a pull request
```

---

<div align="center">

**Version** `0.0.1-SNAPSHOT` · **Last Updated** April 2026

</div>
