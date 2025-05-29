# Eshop-Auth Project

## Overview
Eshop-Auth is a web application built using Flask that provides user authentication, product management, and cart operations. It connects to a MongoDB database to store user and product information.

## Project Structure
```
Eshop-Auth
├── app.py               # Main application file for the Flask app
├── dbinit.py            # Initializes the MongoDB database with predefined products
├── requirements.txt     # Lists the Python dependencies required for the project
├── Dockerfile           # Instructions to build a Docker image for the application
├── docker-compose.yml   # Defines the services for the Docker application
└── README.md            # Documentation for the project
```

## Setup Instructions

### Prerequisites
- Docker
- Docker Compose

### Installation
1. Clone the repository:
   ```
   git clone <repository-url>
   cd Eshop-Auth
   ```

2. Build the Docker image and start the application:
   ```
   docker-compose up --build
   ```

3. Access the application at `http://localhost:5000`.

### Usage
- The application provides endpoints for user registration, login, product management, and cart operations.
- Refer to the API documentation for details on available endpoints and their usage.

## Docker Usage

### Dockerfile
A sample `Dockerfile` is provided to containerize the Flask application:

```
# Use official Python image
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

### docker-compose.yml
A sample `docker-compose.yml` is provided to run the Flask app and a MongoDB instance:

```
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    environment:
      - FLASK_ENV=development
      - MONGO_URI=mongodb://mongo:27017/eshop
    depends_on:
      - mongo

  mongo:
    image: mongo:6
    restart: always
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

> **Note:** Update your `app.py` to use the `MONGO_URI` environment variable for connecting to MongoDB in Docker.

## License
This project is licensed under the MIT License.