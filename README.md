# Microservices Task

## Overview

This project contains four Node.js services:

- `user-service` provides user data.
- `product-service` provides product data.
- `order-service` creates and lists orders.
- `gateway-service` exposes a single public API and forwards requests to the other services.

Each service has its own `Dockerfile`. The services are built and run together using the `docker-compose.yml` file in the `Microservices` directory.

## Project structure

```text
Microservices/
├── docker-compose.yml
├── gateway-service/
│   ├── Dockerfile
│   ├── app.js
│   └── package.json
├── order-service/
│   ├── Dockerfile
│   ├── app.js
│   └── package.json
├── product-service/
│   ├── Dockerfile
│   ├── app.js
│   └── package.json
└── user-service/
    ├── Dockerfile
    ├── app.js
    └── package.json
```

## Docker setup

The Dockerfiles use the `node:22-slim` image, install each service's dependencies, and start the service with `node app.js`.

Docker Compose creates a private network for the services. The gateway reaches the backend services using their Compose service names:

| Service | Internal address | Published to host |
| --- | --- | --- |
| User | `http://user-service:3000` | No |
| Product | `http://product-service:3001` | No |
| Order | `http://order-service:3002` | No |
| Gateway | `http://gateway-service:3003` | `http://localhost:3003` |

Only the gateway is exposed to the host. Requests to the other services should go through the gateway API.

## Run the application

From the repository root:

```bash
cd Microservices
docker compose up --build -d
```

Check the container status:

```bash
docker compose ps
```

View gateway logs:

```bash
docker compose logs -f gateway-service
```

## Gateway endpoints

### Health check

```bash
curl http://localhost:3003/health
```

### List users

```bash
curl http://localhost:3003/api/users
```

### List products

```bash
curl http://localhost:3003/api/products
```

### List orders

```bash
curl http://localhost:3003/api/orders
```

### Create an order

```bash
curl -X POST http://localhost:3003/api/orders \
  -H "Content-Type: application/json" \
  -d '{"userId":1,"productId":2}'
```

Orders are stored in memory and are cleared when the order-service container restarts.

## Stop the application

```bash
docker compose down
```

To rebuild after changing application code:

```bash
docker compose up --build -d
```
