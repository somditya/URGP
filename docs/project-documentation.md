# University Grievance Redressal Portal

## Complete Project Documentation & Development Roadmap

---

# 1. PROJECT OVERVIEW

## Project Name

University Grievance Redressal Portal

## Objective

Build a modern enterprise-grade grievance redressal system for a university that supports:

- Student grievances
- Teaching faculty grievances
- Non-teaching staff grievances
- Role-based grievance routing
- Nodal officer workflows
- Appeal workflows
- File uploads
- Automated email communication
- Audit logging
- Analytics and reporting

The system should resemble official university/government e-governance grievance systems.

---

# 2. TECH STACK

## Frontend

- React
- Vite
- TypeScript
- Tailwind CSS
- React Router DOM
- React Hook Form
- Axios

## Backend

- Node.js
- Express
- TypeScript
- JWT Authentication
- Multer
- Nodemailer
- bcrypt

## Database

- PostgreSQL

## Infrastructure

- Docker
- Docker Compose
- GitHub

## Future Ready

- Nginx
- GitHub Actions
- Cloud deployment
- MinIO / S3

---

# 3. USER ROLES

## Roles

| Role                | Description                       |
| ------------------- | --------------------------------- |
| student             | Student complainant               |
| teaching_faculty    | Teaching faculty member           |
| non_teaching_staff  | Administrative/non-teaching staff |
| nodal_officer       | Handles grievances                |
| appellate_authority | Handles appeals                   |
| admin               | System administrator              |

---

# 4. CORE WORKFLOWS

## 4.1 Grievance Workflow

```text
User submits grievance
        ↓
System auto-routes to nodal officer
        ↓
Nodal officer reviews
        ↓
Officer resolves grievance
        ↓
User accepts OR files appeal
```

---

## 4.2 Appeal Workflow

```text
User files appeal
        ↓
Appeal automatically routed to appellate authority
        ↓
Appellate authority reviews
        ↓
Decision:
- uphold
- reopen
- reassign
- escalate
```

---

# 5. SYSTEM ARCHITECTURE

```text
Browser
   ↓
React Frontend (Vite)
   ↓
Express REST API
   ↓
PostgreSQL Database
```

---

# 6. PROJECT STRUCTURE

```text
university-grievance-portal/
 ├── frontend/
 ├── backend/
 ├── docs/
 ├── .claude/
 │    └── skills/
 ├── docker-compose.yml
 ├── CLAUDE.md
 ├── README.md
 └── .gitignore
```

---

# 7. FRONTEND STRUCTURE

```text
frontend/
 ├── src/
 │   ├── pages/
 │   ├── components/
 │   ├── layouts/
 │   ├── hooks/
 │   ├── services/
 │   ├── routes/
 │   ├── context/
 │   ├── utils/
 │   ├── types/
 │   ├── styles/
 │   └── main.tsx
```

---

# 8. BACKEND STRUCTURE

```text
backend/
 ├── src/
 │   ├── controllers/
 │   ├── services/
 │   ├── middleware/
 │   ├── routes/
 │   ├── db/
 │   ├── uploads/
 │   ├── templates/
 │   ├── utils/
 │   ├── validators/
 │   └── server.ts
```

---

# 9. DATABASE DESIGN

