# CVHub Gateway

The CVHub Gateway repository contains the REST API gateway for the CVHub microservices system. 
It serves as the single external entry point for clients, exposing HTTP/JSON endpoints while internally communicating with the microservices via gRPC.

## Purpose

- Provide RESTful HTTP endpoints for external clients (web, mobile, etc.).
- Forward incoming requests to the appropriate internal gRPC microservice.
- Aggregate responses from multiple services when necessary.
- Handle common API gateway tasks: authentication, logging, rate limiting, error handling.

## Usage

1. Clone this repository.
2. Configure the gateway to connect to the internal gRPC microservices.
3. Start the gateway server (example using Crow / Pistache in C++ or any other framework):

```bash
# Example C++ using Crow
./cvhub-gateway --config config.json
```
4. Clients can now send HTTP requests to the gateway:
```bash
curl -X POST http://localhost:8080/detect \
     -H "Content-Type: application/json" \
     -d '{"image_data": "<base64 encoded image>"}'
```

## Repository Structure
```text
cvhub-gateway/
├── src/                # Source code for the REST API gateway
├── include/            # Header files
├── config/             # Configuration files (gRPC addresses, ports, etc.)
├── README.md
└── LICENSE
```

## Guidelines
- Keep the gateway stateless; all business logic should reside in the microservices.
- Use the shared cvhub-proto repository to generate gRPC client stubs.
- Ensure version compatibility between REST endpoints and internal gRPC services.
- Include logging and error handling to monitor request flow.
