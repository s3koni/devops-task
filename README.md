Nginx Reverse Proxy with Docker Compose


This project demonstrates a containerized web architecture using Docker and Docker Compose. It consists of a Python-based backend service and an Nginx reverse proxy that handles external HTTP requests and forwards them to the backend over an internal Docker network.

The backend is intentionally not exposed to the host system to enforce service isolation, while Nginx acts as the single entry point.



Architecture
Client (Browser / curl)
        |
        v
   Nginx (Port 80 - exposed)
        |
        v
Backend Service (Python HTTP Server - Port 8080, internal only)



Project Structure
devops-task/
├── backend/
│   ├── Dockerfile
│   └── app.py
├── nginx/
│   └── nginx.conf
├── docker-compose.yml
└── README.md


How to Run
Clone and move to the cloned repo
git clone github.com/s3koni/devops-task && cd devops-task


Start services
docker compose up --build -d


How to test
curl http://localhost

Expected output:
Hello from Effective Mobile!


Verify backend isolation
curl http://localhost:8080

Expected output:
curl: (7) Failed to connect to localhost port 8090 after 0 ms: Could not connect to server

Service Communication flow
1. Client sends request to http://loalhost
2. Nginx receives request on port:80
3. Nginx proxies request to backend service via the docker network
4. Backend responds with 
Hello from Effective Mobile!


Design constraints implemented
1. Backend service is not exposed to host machine
2. Only Nginx is publicly accessible
3. Service communication handled via internal Docker bridge network
4. No hardcoded IP addresses used
5. Separate configuration for Nginx reverse proxy

Health check
docker inspect devops-task-backend-1 --format='{{.State.Health.Status}}'

Expected Output:
Healthy


Cleanup
To stop and remove containers
docker compose down

Author
Dan Sekoni