## 9.1 Users Table

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),

  full_name TEXT NOT NULL,

  email TEXT UNIQUE NOT NULL,

  password_hash TEXT NOT NULL,

  role TEXT NOT NULL,

  department TEXT,

  phone TEXT,

  is_approved BOOLEAN DEFAULT false,

  created_at TIMESTAMPTZ DEFAULT now()
);
```

---

## 9.2 Grievances Table

```sql
CREATE TABLE grievances (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),

  ticket_no TEXT UNIQUE NOT NULL,

  submitted_by UUID REFERENCES users(id),

  grievance_type TEXT NOT NULL,

  subject TEXT NOT NULL,

  description TEXT NOT NULL,

  assigned_to UUID REFERENCES users(id),

  status TEXT DEFAULT 'pending',

  priority TEXT DEFAULT 'medium',

  appeal_count INTEGER DEFAULT 0,

  resolved_at TIMESTAMPTZ,

  appealed_at TIMESTAMPTZ,

  closed_at TIMESTAMPTZ,

  created_at TIMESTAMPTZ DEFAULT now()
);
```

---

## 9.3 Appeals Table

```sql
CREATE TABLE grievance_appeals (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),

  grievance_id UUID REFERENCES grievances(id),

  appealed_by UUID REFERENCES users(id),

  assigned_to UUID REFERENCES users(id),

  appeal_reason TEXT NOT NULL,

  appeal_status TEXT DEFAULT 'pending',

  authority_decision TEXT,

  authority_remarks TEXT,

  decided_at TIMESTAMPTZ,

  created_at TIMESTAMPTZ DEFAULT now()
);
```

---

## 9.4 Attachments Table

```sql
CREATE TABLE grievance_attachments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),

  grievance_id UUID REFERENCES grievances(id),

  uploaded_by UUID REFERENCES users(id),

  upload_stage TEXT NOT NULL,

  original_file_name TEXT NOT NULL,

  stored_file_name TEXT NOT NULL,

  file_path TEXT NOT NULL,

  mime_type TEXT,

  file_size BIGINT,

  created_at TIMESTAMPTZ DEFAULT now()
);
```

---

## 9.5 Activity Logs Table

```sql
CREATE TABLE grievance_activity_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),

  grievance_id UUID REFERENCES grievances(id),

  action_by UUID REFERENCES users(id),

  action_type TEXT NOT NULL,

  remarks TEXT,

  created_at TIMESTAMPTZ DEFAULT now()
);
```

---

## 9.6 Email Logs Table

```sql
CREATE TABLE email_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),

  grievance_id UUID REFERENCES grievances(id),

  recipient_email TEXT NOT NULL,

  email_type TEXT NOT NULL,

  sent_at TIMESTAMPTZ DEFAULT now(),

  status TEXT DEFAULT 'sent'
);
```

---

# 10. AUTHENTICATION ARCHITECTURE

## JWT Authentication

Workflow:

```text
Login
  ↓
Backend validates user
  ↓
JWT token generated
  ↓
Frontend stores token
  ↓
All APIs protected using JWT middleware
```

---

## Password Security

- Use bcrypt hashing
- Never store plain passwords
- JWT expiry mandatory

---

# 11. ROLE-BASED ACCESS CONTROL

## Student

Can:

- create grievance
- upload documents
- track grievance
- file appeal

Cannot:

- access others' grievances

---

## Nodal Officer

Can:

- view assigned grievances
- resolve grievances
- upload resolution documents

Cannot:

- resolve appeals

---

## Appellate Authority

Can:

- view assigned appeals
- reopen grievances
- uphold decisions
- escalate matters

---

## Admin

Can:

- create nodal mappings
- manage users
- manage roles
- analytics access

---

# 12. FILE UPLOAD SYSTEM

## Allowed File Types

- pdf
- doc
- docx
- jpg
- jpeg
- png
- zip

## Max File Size

10 MB

## Upload Stages

- grievance_submission
- nodal_resolution
- appeal_submission
- appellate_resolution

---

# 13. EMAIL COMMUNICATION SYSTEM

## Provider

Google Workspace SMTP

## Technology

Nodemailer

## Automated Emails

- registration success
- grievance acknowledgement
- grievance assigned
- grievance resolved
- appeal filed
- appeal decision
- password reset
- reminders

---

# 14. TICKET NUMBER FORMAT

```text
UGRP-2026-000001
```

Pattern:

```text
UGRP-{YEAR}-{AUTO_INCREMENT}
```

---

# 15. STATUS FLOW

```text
pending
under_review
resolved
appealed
reopened
escalated
closed
```

---

# 16. FRONTEND PAGES

## Public Pages

- Login
- Register
- Forgot Password

## User Pages

- Dashboard
- Create Grievance
- My Grievances
- Appeal Submission
- Profile

## Nodal Officer Pages

- Officer Dashboard
- Assigned Grievances
- Resolution Form

## Appellate Authority Pages

- Appeals Dashboard
- Appeal Details
- Reopen Workflow

## Admin Pages

- User Management
- Mapping Configuration
- Analytics

---

# 17. API STRUCTURE

## Authentication

```text
POST /api/auth/register
POST /api/auth/login
POST /api/auth/forgot-password
POST /api/auth/reset-password
```

---

## Grievances

```text
POST /api/grievances
GET /api/grievances
GET /api/grievances/:id
PUT /api/grievances/:id/status
```

---

## Appeals

```text
POST /api/grievances/:id/appeal
GET /api/appeals
GET /api/appeals/:id
PUT /api/appeals/:id/decision
```

---

## Attachments

```text
POST /api/attachments/upload
GET /api/attachments/:id/download
```

---

# 18. UI/UX RULES

## Design Style

- Clean
- Modern
- Government/university style
- Accessibility compliant

## Primary Color

```text
#1F4E79
```

## Requirements

- Responsive layouts
- Keyboard navigation
- Accessible forms
- High contrast
- Sticky headers
- Clean tables
- Soft shadows

---

# 19. ACCESSIBILITY REQUIREMENTS

Must support:

- WCAG-friendly contrast
- keyboard navigation
- screen reader labels
- visible focus states
- responsive layouts
- semantic HTML

---

# 20. SECURITY REQUIREMENTS

## Mandatory

- JWT validation
- bcrypt hashing
- role checks
- protected uploads
- MIME validation
- file size validation
- secure environment variables

## Never

- expose uploads publicly
- store plain passwords
- hardcode secrets

---

# 21. DOCKER SETUP

## docker-compose.yml

```yaml
version: "3.9"

