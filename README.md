# Spring Boot & Spring Cloud Microservices Project

## Overview
This project demonstrates how to build a complete microservices architecture using **Spring Boot** and **Spring Cloud**. It covers essential tools and patterns for building scalable, maintainable, and production-ready microservices.

## Features
- **Microservices with Separate Databases**: Employee, Department, Organization services — each backed by Postgres SQL.
- **Centralized Configuration**: Spring Cloud Config Server storing configs in a Git repository.
- **Service Discovery**: Eureka Server for dynamic registration and discovery.
- **Distributed Tracing**: Spring Cloud Sleuth for correlation IDs, Zipkin UI for visualization.
- **API Gateway**: Spring Cloud Gateway for routing and cross-cutting concerns.
- **Frontend Integration**: React application as a microservice, consuming APIs via the gateway.

## Tech Stack
- Java, Spring Boot, Spring Cloud
- PostGres, Hibernate, Spring Data JPA
- Eureka, Config Server, API Gateway
- Sleuth, Zipkin
- React

## Learning Goals
- Build REST APIs with Spring Boot
- Implement service-to-service communication
- Use Spring Cloud tools to manage configurations and discovery
- Apply distributed tracing in microservices
- Integrate a React frontend with backend microservices
