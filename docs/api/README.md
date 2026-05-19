# API Documentation

## Base URL
```
http://localhost:3000/api/v1
```

## Authentication

### Login
```http
POST /auth/login
Content-Type: application/json

{
  "email": "student@university.edu",
  "password": "password123"
}
```

**Response:**
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIs...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": "uuid",
    "email": "student@university.edu",
    "role": "student",
    "profile": {}
  }
}
```

### Refresh Token
```http
POST /auth/refresh
Authorization: Bearer {refreshToken}
```

## Endpoints

### Auth Module
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /auth/login | User login |
| POST | /auth/logout | User logout |
| POST | /auth/refresh | Refresh access token |
| POST | /auth/forgot-password | Request password reset |
| POST | /auth/reset-password | Reset password |

### Users Module
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /users/profile | Get current user profile |
| PATCH | /users/profile | Update user profile |
| GET | /users/:id | Get user by ID (RBAC) |
| GET | /users | List users with filters (Admin) |
| POST | /users | Create user (Admin) |
| PATCH | /users/:id | Update user (Admin) |

### Grievances Module
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /grievances | List grievances (filtered by role) |
| POST | /grievances | Create new grievance |
| GET | /grievances/:id | Get grievance details |
| POST | /grievances/:id/submit | Submit grievance (from draft) |
| PATCH | /grievances/:id/assign | Assign to handler |
| PATCH | /grievances/:id/resolve | Mark as resolved |
| POST | /grievances/:id/comments | Add comment |

### Appeals Module
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /appeals | List appeals |
| POST | /appeals | Create appeal |
| GET | /appeals/:id | Get appeal details |
| PATCH | /appeals/:id/schedule | Schedule hearing |
| PATCH | /appeals/:id/decide | Record decision |

### Uploads Module
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /uploads | Upload file |
| GET | /uploads/:id | Download file |
| DELETE | /uploads/:id | Delete file |

## Error Response Format

```json
{
  "statusCode": 400,
  "message": "Validation failed",
  "error": "Bad Request",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Pagination

List endpoints support pagination:
```json
{
  "data": [...],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 100,
    "totalPages": 5
  }
}
```

Query parameters: `page`, `limit`, `sort`, `order`

## Rate Limiting

- 100 requests per minute per IP
- 429 response when exceeded