services:
  postgres:
    image: postgres:16
    container_name: grievance_postgres
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: grievance_portal
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

---

# 22. ENVIRONMENT VARIABLES

## Backend .env

```env
PORT=5000

DATABASE_URL=postgresql://postgres:postgres@localhost:5432/grievance_portal

JWT_SECRET=your-secret-key

SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=grievance@university.edu
SMTP_PASS=app-password
SMTP_FROM=University Grievance Portal
```

---

# 23. GITHUB WORKFLOW

## Branches

| Branch            | Purpose          |
| ----------------- | ---------------- |
| main              | stable           |
| develop           | integration      |
| feature/auth      | authentication   |
| feature/grievance | grievance module |
| feature/appeals   | appeal module    |

---

## Commit Style

Examples:

```text
Added login UI
Implemented JWT middleware
Created grievance submission API
Added appeal workflow
```

---

# 24. CLAUDE CODE WORKFLOW

## Best Practice

Never ask Claude to build everything at once.

Correct approach:

```text
small module
→ test
→ fix
→ commit
→ push
```

---

# 25. DEVELOPMENT ROADMAP

# PHASE 1

## Project Setup

Tasks:

- Install Node.js
- Install Docker
- Install Git
- Setup frontend
- Setup backend
- Setup PostgreSQL
- Setup GitHub

---

# PHASE 2

## Authentication

Tasks:

- Registration
- Login
- JWT
- Protected routes
- Role middleware

---

# PHASE 3

## Dashboard UI

Tasks:

- Student dashboard
- Officer dashboard
- Appellate dashboard
- Admin dashboard

---

# PHASE 4

## Grievance Module

Tasks:

- grievance form
- ticket generation
- routing logic
- status updates

---

# PHASE 5

## Upload System

Tasks:

- Multer setup
- attachment uploads
- secure downloads
- validation

---

# PHASE 6

## Nodal Workflow

Tasks:

- assigned grievances
- resolution workflow
- resolution uploads

---

# PHASE 7

## Appeal Workflow

Tasks:

- appeal form
- authority mapping
- appeal dashboard
- reopen workflow

---

# PHASE 8

## Email Automation

Tasks:

- acknowledgement mail
- assignment mail
- resolution mail
- reminder mail

---

# PHASE 9

## Analytics & Audit Logs

Tasks:

- reports
- charts
- audit history
- SLA tracking

---

# PHASE 10

## Deployment

Tasks:

- production build
- Nginx
- HTTPS
- VPS deployment
- backup strategy

---

# 26. DAILY DEVELOPMENT PROCESS

## Recommended Daily Flow

```text
1. Pull latest changes
2. Create feature branch
3. Build one module only
4. Test thoroughly
5. Commit changes
6. Push to GitHub
7. Merge later
```

---

# 27. PROFESSIONAL DEVELOPMENT RULES

## Always

- build incrementally
- write reusable code
- separate frontend/backend
- validate inputs
- commit frequently
- test every module

## Never

- build entire app together
- skip authentication
- skip validation
- hardcode secrets
- expose uploads publicly

---

# 28. FIRST TASKS YOU SHOULD DO NOW

## Immediate Next Steps

1. Install all tools
2. Create GitHub repository
3. Create project folders
4. Add CLAUDE.md
5. Setup frontend
6. Setup backend
7. Setup PostgreSQL Docker
8. Create users table
9. Build login page
10. Implement JWT auth

DO NOT start grievance workflows yet.

Authentication first.

---

# 29. FUTURE READY FEATURES

Architecture should later support:

- OCR
- Digital signatures
- SMS notifications
- WhatsApp integration
- Push notifications
- SLA escalation
- Committee workflows
- Video hearings
- eOffice integration
- DigiLocker integration
- Cloud storage
- Analytics dashboards
- Multi-language support
- Mobile app

---

# 30. FINAL DEVELOPMENT PRINCIPLE

Build like a real enterprise software company.

Correct workflow:

```text
Architecture
→ Authentication
→ Roles
→ Dashboards
→ Grievances
→ Appeals
→ Uploads
→ Emails
→ Analytics
→ Deployment
```

Do not rush.

Build module by module professionally.
