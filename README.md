# Flask Demo App

A simple Python Flask application built to demonstrate DevOps concepts using Git, GitHub, Docker, and Jenkins CI/CD.

## Project Structure

```text
flaskdemo-app/
├── app.py
├── test_app.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile
└── README.md
```

## Prerequisites

* Python 3.x
* pip
* Docker (optional)
* Jenkins (optional)

## Clone the Repository

git clone https://github.com/gurkiran333/flaskdemo-app.git
cd flaskdemo-app

## Install Dependencies

pip install -r requirements.txt

## Run the Application

python app.py

## Run Unit Tests

pytest

## Build Docker Image

docker build -t flaskdemo-app .

## Run Docker Container

docker run -d -p 5000:5000 --name flaskdemo flaskdemo-app

## Jenkins Pipeline

The included `Jenkinsfile` automates the following tasks:

* Checkout source code
* Install project dependencies
* Execute unit tests
* Build Docker image
* Run Docker container

## Technologies Used

* Python
* Flask
* Pytest
* Docker
* Jenkins
* Git & GitHub

## Author

**Gurkiran Singh Padam**

GitHub: https://github.com/gurkiran333