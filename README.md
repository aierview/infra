# Infra repository
The **Infra Repository** contains the components that make up the infrastructure for the AIERVIEW application.

## Repository Structure
The **Infra Repository** is organized to separate environments for homologation and production:

```bash
infra/
├── homolog/
│ ├── kafdrop/
│ │ └── Dockerfile
│ ├── kafka/
│ │ └── Dockerfile
│ ├── zookeeper/
│ │ └── Dockerfile
│ ├── redis/
│ │ └── Dockerfile
│ └── docker-compose.yml
├── prod/
│ ├── kafdrop/
│ │ └── Dockerfile
│ ├── kafka/
│ │ └── Dockerfile
│ ├── zookeeper/
│ │ └── Dockerfile
│ ├── redis/
│ │ └── Dockerfile
│ └── docker-compose.yml
```
> Each environment has its own `Dockerfile` for the respective services and a `docker-compose.yml` to orchestrate them. The homologation environment is used for testing and validation, while the production environment is used for the live deployment of AIERVIEW’s infrastructure components.


## Flow
## Service Startup Flow

For both **homologation** and **production** environments, the recommended startup sequence is:

1. **Zookeeper**
   - Start Zookeeper first and wait until it is ready to accept connections.

2. **Kafka**
   - Start Kafka next and wait until it is fully initialized and ready to accept connections.

3. **KafDrop**
   - Start KafDrop after Kafka is running.

4. **Redis**
   - Redis is independent and can be started at any time, even before the other services.

> Following this sequence ensures that all dependent services start correctly without connection errors.

# 🤝 Contribution

This section provides guidelines for contributing to the **Speech Service**.

Repository: [https://github.com/aierview/infra.git](https://github.com/aierview/speech-service.git)

---

## How to Contribute

1. **Clone the repository**
```bash
git clone https://github.com/aierview/infra.git
cd infra
```
2. **Create a new branch from main for your feature or fix:**
```bash
git checkout main
git pull
git checkout -b your-feature-branch
```

3. **Develop your feature or bug fix.**

4. **Commit your changes with clear messages:**
```bash
git add .
git commit -m "Describe your changes"
```
5. **git push origin your-feature-branch**
```bash
git push origin your-feature-branch
```

6. Open a Merge Request (MR) to the homolog branch. Your feature will be reviewed, and validated.
7. Once validated, open a Merge Request to the main branch following the normal workflow.

## ⚠️ Important Notes

- Always create a branch with a **descriptive name** that indicates the purpose of your changes:
   - Features: prefix with `feature/` → e.g., `feature/add-tts-queue`.
   - Bug fixes: prefix with `fix/` → e.g., `fix/audio-upload-bug`.
   - DevOps / CI-CD changes: prefix with `devops/` → e.g., `devops/docker-config`.
   - Documentation: prefix with `docs/` → e.g., `docs/update-readme`.
   - Tests: prefix with `test/` → e.g., `test/tts-unit-tests`.

- Make **small commits** to facilitate the review process.  
  Avoid large commits with multiple unrelated changes; this ensures that the review and approval process is smoother and more efficient.

> It is important that every contribution follows this branching and commit convention to maintain control and clarity over what changes are introduced into the project.

## 🚀 Roadmap / Future Features

- **Kubernetes deployment**: Currently, the application is deployed directly on Fly.io.  
  The plan is to migrate to Kubernetes for a more professional, scalable, and manageable deployment workflow.

- **Authentication service migration**: Move the authentication module currently inside the Interview Service to a **dedicated microservice**.

- **Microservices architecture enhancements**: Introduce a **Config Server**, **Discovery Server**, and an **API Gateway** to better manage and route requests between microservices.

- **Monitoring and observability**: Implement monitoring using **Grafana** and **Elasticsearch** to track service performance, logs, and metrics in real time.

## 📝 License

This project is licensed under the **MIT License**.

---

MIT License

Copyright (c) 2025 AIRVIEW

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## 🔗 Useful Links
- [Redis Documentation](https://redis.io/documentation) – Used for caching and session management.
- [Fly.io](https://fly.io/docs/) – Platform used for deploying the AIRVIEW services.
- [Apache Kafka](https://kafka.apache.org/documentation/) – Official documentation for Kafka, used for message streaming in AIRVIEW.
