# Nginx Reverse Proxy with Docker Compose

A containerized web architecture using Docker and Docker Compose. The setup includes a Python-based backend service and an Nginx reverse proxy that handles external HTTP requests and forwards them to the backend over an internal Docker network.

The backend is intentionally not exposed to the host system to enforce service isolation. Nginx acts as the single entry point.

<br>

## Architecture

```
Client (Browser / curl)
        |
        v
   Nginx (Port 80 — exposed)
        |
        v
Backend Service (Python HTTP Server — Port 8080, internal only)
```

<br>

## Project Structure

```
devops-task/
├── backend/
│   ├── Dockerfile
│   └── app.py
├── nginx/
│   └── nginx.conf
├── docker-compose.yml
└── README.md
```

<br>

## Getting Started

**Clone the repository**

```bash
git clone github.com/s3koni/devops-task && cd devops-task
```

**Start services**

```bash
docker compose up --build -d
```

<br>

## Testing

**Verify the proxy is working**

```bash
curl http://localhost
```

Expected output:

```
Hello from Effective Mobile!
```

**Verify backend isolation**

```bash
curl http://localhost:8080
```

Expected output:

```
curl: (7) Failed to connect to localhost port 8080 after 0 ms: Could not connect to server
```

<br>

## Service Communication Flow

1. Client sends a request to `http://localhost`
2. Nginx receives the request on port 80
3. Nginx proxies the request to the backend via the internal Docker network
4. Backend responds with `Hello from Effective Mobile!`

<br>

## Design Constraints

- Backend service is not exposed to the host machine
- Only Nginx is publicly accessible
- Service communication is handled via an internal Docker bridge network
- No hardcoded IP addresses
- Nginx reverse proxy configuration is kept separate

<br>

## Health Check

```bash
docker inspect devops-task-backend-1 --format='{{.State.Health.Status}}'
```

Expected output:

```
healthy
```

<br>

## Cleanup

Stop and remove all containers:

```bash
docker compose down
```

<br>

## Author

Dan Sekoni
