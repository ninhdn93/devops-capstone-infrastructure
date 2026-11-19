# DevOps Capstone — Automated 3-Tier Application Deployment

A hands-on DevOps portfolio project implementing containerized application deployment, CI/CD automation, Kubernetes orchestration, and centralized observability.

## Project Overview

This project deploys a three-tier To-Do application consisting of:

- **Frontend:** Next.js 14 / React / TypeScript
- **Backend:** Node.js / Express / TypeScript
- **Database:** PostgreSQL 17
- **Containerization:** Docker and Docker Compose
- **CI/CD:** Jenkins (planned)
- **Production orchestration:** Kubernetes with Kind (planned)
- **Observability:** Prometheus, Grafana, and Loki (planned integration)

## Architecture

```text
Browser
   |
   v
Next.js Frontend (localhost:3001)
   |
   v
Express Backend API (localhost:5000)
   |
   v
PostgreSQL 17 (Private Docker Network)
```

## Related Repositories

- [Frontend](https://github.com/ninhdn93/devops-bootcamp-todolist-frontend)
- [Backend API](https://github.com/ninhdn93/devops-bootcamp-todolist-backend-api)

The application source is based on the DevOpsWay training repositories and is being improved through independent containerization, security, automation, deployment, and troubleshooting work.

## Local Development Deployment

### Prerequisites

- Docker Engine / Docker Desktop
- Docker Compose
- Git

### 1. Clone the repositories

Place the infrastructure, frontend, and backend repositories in the same parent directory.

### 2. Build Docker images

From the parent directory:

```powershell
docker build -t capstone-frontend:baseline ./devops-bootcamp-todolist-frontend
docker build -t capstone-backend:baseline ./devops-bootcamp-todolist-backend-api
```

### 3. Configure environment variables

Inside the infrastructure repository:

```powershell
Copy-Item .env.example .env
```

Replace `REPLACE_WITH_SECURE_PASSWORD` in `.env` with a strong, unique password.

Never commit `.env` or real credentials.

### 4. Start the application

```powershell
docker compose -f compose.dev.yaml up -d
docker compose -f compose.dev.yaml ps
```

### 5. Access the application

- Frontend: http://localhost:3001
- Backend API: http://localhost:5000
- Health: http://localhost:5000/health
- Readiness: http://localhost:5000/ready

### 6. Stop the application

```powershell
docker compose -f compose.dev.yaml down
```

The PostgreSQL named volume is retained.

## Verification

The following checks have been completed in the local lab:

- Frontend and backend Docker images successfully built.
- PostgreSQL initialized successfully.
- Backend connected to PostgreSQL.
- Health and readiness endpoints returned HTTP 200.
- To-Do CRUD operations (Create, Read, Update, Delete) were verified.
- PostgreSQL data persisted across container recreation.

## Project Roadmap

- [x] Local three-tier deployment using Docker Compose
- [x] Application API and CRUD verification
- [ ] Docker image security hardening
- [ ] Automated tests and Jenkins CI/CD
- [ ] Kubernetes Kind deployment
- [ ] Infrastructure and application observability
- [ ] Architecture diagrams and deployment evidence

## Security Considerations

- Database credentials are injected through environment variables.
- PostgreSQL is not published to the host.
- Local application ports are bound to `127.0.0.1`.
- Sensitive configuration files are excluded from Git.
- Kubernetes example secrets contain placeholders only.

## Acknowledgements

Application source repositories originate from the DevOpsWay bootcamp. This portfolio documents the deployment implementation, operational validation, troubleshooting, and subsequent DevOps improvements.