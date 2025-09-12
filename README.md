# BobApp

Clone project:

> git clone XXXXX

## Front-end

Go inside folder the front folder:

> cd front

Install dependencies:

> npm install

Launch Front-end:

> npm run start;

### Docker

Build the container:

> docker build -t bobapp-front .

Start the container:

> docker run -p 8080:80 --name bobapp-front -d bobapp-front

## Back-end

Go inside folder the back folder:

> cd back

Install dependencies:

> mvn clean install

Launch Back-end:

> mvn spring-boot:run

Launch the tests:

> mvn clean install

### Docker

Build the container:

> docker build -t bobapp-back .

Start the container:

> docker run -p 8080:8080 --name bobapp-back -d bobapp-back

## Production Deployment

### Using Docker Compose

1. Copy the environment file:

   ```bash
   cp .env.example .env
   ```

2. Edit `.env` with your Docker Hub credentials

3. Run with Docker Compose:
   ```bash
   docker-compose up -d
   ```

## CI/CD Pipeline

This project uses GitHub Actions for continuous integration and deployment.

### Automated Workflows

1. **CI Pipeline** (`.github/workflows/ci.yml`):

   - Runs on every push to `main` branch
   - Executes tests for both backend and frontend
   - Generates coverage reports (Jacoco for backend, npm coverage for frontend)
   - Runs SonarQube analysis for code quality
   - Builds and pushes Docker images to Docker Hub

2. **Deploy Pipeline** (`.github/workflows/deploy.yml`):
   - Manual deployment workflow
   - Can deploy to production or staging environments

### Required Secrets

Add these secrets to your GitHub repository:

- `DOCKER_USERNAME`: Your Docker Hub username
- `DOCKER_PASSWORD`: Your Docker Hub password
- `SONAR_TOKEN`: Your SonarQube/SonarCloud token
- `SONAR_HOST_URL`: Your SonarQube/SonarCloud URL (e.g., https://sonarcloud.io)

### Quality Gates (KPIs)

- **Coverage**: Backend ≥ 80%, Frontend ≥ 70%
- **SonarQube Issues**: 0 blocker, < 5 critical
- **Duplication**: < 3%

### Workflow Triggers

- **Automatic**: Push to `main` branch triggers CI
- **Manual**: Go to Actions tab → Deploy to Production → Run workflow

## Project Structure

```
├── back/                 # Spring Boot backend
│   ├── src/
│   ├── Dockerfile
│   └── pom.xml
├── front/                # Angular frontend
│   ├── src/
│   ├── Dockerfile
│   └── package.json
├── .github/workflows/    # GitHub Actions
├── docker-compose.yml    # Docker Compose configuration
└── README.md
```
# Test SonarQube
# Test Docker deployment - Ven 12 sep 2025 12:46:50 CEST
