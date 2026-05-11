# RentyCar - Backend (NestJS)

REST API for the RentyCar car-rental application. Clients, agents, and admins manage vehicles, offices, reservations, and reviews. JWT auth with role-based guards.

## Prerequisites

- Node.js 18+
- MySQL 8 (originally developed against XAMPP's bundled MySQL)
- npm

## Setup

1. Start a local MySQL server.
2. Load the schema and dev seed from `database.sql` (via phpMyAdmin or any MySQL client). The seed creates one admin and one agent with bcrypt-hashed dev passwords - **rotate before deploying.**
3. `npm install`
4. `cp .env.example .env`, then fill in `DB_PASSWORD` and `JWT_SECRET`.

## Running

```bash
npm run start:dev      # watch mode
npm run build && npm run start:prod
```

## API surface

### Auth
- `POST /auth/client/login`
- `POST /auth/admin/login`
- `POST /auth/agent/login`

### Resources
- `clients/` - register, list, read, update, delete
- `admins/` - admin-only CRUD on admin accounts
- `agents/` - admin-only CRUD on agent accounts
- `offices/` - branch offices
- `vehicles/` - admin / agent / client controllers (different fields per role)
- `reservations/` - book, list, update, cancel
- `reviews/` - post-rental reviews

Each module follows the standard NestJS layout (`*.controller.ts`, `*.service.ts`, `*.module.ts`, `dto/`, `entities/`).
