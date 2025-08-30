# Spring Boot Demo Microservice

A Spring Boot 3.5.5 demo microservice with JKube for Kubernetes deployment.

## Prerequisites

- Java 21
- Maven 3.6+
- Docker (for local image building)
- Access to Oracle Container Registry (OCIR)

## Maven Commands

### Build the JAR

```bash
mvn clean compile
mvn clean package
```

### Build the Container Image

```bash
mvn k8s:build
```

### Push the Image to Registry

First, ensure you're logged into the Oracle Container Registry:

```bash
docker login phx.ocir.io
```

Then push the image:

```bash
mvn k8s:push
```

### Generate Kubernetes Manifests

```bash
mvn k8s:resource
```

The generated manifests will be placed in `target/classes/META-INF/jkube/kubernetes/`.

### Deploy to Kubernetes

```bash
mvn k8s:deploy
```

This will deploy the application to the `application` namespace.

### Undeploy from Kubernetes

```bash
mvn k8s:undeploy
```

## Complete Workflow

To build, push, and deploy in one command:

```bash
mvn clean package k8s:build k8s:push k8s:resource k8s:deploy
```

## Configuration

The application is configured to:
- Use Oracle OCIR registry: `phx.ocir.io/maacloud/mark-artifactory/demo`
- Deploy to namespace: `application`
- Expose service on port 8080
- Use Oracle OpenJDK 21 base image

## Endpoints

- Application: http://localhost:8080
- Health check: http://localhost:8080/actuator/health
- API Documentation: http://localhost:8080/swagger-ui.html

## Features

- Spring Boot 3.5.5
- Spring Data JPA with Oracle Database
- Spring Cloud (Eureka, Config, OpenFeign)
- Observability (Micrometer, Prometheus, OpenTelemetry)
- API Documentation (SpringDoc OpenAPI)