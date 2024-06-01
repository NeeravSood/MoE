# Mixture of Experts (MoE) System

This repository contains a Mixture of Experts (MoE) system designed to handle various natural language processing (NLP) tasks by routing queries to specialized expert models. The system is built using FastAPI and integrates multiple pre-trained transformer models from Hugging Face's `transformers` library.

## Features

- **General Language Understanding**: Utilizes the LLama model from EleutherAI for general NLP tasks.
- **Sentiment Analysis**: Uses the efficient DistilBERT model for analyzing the sentiment of the text.
- **Text Generation**: Implements GPT-Neo from EleutherAI for generating human-like text based on given prompts.
- **Scientific Text Classification**: Leverages SciBERT from AllenAI for classifying and understanding scientific texts.
- **Router**: Employs a BERT-based router to classify incoming queries and route them to the appropriate expert model.
- **Scalable Deployment**: Containerized using Docker and deployable on cloud platforms such as AWS ECS.
- **CI/CD Pipeline**: Automated build, test, and deployment using GitHub Actions.

## Getting Started

### Prerequisites

- Docker
- Python 3.9
- GitHub account for CI/CD

### Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/your-username/mixture-of-experts.git
    cd mixture-of-experts
    ```

2. **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

3. **Train the Router Model**:
    ```bash
    python router_training.py
    ```

### Running the Application

#### Using Docker

1. **Build the Docker image**:
    ```bash
    docker build -t mixture_of_experts .
    ```

2. **Run the Docker container**:
    ```bash
    docker run -p 80:80 mixture_of_experts
    ```

#### Using Docker Compose

1. **Run the application with Docker Compose**:
    ```bash
    docker-compose up
    ```

### API Usage

The MoE system provides an API endpoint to process queries.

- **Endpoint**: `/query`
- **Method**: POST
- **Request Body**: JSON object with the query text
    ```json
    {
      "query": "Tell me a story about a dragon."
    }
    ```
- **Response**: JSON object with the query, the expert model used, and the response
    ```json
    {
      "query": "Tell me a story about a dragon.",
      "expert": "generation",
      "response": "Once upon a time..."
    }
    ```

### CI/CD Pipeline

The repository includes a GitHub Actions workflow to automate the build, test, and deployment process.

1. **Configure Secrets**:
    - `DOCKER_HUB_USERNAME`
    - `DOCKER_HUB_PASSWORD`
    - `AWS_ACCESS_KEY_ID`
    - `AWS_SECRET_ACCESS_KEY`

2. **Push Changes to Main Branch**:
    - The pipeline triggers on pushes to the `main` branch and follows these steps:
        - Checkout code
        - Set up Python environment
        - Install dependencies
        - Run tests
        - Build and push Docker image
        - Deploy to AWS ECS

### Deployment

#### AWS ECS

1. **Create a Task Definition**:
    - Define your container settings, including the image URI and necessary environment variables.

2. **Create an ECS Service**:
    - Set up the service to run the task definition, including load balancing and auto-scaling configurations.

3. **Set Up a Load Balancer**:
    - Configure an Elastic Load Balancer (ELB) to distribute traffic to your ECS service.

4. **Configure CloudWatch Monitoring**:
    - Set up CloudWatch for logging and monitoring the performance and health of your service.

### Contributing

Contributions are welcome! Please submit a pull request or open an issue to discuss improvements or new features.
