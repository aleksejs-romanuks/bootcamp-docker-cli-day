# Module 2: Self Practice - Docker Basics

## Introduction
The self-practice section will guide you through essential Docker operations. Complete these exercises before attempting the challenge.

## Exercise 1: Getting Started with Docker

### Objective
Learn basic Docker commands and run your first container.

### Instructions

#### Step 1: Test Docker
```bash
# Check if Docker is working
docker --version
docker run hello-world
```

#### Step 2: Run a Web Server
```bash
# Run nginx web server
docker run -d --name my-web -p 8080:80 nginx

# Check if it's running
docker ps

# Test in browser or with curl
curl http://localhost:8080

# View logs
docker logs my-web

# Stop and remove
docker stop my-web
docker rm my-web
```

### What You Learned
- How to run containers
- How to map ports
- How to check container status
- How to view logs and clean up

---

## Exercise 2: Building Your First Image

### Objective
Create a simple Docker image with a custom web page.

### Instructions

#### Step 1: Create a Simple Web App
```bash
# Create workspace
mkdir ~/docker-practice
cd ~/docker-practice

# Create a simple HTML file
cat > index.html << 'EOF'
<!DOCTYPE html>
<html>
<head><title>My Docker App</title></head>
<body>
    <h1>Hello from My Docker Container!</h1>
    <p>This page is served from a custom Docker image.</p>
</body>
</html>
EOF
```

#### Step 2: Create a Dockerfile
```bash
# Create Dockerfile
cat > Dockerfile << 'EOF'
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
EOF
```

#### Step 3: Build and Test
```bash
# Build the image
docker build -t my-app .

# Run your custom container
docker run -d --name my-custom-app -p 8081:80 my-app

# Test it
curl http://localhost:8081

# Clean up
docker stop my-custom-app
docker rm my-custom-app
```

### What You Learned
- How to create a Dockerfile
- How to build custom images
- How to copy files into images

---

## Exercise 3: Working with Data

### Objective
Learn how to persist data using volumes.

### Instructions

#### Step 1: Create a Volume
```bash
# Create a named volume
docker volume create my-data

# Run container with volume
docker run -d --name data-test -v my-data:/data alpine sleep 3600

# Add some data
docker exec data-test sh -c "echo 'Hello Volume' > /data/message.txt"

# Stop and remove container
docker stop data-test
docker rm data-test

# Run new container with same volume
docker run --rm -v my-data:/data alpine cat /data/message.txt

# Clean up
docker volume rm my-data
```

### What You Learned
- How to create and use volumes
- How data persists between containers
- How to share data between containers

---

## Exercise 4: Simple Docker Compose

### Objective
Use Docker Compose to run multiple services together.

### Instructions

#### Step 1: Create a Simple Compose File
```bash
# Create docker-compose.yml
cat > docker-compose.yml << 'EOF'
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    
  database:
    image: postgres:13-alpine
    environment:
      POSTGRES_DB: testdb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
EOF
```

#### Step 2: Run with Compose
```bash
# Start all services
docker-compose up -d

# Check running services
docker-compose ps

# View logs
docker-compose logs

# Stop all services
docker-compose down
```

### What You Learned
- How to define multiple services in one file
- How to start/stop services together
- How to configure environment variables

---

## Quick Reference

### Essential Docker Commands
```bash
# Container management
docker run                # Run a new container
docker ps                 # List running containers
docker stop <name>        # Stop a container
docker rm <name>          # Remove a container

# Image management
docker build -t <name> .   # Build image from Dockerfile
docker images             # List images
docker rmi <image>        # Remove image

# Volume management
docker volume create <name>   # Create volume
docker volume ls             # List volumes
docker volume rm <name>      # Remove volume

# Docker Compose
docker-compose up -d         # Start services
docker-compose down          # Stop services
docker-compose ps            # List services
```

### Common Patterns
```bash
# Run and remove when done
docker run --rm <image>

# Run in background
docker run -d <image>

# Map ports
docker run -p 8080:80 <image>

# Mount volume
docker run -v volume-name:/path <image>

# Set environment variables
docker run -e VAR=value <image>
```

## Next Steps

You're now ready for the Docker Compose challenge! The skills you've practiced here will help you:
- Build more complex applications
- Manage multiple services
- Handle data persistence
- Create production-ready configurations

Proceed to the `challenge/` directory when ready.
