# University Grievance Redressal Portal

A comprehensive enterprise-grade platform for managing student and faculty grievances with workflow automation, role-based access control, and appeal management.

## Overview

This portal provides a transparent, efficient, and accountable grievance redressal system for universities, enabling structured submission, tracking, and resolution of grievances with built-in appeal mechanisms.

## Architecture

### Tech Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| Frontend | React 18 + Vite + TypeScript | Modern SPA with fast builds |
| Backend | Node.js + Express + TypeScript | RESTful API with type safety |
| Database | PostgreSQL | ACID-compliant relational storage |
| Auth | JWT + RBAC | Modular permission system |
| Styling | Tailwind CSS | Utility-first CSS framework |

### Project Structure

```
├── frontend/                 # React application
│   ├── src/
│   │   ├── app/             # App configuration, routing, store
│   │   ├── assets/          # Static assets, icons, images
│   │   ├── components/      # Reusable UI components
│   │   │   ├── common/      # Shared components (tables, forms)
│   │   │   ├── layout/      # Layout components (header, sidebar)
│   │   │   └── ui/          # Primitive UI (buttons, inputs)
│   │   ├── features/        # Feature modules by domain
│   │   │   ├── auth/        # Authentication flows
│   │   │   ├── dashboard/   # Role-based dashboards
│   │   │   └── grievances/  # Grievance lifecycle workflows
│   │   ├── services/        # API integration layer
│   │   ├── shared/          # Utilities and custom hooks
│   │   ├── styles/          # Tailwind configuration
│   │   └── i18n/            # Internationalization
│   └── public/
│
├── backend/                  # Node.js API server
│   ├── src/
│   │   ├── config/          # Environment, database, logger
│   │   ├── modules/         # Domain-driven modules
│   │   │   ├── auth/        # Authentication & authorization
│   │   │   ├── users/       # User management
│   │   │   ├── grievances/  # Grievance lifecycle
│   │   │   ├── appeals/     # Appeal workflows
│   │   │   ├── uploads/     # File upload handling
│   │   │   ├── notifications/ # Email/SMS notifications
│   │   │   ├── reports/     # Analytics and reporting
│   │   │   ├── audit/       # Audit trails
│   │   │   └── common/      # Shared module utilities
│   │   └── shared/          # Cross-cutting concerns
│   │       ├── middlewares/ # Request processing
│   │       ├── utils/       # Utility functions
│   │       ├── guards/      # Authorization guards
│   │       ├── decorators/  # Metadata decorators
│   │       ├── interceptors/ # Response transformation
│   │       ├── filters/     # Exception filters
│   │       ├── pipes/       # Validation pipes
│   │       ├── constants/   # Shared constants
│   │       ├── dtos/        # Shared DTOs
│   │       └── entities/    # Shared entities
│   └── test/
│
├── docs/
│   ├── architecture/        # System design documents
│   ├── api/                 # API specifications
│   ├── database/            # Schema diagrams and migrations
│   └── operations/          # Deployment and maintenance
│
└── .claude/
    ├── skills/              # Custom skills for development
    └── memory/              # Project context memory
```

## Features

### Core Workflows

- **Grievance Submission**: Multi-step forms with file attachments
- **Role-Based Triage**: Automatic routing based on grievance type
- **Assignment Tracking**: HOD/Faculty assignment with deadlines
- **Resolution Timeline**: Escalation on SLA breaches
- **Appeal Mechanism**: Two-tier appeal process with hearing scheduling
- **Notification System**: Email alerts at each workflow stage

### User Roles

| Role | Permissions |
|------|-------------|
| Student | Submit grievances, track status, submit appeals |
| Faculty | View assigned grievances, update status, submit resolutions |
| HOD | Assign grievances, monitor department metrics, approve resolutions |
| Dean | Oversee college-level grievances, generate reports |
| Registrar | System-wide access, final appeal authority |
| Admin | User management, system configuration |

## Development

### Prerequisites

- Node.js 18+
- PostgreSQL 14+
- Docker (optional)

### Setup

```bash
# Clone repository
git clone <repo-url>
cd university-grievance-portal

# Frontend
cd frontend
npm install
npm run dev

# Backend
cd ../backend
npm install
npm run start:dev
```

### Environment Variables

Copy `.env.example` to `.env` in both frontend and backend directories.

## Documentation

- [Architecture Overview](./docs/architecture/overview.md)
- [API Documentation](./docs/api/README.md)
- [Database Schema](./docs/database/schema.md)
- [Deployment Guide](./docs/operations/deployment.md)

## License

MIT