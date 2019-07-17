# Spring Cloud Cheat sheet

# Microservices
- Similar to design pattern to a service-oriented architecture
- More encapsulated domains but still loosely coupled
- Single domain, single purpose services
- Decomposition at an application instead of a component

# External Configuration
- Uses 12-factor methodologies
- Increase portability and scalability
- Removes need for environment variables

# Config server
- Version control on configuration
- Easier management and staging
- Centralized management of variables

# Spring Cloud Config Server
- Simple Spring Boot Starter project
- Is tied directly to a git repo
- Loads config on startup and serves it via REST
- Provides support to branches and Spring profiles


boostrap.properties -> load before application.properties
-> use to store config server uri

# Service Discovery Eureka
- Both a sonsole and discovery platform
- Nextflix contributed
- REST-based service
- Nextflix-contributed client

# Why Eureka
- Clean interface for registration and interface
- Default round-robin load balancing in client
- Easy integration with Spring


# Eureka Server
- Similar to Config Server
- Easy build-in dashboard supports replication

# Feign
- @FeignClient(value="user-service")

# The Circuit Breaker Pattern
- Isolation from failure
- Pattern builds resiliency into applications
- It wraps remote calls with a circuit breaker than can trip
- Tripped circuit can prevent other calls from falling

# Hystrix
- Is a Nextflix project to implement the circuit breaker
- Work seamlessly with Feign
- Includes a console application
- Includes client-side functionality

## Hystrix implementation
- @EnableCircuitBreaker
- add config: feign.hystrix.enable=true
- adding fallback -> to the impl service

## Hystrix dashboard