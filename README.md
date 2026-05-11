# RentyCar

REST API for a car-rental application. Three roles (clients, agents, admins) interact with vehicles, offices, reservations, and reviews. Built with NestJS + MySQL, JWT auth with role-based guards.

This snapshot contains only the backend - the planned React frontend was not preserved.

## Tech stack

- NestJS (TypeScript), TypeORM, MySQL 8
- `@nestjs/jwt` + `passport-jwt` for auth, `bcrypt` for password hashing
- ESLint + Prettier

## Folder structure

```
rentycar/
└── backend/
    ├── src/
    │   ├── admins/   agents/   auth/   clients/
    │   ├── offices/  reservations/  reviews/  vehicles/
    │   └── main.ts, app.module.ts
    ├── test/
    ├── database.sql       # schema + dev seed
    ├── .env.example
    ├── package.json
    └── README.md
```

## How to run

See [`backend/README.md`](backend/README.md). Short version:

```bash
cd backend
npm install
cp .env.example .env       # fill in DB_PASSWORD and JWT_SECRET
# load database.sql into a local MySQL
npm run start:dev
```

API at `http://localhost:3000`.

## What the code does

Each domain (admins, agents, clients, offices, vehicles, reservations, reviews) is a standard NestJS module with `controller.ts`, `service.ts`, `module.ts`, `dto/`, and `entities/`. Auth issues role-tagged JWTs from three separate login endpoints (`/auth/{client,agent,admin}/login`); routes are protected by `JwtAuthGuard` + a `RolesGuard` that reads the `@Roles(...)` decorator. Vehicles have three controllers (admin / agent / client) exposing different fields per role. Reservations enforce date-overlap and availability checks.
