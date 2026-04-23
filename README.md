<img width="1900" height="883" alt="image" src="https://github.com/user-attachments/assets/343622e2-a567-4483-b7df-1d7b7c266f98" />


### *Smart Petty Cash Management System*

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-14-black?logo=next.js" />
  <img src="https://img.shields.io/badge/React-18-blue?logo=react" />
  <img src="https://img.shields.io/badge/TailwindCSS-3-38B2AC?logo=tailwind-css" />
  <img src="https://img.shields.io/badge/Prisma-ORM-2D3748?logo=prisma" />
  <img src="https://img.shields.io/badge/PostgreSQL-Database-336791?logo=postgresql" />
  <img src="https://img.shields.io/badge/License-MIT-green" />
</p>

---

## Overview

**Cashra** adalah sistem manajemen petty cash berbasis web yang dirancang untuk memberikan kontrol penuh terhadap pengeluaran operasional secara:

* **Real-time**
* **Terstruktur**
* **Audit-ready**
* **Scalable (multi-user & multi-branch)**

Dibangun dengan arsitektur modern dan siap production.

---

## Key Features

* NIK-based Authentication + RBAC
* Expense Submission & Tracking
* Multi-Level Approval Workflow
* Fund & Balance Management
* Real-time Notification (In-app + Push)
* Export (Excel, PDF, Word)
* Audit Trail (Immutable Logs)

---

## Tech Stack

| Layer        | Technology                          |
| ------------ | ----------------------------------- |
| Frontend     | Next.js, React, TailwindCSS, ShadCN |
| Backend      | Next.js API Route + Service Layer   |
| Database     | PostgreSQL                          |
| ORM          | Prisma                              |
| Notification | Firebase Cloud Messaging            |
| Export       | ExcelJS, PDF-lib, Puppeteer, DOCX   |

---

## System Architecture

```mermaid
flowchart LR

A[Client / Browser] --> B[Next.js Frontend]
B --> C[API Route Handler]
C --> D[Service Layer]

D --> E[(PostgreSQL)]
D --> F[Notification Service]
D --> G[Export Service]

F --> H[FCM Push Notification]
F --> I[In-App Notification]

G --> J[Excel / PDF / Word]
```

---

## Main Workflow (End-to-End)

```mermaid
flowchart TD

%% LOGIN
A[User Login] --> B[Input NIK & Password]
B --> C{Valid?}
C -- No --> B
C -- Yes --> D[Load Role & Permission]

%% DASHBOARD
D --> E[Dashboard]

%% SUBMIT
E --> F[Create Expense]
F --> G[Input Data + Upload Receipt]
G --> H[Save Draft]
H --> I[Submit]

I --> J[Status: Pending]
J --> K[Assign Manager]
K --> L[Notify Manager]

%% MANAGER APPROVAL
L --> M[Manager Review]
M --> N{Approve?}

N -- Reject --> O[Rejected]
O --> P[Notify Staff]
P --> F

N -- Approve --> Q[Forward to Finance]
Q --> R[Notify Finance]

%% FINANCE
R --> S[Finance Review]
S --> T{Valid?}

T -- Reject --> U[Rejected by Finance]
U --> V[Notify Staff]
V --> F

T -- Approve --> W[Final Approval]

%% TRANSACTION
W --> X[Create Transaction]
X --> Y[Update Balance]
Y --> Z[Status: Completed]

Z --> AA[Notify User]
AA --> AB[Audit Log]
AB --> AC[End]
```

---

## Database Core Entities

```mermaid
erDiagram

users ||--o{ expenses : creates
users ||--o{ approvals : approves
users ||--o{ notifications : receives

roles ||--o{ users : has

expenses ||--o{ approvals : has
expenses ||--o{ transactions : generates

petty_cash_funds ||--o{ transactions : contains

transactions ||--o{ audit_logs : tracked
```

---

## Role-Based Access Control (RBAC)

| Role    | Access Level                     |
| ------- | -------------------------------- |
| Admin   | Full system control              |
| Finance | Final approval + fund management |
| Manager | Approval level                   |
| Staff   | Submit expense                   |
| Auditor | Read-only + audit                |

---

## Project Structure

```bash
/app/api
  /auth
  /expenses
  /approvals
  /transactions
  /notifications
  /export

/services
  authService
  expenseService
  approvalService
  notificationService
  exportService

/middleware
  authMiddleware
  rbacMiddleware
```

---

## Engineering Principles

* Atomic DB Transaction (financial safety)
* Strict validation (Zod)
* Clean architecture (service layer separation)
* No business logic in controller
* Async queue for notification

---

## Getting Started

### 1. Clone Repository

```bash
git clone https://github.com/your-username/cashra.git
cd cashra
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Setup

```env
DATABASE_URL=
NEXTAUTH_SECRET=
FCM_SERVER_KEY=
```

### 4. Run Migration

```bash
npx prisma migrate dev
```

### 5. Run App

```bash
npm run dev
```

---

## Export Capability

* Excel (.xlsx)
* PDF (.pdf)
* Word (.docx)

```ts
generateExcel(data)
generatePDF(data)
generateWord(data)
```

---

## Use Cases

* Manufacturing
* Logistics
* Retail
* Consulting
* Technology
* NGO

---

## Roadmap

* [ ] Multi-branch analytics
* [ ] PWA / Mobile support
* [ ] AI anomaly detection
* [ ] Budget forecasting

---

## Contributing

Pull request terbuka.
Ikuti standar arsitektur dan coding yang sudah ditetapkan.

---
