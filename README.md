# 🎓 UMMU University System

A modern university information system built with microservices architecture using Go, PostgreSQL, Kong Gateway, OpenTelemetry, Prometheus, Grafana, and Jaeger.

---

## About

UMMU University System is a portfolio project designed to explore how large-scale academic platforms can be built using modern backend engineering practices.

Instead of building a traditional monolithic application, this project adopts a microservices architecture where each business domain is developed, deployed, and maintained independently.

The goal is to understand not only application development, but also infrastructure, observability, scalability, and production-oriented system design.

---

## Architecture Principles

* Domain-driven service separation
* API Gateway pattern
* Centralized authentication and authorization
* Distributed tracing and monitoring
* Containerized deployment
* Infrastructure as Code
* Production-ready development workflow

---

## Technology Stack

### Backend

* Go (Golang)
* GORM (Auth Service)

### Data Layer

* PostgreSQL (Auth Service)
* Legacy SIAK SOAP services

### Infrastructure

* Docker
* Docker Compose
* Kong Gateway

### Frontend and authentication

* React, TypeScript, and Vite
* OAuth 2.0 / OpenID Connect
* JWT, JWKS, and scope-based authorization

### Observability

* OpenTelemetry
* Jaeger
* Prometheus

---

## Ecosystem

The repositories are connected as Git submodules. The system separates runtime
microservices from the frontend and reusable authentication libraries:

```text
Browser
  │
  ▼
UMMU Digital Campus ── @ganz404/js-auth
  │
  ▼
Kong API Gateway
  ├── UMMU Auth Service ── PostgreSQL
  │       └── issues tokens and publishes JWKS
  └── SIAK Legacy API ── legacy SIAK SOAP services
          └── validates tokens with ummu-go-auth
```

Infrastructure includes OpenTelemetry Collector and Prometheus configuration
for service observability.

### Infrastructure

| Module | Responsibility |
| --- | --- |
| [`api-getway/`](./api-getway/README.md) — `ummu-infrastructure` | Runs and configures Kong as the API gateway and contains Docker Compose, OpenTelemetry Collector, and Prometheus configuration. |

### Backend microservices

| Module | Responsibility |
| --- | --- |
| [`auth-service/`](./auth-service/README.md) — `ummu-auth-service` | Central authentication and authorization: local and Google OIDC login, JWT access and refresh tokens, client management, token validation, and role/permission-based access. |
| [`siak-legacy-api/`](./siak-legacy-api/README.md) — `Siak-Legacy-API` | Exposes selected legacy SIAK academic, portal, admissions, registration, payment, feeder, and mCampus operations as REST APIs. It validates access tokens and scopes before forwarding allowed requests to legacy services. |

### Frontend and shared authentication libraries

| Module | Responsibility |
| --- | --- |
| [`ummu-akademik-frontend/`](./ummu-akademik-frontend/README.md) — `ummu-akademik-frontend` | Browser SPA for login and role-based Developer, Finance, Administration, Student, and Lecturer portals. Calls backend APIs through the gateway. |
| [`ummu-js-auth/`](./ummu-js-auth/README.md) — `ummu-js-auth` | Browser SDK used by the frontend for service-managed Google login, session/token handling, token refresh, logout, and authenticated HTTP requests. It does not issue tokens. |
| [`ummu-go-outh/`](./ummu-go-outh/README.md) — `ummu-go-auth` | Reusable Go resource-server SDK for validating JWTs with JWKS and enforcing scopes in backend HTTP handlers. Token issuance remains the responsibility of Auth Service. |

### Planned services

Student, Lecturer, Academic, Finance, Payment, Notification, and BAAK services
can be added as separate backend microservices as their domains are developed.

---

## Why This Project Exists

Most portfolio projects stop at CRUD operations.

This project focuses on the challenges commonly found in real production systems:

* Service communication
* Authentication strategy
* API Gateway management
* Monitoring and observability
* Scalability considerations
* Infrastructure management

The objective is to gain hands-on experience with technologies and architectural patterns frequently used in modern backend environments.

---

## Current Status

The ecosystem currently includes gateway infrastructure, centralized
authentication, a REST adapter for legacy SIAK services, the browser frontend,
and shared Go and JavaScript authentication libraries. Additional academic
domains can be developed as independent services.

```git submodule update --init --recursive```

---

## Author

Agung Nurdin

Backend Developer • Golang • Microservices • Software Architecture • Rest Client • Javascript
