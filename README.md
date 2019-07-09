# Annotations

@Configuration

@Bean

@Import

@PropertySource("classpath:/application.properties")

@Value("${config.text.from.application.properties}")

@Profile("dev")
spring.profiles.active=dev
or: application-dev.properties

@Profile("prod")
spring.profiles.active=prod
or: application-prod.properties

-> @PropertySource("classpath:/application-${spring.profiles.active}.properties")

# Spring Expression Language
@Value("#{new Boolean(environment['spring.profiles.active']=='dev'}")
private boolean isDev;

# Bean Scope
- Singletons
- Prototype
- Session -> Web only
- Request -> Web only

-> Definition is stored in bean factory, instances are not


How to config? 
@Bean
@Scope("singleton")
@Scope("prototype")

# Proxies
Everything is a Proxy since Spring 4.0

