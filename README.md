# E-Commerce Platform

A modern E-Commerce Platform built using Django and containerized with Docker. This platform provides a seamless shopping experience with features like product management, user authentication, order processing, and background task handling using Celery and Celery Beat. The project is designed for easy local deployment using Docker Compose.

## Features
Product Management: Add, update, and delete products.
User Authentication: Secure user registration and login.
Order Processing: Manage orders and track their status.
Background Tasks: Handle asynchronous tasks (e.g., sending emails, processing payments) using Celery.
Periodic Tasks: Schedule recurring tasks (e.g., generating reports, cleaning up old data) using Celery Beat.
Dockerized: Easy setup and deployment using Docker Compose.
Scalable: Designed to handle high traffic with resource limits for each service.

## Installation
### Prerequisites
#### 1. Install Docker
Run the following commands to install Docker on Ubuntu:

```bash
sudo apt update && sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update && sudo apt install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER && newgrp docker
```
### Steps

Clone the repository:
```bash
git clone --recurse-submodule https://github.com/him4lik/deploy-ecommerce.git
```
    
## Configuration
### 1. Add Aliases to .bash_aliases
Add the following script to your .bash_aliases file for easier Docker management:

```bash
alias dc='docker compose -f docker-compose.yml -f docker-compose.dev.yml --compatibility'
alias dshell='docker exec -ti leaderboard_deploy_leaderboard_1 /bin/bash'
dclogs(){
        dc logs --tail=100 --follow $@
}
dcrestart(){
        dc stop $@
        dc rm -f -v $@
        dc up --build -d $@
}
```
### 2. Environment Variables

Create a .env_dev file in the root directory with the following variables:
```bash
# Django Settings
DEBUG=True
PATH_SPEC=test

# Database Settings
DB_NAME=yourdb
DB_USER=youruser
DB_PASSWORD=yourpassword
DB_HOST=postgres
```
### 3. Navigate to the project directory:
```bash
cd deploy-ecommerce
```
### 4. Start the services using command added in .bash_aliases file:
```bash
dcrestart
```
### Volumes
The api directory is mounted to /code inside the api container for live code updates.
The web directory is mounted to /code inside the website container for live code updates.
PostgreSQL data is stored in /dbpool/user1/finaldata/.

## Usage
### Running the Services
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
### Stopping the Services
Stop all services:
```bash
docker-compose down
```

## Architecture

### The project uses the following architecture:
    - Django: Backend framework for handling HTTP requests, business logic, and database interactions.
    - PostgreSQL: Relational database for persistent data storage.
    - Celery: Handles asynchronous and periodic tasks.
    - Redis: Message broker for Celery and caching.
    - Docker: Containerization for easy deployment and scalability.
    - Docker Compose: Manages multi-container setup (API, Website, PostgreSQL, Redis, Celery Worker, Celery Beat).
