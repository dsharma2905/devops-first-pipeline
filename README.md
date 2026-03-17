# DevOps First Pipeline
Simple Flask app for practicing Jenkins + Docker CI/CD.

How to run locally:
- python3 -m pip install -r requirements.txt
- python3 app.py

Docker:
docker build -t devanshu2905/devops-first-pipeline:local .
docker run -p 5000:5000 devanshu2905/devops-first-pipeline:local
