# Spring Boot 2 cheat sheet
- rapid to development and speed to market
- self-contained application
- Fits with 12 factors culture
- Property-based configurations

## Annotations
@EnableAutoConfiguration: allows for configuration classes to be scanned dynamically

@ConditionalOnClass

@ConditionalOnBean

@ConditionalOnProperty

@ConditionalOnMissingBean

### @Controller

### @RestController
@RestController = @Controller + @ResponseBody

### @ControllerAdvice



## Profiles
- Flex config based on environment
- Valuable in real world, multi-environment deployment
- Active profile can be injected via command line (spring.profiles.active)
    ```
    java -jar -Dspring.profiles.active=dev
    ```


## spring-boot-stater-web
### Tomcat: 
- default embedded
- default config
- can change to Jetty if preferred

### JSON Marshaller
### Slf4J



# Packaging
## The Springboot JAR file:
- Default behavior is JAR packaging
- Produces a "fat jar": not only contains source code, but also all dependencies that the source code rely on
- Executable
- Registrable with systemd or init.d

# Springboot support WAR file 
Just some config as bellow:
- Modify build (set maven package to WAR)
- Exclude spring-boot-starter-tomcat from spring-boot-starter-web

# Running Springboot application
- java -jar
- shell scripts
- *nix systemd or init.d
- Cloud ecosystem

# Deployment WAR and JAR:
- Running WAR file: running in other process in Tomcat, Weblogic...
- Running JAR file: it becomes the process and the embedded Tomcat become part of it


# Twelve-Factor application
- Modern paradigm
- Rapid development, spped to market
- Move to microservices from monoliths
- Fits devops culture


# CommandLineRunner interface
- Provide access to application arguments
- Run a single tasks

### ApplicationRunner


# SpringBoot Starters
## Spring Data: spring-boot-starter-data-jpa
- Rich support both RDBMS and NoSQL
- Rich database drivers
- Support embedded database: H2, HSQLDB autoconfig
- Springboot will auto config data source

## Spring Security: spring-boot-starter-security
- Give basic authentication on all endpoints
- Extends WebSecurityConfigurerAdapter
- @EnableWebSecurity
- Full support for OAuth2
- @EnableOAuth2Client
- @EnableAuthorizationServer
- @EnableResourceServer
- Password should always be hashed, not encrypted
- Hash: SHA-1 should be considered

# Springboot messaging
- RabbitMQ
- Rabbit template with default configs


# AutoConfiguration
- @EnableAutoConfiguration: spring.factories
- @Conditional
- @ConditionalOnMissionBean(aaa.class): only load if missing
- @EnableConfigurationProperties
- @ConfigurationProperties(prefix="aaa")

# Create own spring boot starter
## Why need?
- Common code
- Common configuration
- Improve easy of use

# Springboot Actuator
- Provides insights into running application
- Provides configuration settings
- Allow to monitors running application

## Feautes:
- Health endpoints: sattus of app, status of dependencies
- Info endpoints
- JMX functionality: Beans, Env, Heapdump/threaddump, mappings (list all web urls), metrics
- Secure actuator
- Admin management endpoints: show/hide endpoints to users

## The info endpoint
- show all configs start with "info.*"
- Add build Plugin to show commit and artifact into:

## The health endpoint
- Config: management.endpoint.health.show-details=when_authorized
- Can show status of app, diskpace, db, database type...
- HealthIndicator interface: to customize health of application

## Metrics endpoint
- Endpoint: /actuator/metrics -> to show all available metrics
- Start with: management.metrics.*
- Ex: register new metric and monitor the value:
    + add @Timed (from io.micrometer.core.annotation) to the method
    + add Counter
    + register the counter with the metric registry: MeterRegistry
    + navigate to the /metrics you can see the metric
    
## Custom Endpoint
- Create a component with @Endpoint(id="abc-xyz")
- Add method with @Data annotation
- Add @ReadOperation bean
- Details at: https://www.linkedin.com/learning/spring-boot-2-essential-training/custom-endpoints

## Others
- /beans -> show all JMX beans
- /auditevents
- /conditions -> see all conditions bean
- /configprops
- /env
- /loggers -> show all log level info, can use JMX endpoint to change the log level
- /threaddump
- /heapdump
- /httptrace
- /mappings