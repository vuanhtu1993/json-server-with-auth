# JSON Server Mock API

A simple mock API server built with json-server and json-server-auth providing RESTful endpoints for products, categories, and users with authentication.

## Features

- RESTful API endpoints
- Authentication with json-server-auth
- Mock data for products and categories
- Dockerized for easy deployment

## Prerequisites

- Docker and Docker Compose
- Node.js (if running locally without Docker)

## Getting Started

### Using Docker

Build and run the Docker container:

```bash
docker build -t json-server --build-arg PORT=3000 .
docker run -p 3000:3000 -e PORT=3000 json-server
```

To use a different port (e.g., 8082):

```bash
docker build -t json-server --build-arg PORT=8082 .
docker run -p 8082:8082 -e PORT=8082 json-server
```

### Using Docker Compose (Recommended)

Start the service with Docker Compose:

```bash
docker-compose up
```

To use a different port (e.g., 8082):

```bash
# Update your .env file first with PORT=8082
# Then run:
docker-compose up
```

Or specify the port directly:

```bash
PORT=8082 docker-compose up
```

To run in detached mode:

```bash
docker-compose up -d
```

To stop the service:

```bash
docker-compose down
```

### Troubleshooting Port Access Issues

If you can't access the container after changing the port:

1. Make sure both the exposed port and the internal port match in your configuration
2. Check that the PORT environment variable is properly passed to the application
3. Ensure the container is running with `docker-compose ps` or `docker ps`
4. Verify no other services are using the same port on your host machine
5. Try accessing the API with the correct URL: `http://localhost:PORT/`

### Running Locally (without Docker)

1. Install dependencies:
```bash
npm install
```

2. Start the server:
```bash
npm start
```

For development with hot reload:
```bash
npm run dev
```

## API Endpoints

### Authentication

- POST `/register` - Register a new user
- POST `/login` - Login with email and password

Example:
```json
// Register
POST /register
{
  "email": "user@example.com",
  "password": "password123"
}

// Login
POST /login
{
  "email": "user@example.com",
  "password": "password123"
}
```

### Products

- GET `/products` - Get all products
- GET `/products/:id` - Get a specific product
- POST `/products` - Create a new product (requires authentication)
- PUT `/products/:id` - Update a product (requires authentication)
- DELETE `/products/:id` - Delete a product (requires authentication)

### Categories

- GET `/categories` - Get all categories
- GET `/categories/:id` - Get a specific category
- POST `/categories` - Create a new category (requires authentication)
- PUT `/categories/:id` - Update a category (requires authentication)
- DELETE `/categories/:id` - Delete a category (requires authentication)

## Filtering, Sorting and Pagination

json-server supports advanced querying:

- Filter: `GET /products?name=Computer`
- Sort: `GET /products?_sort=originalPrice&_order=desc`
- Pagination: `GET /products?_page=1&_limit=10`

## Environment Variables

- `PORT` - The port the server runs on (default: 3000)

## Project Structure

```
├── src/
│   ├── api.json         # Main database file
│   ├── api-sample.json  # Sample data structure
│   └── index.js         # Server entry point
├── Dockerfile           # Docker configuration
├── docker-compose.yml   # Docker Compose configuration
├── .env                 # Environment variables
├── .dockerignore        # Files to ignore in Docker build
└── package.json         # Node.js dependencies and scripts
```
