# Capstone Project Platform

This repository contains the three infrastructure components required by the Capstone Project microservices architecture:

* Config Server
* Service Registry
* API Gateway

The three applications are maintained as separate repositories and included here as **Git submodules**. This allows the complete platform to be cloned and deployed together on a cloud VM.

## Platform Components

| Component        | Port | Purpose                   |
| ---------------- | ---: | ------------------------- |
| Config Server    | 9000 | Centralized configuration |
| Service Registry | 9001 | Service discovery         |
| API Gateway      | 7000 | API routing               |

## Project Structure

```text
Capstone-Project-Platform/
│
├── config-server/
├── service-registry/
├── api-gateway/
│
├── .gitmodules
├── ecosystem.config.js
└── pom.xml
```

## Config Server

The Config Server loads application configuration from the separate configuration repository.

```text
Port: 9000
```

It provides configuration to both the platform components and business services.

Configuration repository:

```text
Capstone-Project-Configurations
```

## Service Registry

The Service Registry uses **Netflix Eureka** for service discovery.

```text
Port: 9001
```

The business services register themselves with Eureka, allowing the API Gateway to discover them without depending on fixed service IP addresses.

## API Gateway

The API Gateway is the main entry point for backend API requests.

```text
Port: 7000
```

Main routes:

```text
/api/v1/students/**
/api/v1/programs/**
/api/v1/enrollments/**
```

The Gateway uses Eureka service discovery and load-balanced service names to forward requests to the correct microservice.

## Clone

Clone the repository together with its submodules:

```bash
git clone --recurse-submodules https://github.com/DuliniPrabhashini/Capstone-Project-Platform.git
```

## Run

Recommended startup order:

```text
1. Config Server       : 9000
2. Service Registry    : 9001
3. API Gateway         : 7000
4. Business Services  : 8000 - 8002
```

Individual applications can be started using:


## Cloud Deployment

This repository is intended to make deployment easier by keeping the three platform applications together.

A cloud VM can be prepared with:

```bash
git clone --recurse-submodules https://github.com/DuliniPrabhashini/Capstone-Project-Platform.git
cd Capstone-Project-Platform
./mvnw clean install
```
