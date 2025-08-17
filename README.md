# Experiments in Automated Testing with Codellama.

In this repository, I decided to take up an existing simple MLOPs project form github in order to illustrate
how CodeLLama can be used to automatically generate unit tests. The code below explains 
a typical MLOPs flow for continuous integration and testing. 

Studying Docker and how to package a system to follow this cycle is beyond the scope of the Software Engineering and AI course,
in this tutorial we look into how to generate tests for an existing project using LLKMs.

A part that is normally really difficult in a machine learning project is to produce tests that would allow to check
the behaviour of the system under many circumstances. 
Also one can think about a test, but then it has to be translated into code. The whole process is **boringly important**, 
so a data scientist would try to avoid it to focus on modeling, the software engineer would test the flask application input output,
and that would create something that put in production, crashes after asking the wrong question to the machine learning model.

Let's see how AI can come to rescue.


# Original code:

[![MLOps with Python application](https://github.com/EzioDEVio/MLOps/actions/workflows/main.yml/badge.svg)](https://github.com/EzioDEVio/MLOps/actions/workflows/main.yml)   [![Build and Push Docker image to Github Container Registry](https://github.com/EzioDEVio/MLOps/actions/workflows/GHCR.yml/badge.svg)](https://github.com/EzioDEVio/MLOps/actions/workflows/GHCR.yml)
![Stars](https://img.shields.io/github/stars/EzioDEVio/MLOps?style=social)
![MIT License](https://img.shields.io/github/license/EzioDEVio/MLOps)
![Repo Size](https://img.shields.io/github/repo-size/EzioDEVio/MLOps)
![Last Commit](https://img.shields.io/github/last-commit/EzioDEVio/MLOps?color=blue)

# MLOps Application for Real Estate Price Prediction

This project demonstrates the application of Machine Learning Operations (MLOps) principles to a real estate price prediction model. It includes setting up a Flask application to serve predictions from a trained model and deploying this application using Docker and integrating it into a CI/CD workflow.

## Project Structure

- `app/`: Contains the Flask application files.
  - `server.py`: The Flask server file with API endpoints.
- `models/`: Contains the trained model file.
  - `california_housing_model.joblib`: Pre-trained scikit-learn model.
- `templates/`: HTML files for the application frontend.
- `static/`: CSS and JS files for the frontend.
- `Dockerfile`: Contains all the commands to assemble the app Docker image.
- `requirements.txt`: List of packages required for the application.

## Setup and Installation

### Prerequisites

- Python 3.8+
- pip
- virtualenv (optional)

### Local Setup

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/EzioDEVio/MLOps.git
   cd MLOps
   ```

2. **Create and Activate a Virtual Environment (optional):**

   Windows:
   ```bash
   python -m venv venv
   venv\Scripts\activate
   ```

   macOS/Linux:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install Dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Run the Application:**

   ```bash
   python app/server.py
   ```

   Visit `http://127.0.0.1:5000` in your web browser to view the app.

## Docker Deployment

1. **Build the Docker Image:**

   ```bash
   docker build -t mlops-app .
   ```

2. **Run the Docker Container:**

   ```bash
   docker run -p 5000:5000 mlops-app
   ```

   The application should now be accessible at `http://localhost:5000`.

## CI/CD Integration

This project uses GitHub Actions for Continuous Integration and Continuous Deployment (CI/CD).

### Workflow

1. **Continuous Integration:**

   - Build the Docker image.
   - Run tests (add your tests in the workflow).

2. **Continuous Deployment:**

   - Push the Docker image to a registry (e.g., Docker Hub).
   - Deploy the image to a cloud service (e.g., AWS, Azure).

### Setup GitHub Actions

1. **Create a `.github/workflows` directory in your repository.**

2. **Add a workflow file (e.g., `ci-cd.yml`):**

   ```yaml
   name: CI/CD Pipeline

   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
       - uses: actions/checkout@v2
       - name: Set up Python
         uses: actions/setup-python@v2
         with:
           python-version: '3.8'
       - name: Install dependencies
         run: |
           python -m pip install --upgrade pip
           pip install -r requirements.txt
       - name: Build Docker image
         run: docker build -t mlops-app .
       # Add additional steps for testing and deployment
   ```

## Contributing

Contributions to this project are welcome! Please fork the repository and submit a pull request with your proposed changes.

## License

MIT.


.

