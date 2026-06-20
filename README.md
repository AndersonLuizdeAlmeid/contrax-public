
Cole no repo contrax-public no GitHub:

<div align="center">

# Contrax

**Document management SaaS — upload, organize, approve, and track document expiration with automated email alerts.**

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Azure](https://img.shields.io/badge/Azure_Blob_Storage-files-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)](https://azure.microsoft.com/)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=flat-square&logo=nextdotjs&logoColor=white)](https://nextjs.org/)
[![Docker](https://img.shields.io/badge/Docker-ready-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)](https://github.com/features/actions)

</div>

---

## About

Contrax is a production-grade document management SaaS that enables companies to upload, organize, approve, and monitor their documents — with automatic expiration alerts delivered by email before deadlines hit.

The platform ships as two applications: a **web app** for day-to-day document management and a **landing page** for lead capture. Files are stored in Azure Blob Storage, keeping the database lean and storage scalable.

> This repository is a public showcase. The source code is proprietary and kept in a private repository.

---

## Key Features

- **Document upload** — files stored in Azure Blob Storage, metadata in PostgreSQL
- **Expiration tracking** — background service monitors deadlines and sends email alerts automatically
- **Document groups** — organize documents into folders with rename and deactivation support
- **Configurable document types** — define custom types per company with full CRUD
- **Approval workflows** — multi-step document approval with status tracking
- **Signing workflows** — document signing flow with status lifecycle
- **Advanced search and filtering** — filter documents by type, group, status, and date
- **Calendar view** — visualize document deadlines on a calendar
- **Subscription management** — built-in billing and subscription lifecycle
- **Lead capture** — landing page with lead form feeding directly into the backend
- **Guided onboarding** — first-register wizard sets up company and admin in one step
- **Password recovery** — full forgot/reset password flow via email

---

## Architecture
Contrax
├── Contrax.WebApi # REST API — controllers, background services, DI, filters
├── Contrax.Application # Business logic — handlers, queries, repositories, domain
├── Contrax.Commom # Cross-cutting — JWT, Blob Storage, DB, encryption, validators
└── Contrax.Notifications # Email service — expiration alerts and lead notifications

Clean Architecture with a custom Handler pattern:
Request → Controller → IHandler → Handler → IRepository → PostgreSQL
↘ IBlobStorageService → Azure Blob

Background service running on a schedule:
DocumentExpirationNotificationsBackground
└── Queries documents nearing expiration
└── Sends email via Contrax.Notifications (EmailsService)

---
## Tech Stack
| Layer | Technology |
|---|---|
| API | ASP.NET Core 8, C# |
| ORM / Query | Dapper (raw SQL, no EF Core) |
| Database | PostgreSQL 16 |
| File Storage | Azure Blob Storage |
| Email | SMTP via custom EmailsService |
| Background Jobs | ASP.NET Core IHostedService |
| Frontend (App) | Next.js 15, TypeScript |
| Frontend (Landing) | Next.js 15, Tailwind CSS |
| Auth | JWT + Argon2 password hashing |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions → Docker Hub |
| Migrations | Versioned SQL scripts |
---
## Domain Modules
| Module | Responsibilities |
|---|---|
| `Documents` | Upload, update, delete, filter, download, expiration confirmation |
| `DocumentsGroups` | Folder-like grouping — create, rename, deactivate |
| `DocumentsTypes` | Configurable document type catalog per company |
| `DocumentUsages` | Track document access and usage history |
| `ApprovalWorkflows` | Multi-step approval lifecycle with status enum |
| `SignWorkflows` | Signing request lifecycle with status enum |
| `Subscriptions` | Subscription plans and billing status |
| `Leads` | Lead capture from landing page |
| `Companies` | Company profile and settings |
| `Users` | User lifecycle — create, activate, deactivate |
| `ForgotPasswordRequests` | Full forgot/reset password flow |
| `FirstRegisters` | Guided company + admin onboarding |
---
## Background Service
A hosted background service runs on a configurable schedule and:
1. Queries all documents with upcoming expiration dates
2. Groups notifications by company and user
3. Sends personalized email alerts with document details
4. Logs notification delivery for audit purposes
This ensures companies never miss a document deadline without manual monitoring.
---
## Applications
| App | Description |
|---|---|
| **Web App** | Full document management dashboard — upload, organize, search, approve, sign |
| **Landing Page** | Marketing page with lead capture form integrated to the backend |
---
## API Overview
POST /auth/login
POST /first-register
POST /forgot-password/request
POST /forgot-password/reset

POST /documents
GET /documents
GET /documents/{id}
PUT /documents/{id}
DELETE /documents/{id}
GET /documents/{id}/download
PUT /documents/{id}/confirm-expiration

GET /documents-groups
POST /documents-groups
PUT /documents-groups/{id}/rename

GET /documents-types
POST /documents-types
PUT /documents-types/{id}

POST /leads
GET /users
GET /company

---
## Contact
**Anderson Luiz de Almeida** — Backend Developer | .NET · Clean Architecture · Azure

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/anderson-luiz-almeida)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/AndersonLuizdeAlmeid)
