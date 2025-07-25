# Express TypeScript API with PostgreSQL

A simple Express.js API built with TypeScript and PostgreSQL database support.

## Prerequisites

- Node.js (v18 or higher)
- Docker and Docker Compose
- npm or yarn

## Setup Instructions

### 1. Install Dependencies

```bash
npm install
```

### 2. Start PostgreSQL Database

Start the PostgreSQL database using Docker Compose:

```bash
docker compose up -d
```

This will start:

- PostgreSQL database on port 5432

### 3. Environment Variables

The `.env` file is already configured with default values:

- Database: `os_assignment_db`
- Username: `postgres`
- Password: `password123`
- Host: `localhost`
- Port: `5432`

### 4. Run the Application

Development mode (with hot reload):

```bash
npm run dev
```

Production mode:

```bash
npm run build
npm start
```

## Available Endpoints

### API Endpoints

- `GET /health/db` - Database connection health check
- `GET /users` - Get all users
- `POST /users` - Create a new user (requires `name` and `email` in request body)

## Database Schema

The database is automatically initialized with a `users` table:

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Example API Calls

### Get all users

```bash
curl http://localhost:3000/users
```

### Create a new user

```bash
curl -X POST http://localhost:3000/users \
  -H "Content-Type: application/json" \
  -d '{"name": "John Doe", "email": "john@example.com"}'
```

### Check database health

```bash
curl http://localhost:3000/health/db
```

## Docker Commands

Start the database:

```bash
docker-compose up -d
```

Stop the database:

```bash
docker-compose down
```

View logs:

```bash
docker-compose logs postgres
```

Connect to PostgreSQL directly:

```bash
docker exec -it os-assignment-postgres psql -U postgres -d os_assignment_db
```
