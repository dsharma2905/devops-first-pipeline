# DevOps First Pipeline
Simple Flask app for practicing Jenkins + Docker CI/CD.

How to run locally:
- python3 -m pip install -r requirements.txt
- python3 app.py

Docker:

docker build -t devanshu2905/devops-first-pipeline:local .

docker run -p 5000:5000 devanshu2905/devops-first-pipeline:local

Architecture:
Developer pushes code → GitHub → GitHub Webhook → ngrok tunnel → Jenkins CI Pipeline → Docker Image Build → DockerHub Push → Kubernetes Deployment → Prometheus Scraping → Grafana Monitoring Dashboard

CI/CD Pipeline:
1. Developer pushes code to GitHub
2. GitHub webhook triggers Jenkins via ngrok
3. Jenkins builds Docker image
4. Jenkins pushes image to DockerHub
5. Jenkins updates Kubernetes deployment
6. Prometheus collects application metrics
7. Grafana visualizes metrics

Project Components:
app.py                 → Flask application
Dockerfile             → Container build instructions
Jenkinsfile            → CI/CD pipeline configuration
deployment.yaml        → Kubernetes deployment manifest
service.yaml           → Kubernetes service (NodePort)
flask-servicemonitor.yaml → Prometheus monitoring configuration
