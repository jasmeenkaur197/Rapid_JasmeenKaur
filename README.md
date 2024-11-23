PDF Web App
A simple web application that converts PDFs to text and provides a UI to interact with the PDF files. The app allows users to upload PDF files, converts them to text, and displays the extracted text on a webpage.

Features
PDF to Text Conversion: Upload PDF files and convert them to plain text.
UI: A simple web interface for users to upload PDFs and view the extracted text.
Dockerization: The application is Dockerized for easy deployment and scaling.
Kubernetes Deployment: Kubernetes manifest files for hosting the application on a Kubernetes cluster.
Technologies Used
Backend: Python (Flask)
Frontend: HTML, CSS (with a modern UI design)
Containerization: Docker
Orchestration: Kubernetes
CI/CD: GitHub Actions for automated Docker image building and deployment
Installation
Prerequisites
Before running the application, ensure that you have the following:

Python 3.x (for local development)
Docker (for containerization)
Kubernetes (for deployment)
GitHub or Bitbucket (for repository management)
Local Development Setup
Clone the repository:

bash
Copy code
git clone https://github.com/yourusername/pdf-web-app.git
cd pdf-web-app
Install dependencies:

bash
Copy code
pip install -r requirements.txt
Run the Flask web server:

bash
Copy code
python app.py
The app will be accessible at http://127.0.0.1:5000.
Docker Setup
To run the application in a Docker container:

Build the Docker image:

bash
Copy code
docker build -t pdf-web-app .
Run the Docker container:

bash
Copy code
docker run -p 8080:8080 pdf-web-app
Access the application at http://127.0.0.1:8080.

CI/CD with GitHub Actions
A GitHub Actions pipeline is set up to build and push the Docker image to Docker Hub automatically when changes are pushed to the main branch.

GitHub Actions Pipeline
The GitHub Actions pipeline (.github/workflows/docker.yml) will:

Build the Docker image.
Log in to Docker Hub using stored credentials.
Push the Docker image to Docker Hub.
GitHub Secrets
Make sure to set the following GitHub Secrets:

DOCKER_USERNAME: Your Docker Hub username.
DOCKER_PASSWORD: Your Docker Hub password.
Bash Script to Run the Container
Create a run.sh script to build and run the Docker container:

bash
Copy code
#!/bin/bash

# Build the Docker image
docker build -t pdf-web-app .

# Run the Docker container on port 8080
docker run -p 8080:8080 pdf-web-app
Make the script executable:

bash
Copy code
chmod +x run.sh
Run the container using:

bash
Copy code
./run.sh
Kubernetes Setup
Kubernetes manifest files are provided to deploy the web app in a Kubernetes cluster.

Kubernetes Deployment
Create the deployment (deployment.yaml):

yaml
Copy code
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pdf-web-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: pdf-web-app
  template:
    metadata:
      labels:
        app: pdf-web-app
    spec:
      containers:
      - name: pdf-web-app
        image: pdf-web-app:latest
        ports:
        - containerPort: 8080
Create the service (service.yaml):

yaml
Copy code
apiVersion: v1
kind: Service
metadata:
  name: pdf-web-app-service
spec:
  selector:
    app: pdf-web-app
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
  type: LoadBalancer
Apply the files to Kubernetes:

bash
Copy code
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
The web app will be hosted and accessible through the Kubernetes service.

Exception Handling
The web application includes exception handling for various scenarios, such as:

File Not Found: If the uploaded PDF file is not found or is corrupted, an appropriate error message will be shown.
Invalid File Format: If a non-PDF file is uploaded, an error message will inform the user to upload a valid PDF.
General Errors: Generic errors are captured and displayed to the user, with detailed logs for developers.
UI Improvements
The UI has been improved to be modern and responsive, featuring:

Custom Styling: Colors have been customized, and the layout is designed for simplicity and clarity.
Responsive Design: The web app is designed to work seamlessly on both desktop and mobile devices using media queries.
Interactive Feedback: Success or failure messages are shown based on the result of the PDF conversion.
