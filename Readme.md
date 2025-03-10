# Django React Project Setup Guide

This guide will help you set up and run the Django React project using Docker.

## Prerequisites

Before you begin, make sure you have the following installed on your system:

- Docker
- Docker Compose (usually included with Docker Desktop)
- Git (optional, for cloning the repository)

## Getting Started

### 1. Clone the Repository (if applicable)

```bash
git clone <repository-url>
cd django
```

### 2. Project Structure

The project consists of three main components:

- **Backend**: Django REST API
- **Frontend**: React application with Vite
- **Nginx**: Reverse proxy to route requests

### 3. First-time Setup

Build and Start the Containers

```bash
docker-compose up -d --build
```

This command will:

- Build all the Docker images
- Create and start the containers
- Set up the network between containers
- Initialize the PostgreSQL database

### 4. Accessing the Application

Once the containers are running, you can access:

- **Frontend**: http://localhost:8080
- **Backend API**: http://localhost:8080/api/
- **Django Admin**: http://localhost:8080/api/admin/

### 5. Development Workflow

#### View Logs

To see logs from all containers:

```bash
docker-compose logs -f
```

To see logs from a specific container:

```bash
docker-compose logs -f [service-name]
```

Where [service-name] can be: frontend, backend, nginx, or db.

#### Restart a Service

If you need to restart a specific service:

```bash
docker-compose restart [service-name]
```

#### Stop the Application

To stop all containers:

```bash
docker-compose down
```

To stop all containers and remove volumes (will delete database data):

```bash
docker-compose down -v
```

### 6. Making Changes

- **Frontend**: Changes to the React code will automatically be reflected due to Vite's hot module replacement.
- **Backend**: For some changes to the Django code, you may need to restart the backend container:

```bash
docker-compose restart backend
```

### 7. Troubleshooting

If you encounter issues:

1. Check container logs:

```bash
docker-compose logs [service-name]
```

2. Ensure all containers are running:

```bash
docker-compose ps
```

3. Try rebuilding the containers:

```bash
docker-compose down
docker-compose up -d --build
```

4. If the frontend shows "Host not allowed" errors, ensure your vite.config.js includes:

```bash
   server: {
   host: '0.0.0.0',
   allowedHosts: ['localhost', 'frontend']
   }
```

### 8. Project Configuration

- **Database**: PostgreSQL 15
- **Backend**: Django with Django REST Framework
- **Frontend**: React with Vite
- **Web Server**: Nginx as reverse proxy

## Additional Information

- The PostgreSQL database data is persisted in a Docker volume named `postgres_data`
- The Nginx server routes requests to the appropriate service based on the URL path
- Frontend development server runs on port 5173 inside the container
- Backend API server runs on port 8000 inside the container
- All services are accessible through Nginx on port 8080

##

Happy Coding
