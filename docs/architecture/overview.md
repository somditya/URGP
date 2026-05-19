# Architecture Overview

## System Architecture

The University Grievance Redressal Portal follows a layered architecture pattern with clear separation between presentation, business logic, and data layers.

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Frontend (React)                      │
│  ┌──────────────────────────────────────────────────┐   │
│  │                    Vite Dev Server                │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                            │ HTTP/JSON
                            ▼
┌─────────────────────────────────────────────────────────┐
│                    Backend (Express)                     │
│  ┌──────────────────────────────────────────────────┐   │
│  │         Modules (Auth, Grievances, etc.)         │   │
│  │  ┌─────────────┬─────────────┬───────────────┐   │   │
│  │  │ Controllers │  Services   │ Repositories  │   │   │
│  │  └─────────────┴─────────────┴───────────────┘   │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                            │
            ┌───────────────┼───────────────┐
    ┌───────▼───────┐  ┌────▼────┐  ┌───────▼───────┐
    │   PostgreSQL  │  │ Redis   │  │ File Storage  │
    │   (Primary)   │  │ (Cache) │  │   (Local)     │
    └───────────────┘  └─────────┘  └───────────────┘
```

## Component Architecture

### Frontend Layers

1. **Presentation Layer** (`components/`)
   - UI primitives, layout components, feature-specific views
   - State-driven rendering with React hooks

2. **State Management** (`app/`)
   - React Query for server state
   - Zustand/Context for client state
   - Feature-specific stores

3. **Data Layer** (`services/`)
   - API client with interceptors
   - Request/response transformation
   - Error handling abstraction

### Backend Layers

1. **Entry Point** (`main.ts`)
   - Express application bootstrap
   - Middleware configuration
   - Route registration

2. **Module Layer** (`modules/`)
   - **Controllers**: Handle HTTP requests/responses
   - **Services**: Business logic execution
   - **Repositories**: Database queries with TypeORM
   - **DTOs**: Data validation and transformation
   - **Entities**: TypeORM database entities

3. **Shared Layer** (`shared/`)
   - Cross-cutting concerns
   - Guards for authorization
   - Interceptors for logging/response transformation
   - Pipes for validation

## Database Schema

### Core Entities

```
users
├── id (PK)
├── email
├── password_hash
├── role
├── profile_data (JSON)
└── created_at

grievances
├── id (PK)
├── title
├── description
├── type
├── status (enum: DRAFT, SUBMITTED, ASSIGNED, RESOLVED, CLOSED)
├── submitted_by (FK users)
├── assigned_to (FK users)
├── department_id
├── resolution_text
├── created_at
└── updated_at

appeals
├── id (PK)
├── grievance_id (FK grievances)
├── status (enum: PENDING, SCHEDULED, HEARD, DECIDED)
├── hearing_date
├── decision_text
└── created_at

uploads
├── id (PK)
├── filename
├── original_name
├── mime_type
├── size
├── uploaded_by (FK users)
└── created_at
```

## Security Architecture

### Authentication Flow

1. User submits credentials to `/auth/login`
2. Backend validates credentials, generates JWT
3. Frontend stores JWT in secure httpOnly cookie
4. Subsequent requests include JWT in Authorization header

### Authorization Model

Role-based access control with the following permissions:

| Resource | Student | Faculty | HOD | Dean | Registrar | Admin |
|----------|---------|---------|-----|------|-----------|-------|
| Submit Grievance | ✓ | | | | | |
| View Own Grievances | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Assign Grievances | | | ✓ | ✓ | | |
| Resolve Grievances | | ✓ | ✓ | ✓ | |
| Process Appeals | | | | ✓ | ✓ | |
| Manage Users | | | | | | ✓ |
| System Config | | | | | | ✓ |

## Workflow Patterns

### Grievance Lifecycle

```
DRAFT → SUBMITTED → TRIAGE → ASSIGNED → IN_PROGRESS → RESOLVED → CLOSED
                    ↘                                           ↗
                     → ESCALATED → REASSIGNED → RESOLVED → CLOSED
```

### Appeal Lifecycle

```
APPEAL_SUBMITTED → REVIEW → HEARING_SCHEDULED → HEARD → DECISION_MADE → CLOSED
```

## Deployment Architecture

### Development
- Docker Compose for local development
- Hot reload on both frontend and backend
- Local PostgreSQL instance

### Production
- Frontend: Static hosting (Nginx, S3, or CDN)
- Backend: Node.js process manager (PM2 or Docker Swarm)
- Database: Managed PostgreSQL (AWS RDS, Supabase)
- Cache: Redis cluster
- Storage: Cloud object storage (S3, GCS)

## Monitoring & Observability

- Request logging with correlation IDs
- Error tracking with stack traces
- Performance metrics via Prometheus
- Health check endpoints
- Audit log for compliance