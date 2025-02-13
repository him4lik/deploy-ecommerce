# E-Commerce Platform

### A modern E-Commerce Platform built using Django and containerized with Docker. This platform provides a seamless shopping experience with features like product management, user authentication, order processing, and background task handling using Celery and Celery Beat. The project is designed for easy local deployment using Docker Compose.

##Features

    Product Management: Add, update, and delete products.

    User Authentication: Secure user registration and login.

    Order Processing: Manage orders and track their status.

    Background Tasks: Handle asynchronous tasks (e.g., sending emails, processing payments) using Celery.

    Periodic Tasks: Schedule recurring tasks (e.g., generating reports, cleaning up old data) using Celery Beat.

    Dockerized: Easy setup and deployment using Docker Compose.

    Scalable: Designed to handle high traffic with resource limits for each service.

##Installation
###Prerequisites

    Docker and Docker Compose installed on your machine.

###Steps

    Clone the repository:
    ```bash
    git clone https://github.com/yourusername/ecommerce-platform.git
    ```
    Navigate to the project directory:
    ```bash
    cd ecommerce-platform
    ```
    Start the services using Docker Compose:
    ```bash
    docker-compose up --build
    ```
    
##Configuration
###Environment Variables

Create a .env_dev file in the root directory with the following variables:
```bash
# Django Settings
SECRET_KEY=your-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

# Database Settings
POSTGRES_DB=yourdb
POSTGRES_USER=youruser
POSTGRES_PASSWORD=yourpassword
POSTGRES_HOST=postgres
POSTGRES_PORT=5432

# Redis Settings
REDIS_URL=redis://redis:6379/0
CELERY_BROKER_URL=redis://redis:6379/0
```
###Volumes

    The api directory is mounted to /code inside the api container for live code updates.

    The web directory is mounted to /code inside the website container for live code updates.

    PostgreSQL data is stored in /dbpool/user1/finaldata/.

##Usage
###Running the Services

    Start all services:
    ```bash
    docker-compose up
    ```
    Access the API at:
    ```bash
    http://localhost:8001
    ```
    Access the website at:
    ```bash
    http://localhost:8101
    ```
###Stopping the Services

    Stop all services:
    ```bash
    docker-compose down
    ```

##Architecture

### The project uses the following architecture:

    ####Django: Backend framework for handling HTTP requests, business logic, and database interactions.

    ####PostgreSQL: Relational database for persistent data storage.

    ####Celery: Handles asynchronous and periodic tasks.

    ####Redis: Message broker for Celery and caching.

    ####Docker: Containerization for easy deployment and scalability.

    ####Docker Compose: Manages multi-container setup (API, Website, PostgreSQL, Redis, Celery Worker, Celery Beat).
