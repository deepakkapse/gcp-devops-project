# GCP DevOps Project: Python Flask App Deployment

This project demonstrates a complete DevOps pipeline for deploying a Python Flask application on Google Cloud Platform (GCP) using Docker, Google Kubernetes Engine (GKE), and Cloud Build.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Project Structure](#project-structure)
4. [Local Setup and Testing](#local-setup-and-testing)
5. [GCP Setup](#gcp-setup)
6. [Deployment Process](#deployment-process)
7. [Continuous Integration/Continuous Deployment (CI/CD)](#cicd)
8. [Monitoring and Maintenance](#monitoring-and-maintenance)
9. [Troubleshooting](#troubleshooting)
10. [Contributing](#contributing)
11. [License](#license)

## Project Overview

This project sets up an end-to-end DevOps pipeline that includes:
- A simple Python Flask application
- Containerization using Docker
- Version control with Git and GitHub
- Automated builds using Cloud Build
- Deployment to Google Kubernetes Engine (GKE)
- Load balancing for production-ready setup

The application is a basic "Hello, World!" Flask app that demonstrates the deployment process.

## Prerequisites

- Google Cloud Platform account
- gcloud CLI installed and configured
- Docker installed locally
- kubectl installed locally
- Python 3.x installed locally

## Project Structure

```
.
├── Dockerfile
├── app.py
├── cloudbuild.yaml
├── deployment.yaml
├── requirements.txt
└── README.md
```

- `app.py`: The main Flask application
- `Dockerfile`: Instructions for building the Docker image
- `cloudbuild.yaml`: Configuration for Cloud Build
- `deployment.yaml`: Kubernetes deployment configuration
- `requirements.txt`: Python dependencies

## Local Setup and Testing

1. Clone the repository:
   ```
   git clone https://github.com/deepakkapse/gcp-devops-project.git
   cd gcp-devops-project
   ```

2. Create a virtual environment and install dependencies:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   pip install -r requirements.txt
   ```

3. Run the Flask app locally:
   ```
   python app.py
   ```

   Visit `http://localhost:5000` in your browser to see the app running.

4. Build and run the Docker container locally:
   ```
   docker build -t flask-app:v1 .
   docker run -p 5000:5000 flask-app:v1
   ```

   Again, visit `http://localhost:5000` to verify the containerized app is working.

## GCP Setup

1. Create a new GCP project or select an existing one.

2. Enable the following APIs:
   - Cloud Build API
   - Container Registry API
   - Kubernetes Engine API

3. Create a GKE cluster:
   ```
   gcloud container clusters create flask-cluster --num-nodes=2 --zone=us-central1-a
   ```

4. Configure kubectl to use your GKE cluster:
   ```
   gcloud container clusters get-credentials flask-cluster --zone=us-central1-a
   ```

## Deployment Process

1. Push your code to GitHub.

2. Set up a Cloud Build trigger:
   - Go to Cloud Build > Triggers
   - Connect your GitHub repository
   - Create a new trigger that activates on pushes to the main branch

3. The `cloudbuild.yaml` file will instruct Cloud Build to:
   - Build the Docker image
   - Push the image to Container Registry
   - Deploy the application to GKE

4. After the build completes, you can check your deployment:
   ```
   kubectl get deployments
   kubectl get services
   ```

5. Get the external IP of your service and visit it in a browser to see your deployed app.

## CI/CD

The CI/CD pipeline is set up as follows:

1. Developer pushes code to GitHub
2. Cloud Build trigger activates
3. Cloud Build builds Docker image and pushes to Container Registry
4. Cloud Build deploys the new image to GKE
5. Kubernetes rolls out the new version of the application

This process ensures that every push to the main branch results in an automated deployment of the latest version of your application.

## Monitoring and Maintenance

- Use Google Cloud Console to monitor your GKE cluster and deployments
- Set up logging and monitoring in GCP to track application performance
- Regularly update your dependencies and Docker base image for security

## Troubleshooting

- Check Cloud Build logs for build and deployment issues
- Use `kubectl logs` and `kubectl describe` for debugging Kubernetes issues
- Ensure all required APIs are enabled in your GCP project

## Contributing

Contributions to this project are welcome! Please fork the repository and submit a pull request with your changes.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
