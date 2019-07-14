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

@Autowired
@Qualifier

# Autowiring
- Field Level -> Don't do this because you cannot control the construction of you object -> cannot mock in Unit Test
- Setter Injection: used for optional dependencies or changing dependencies
- Constructor Injection -> this is the prefered method, with this you class becomes immutable -> get perfect encapsulation

# Lifecycle
- @PostConstruct: specify a single method to execute after construction
- @PreDestroy: execute when ApplicationContext closes

There are 3 phases:
- Initialisation
- Use
- Destruction

Lazy and Eager:
- Eager: by default
- Lazy: can be config by annotation, but only bean without dependencies can be lazy

ApplicationContextAware: to handle ApplicationContext
BeanFactory
BeanPostProcessor: https://stackoverflow.com/questions/29743320/how-exactly-does-the-spring-beanpostprocessor-work


@ComponentScan

# Spring Expression Language
@Value("#{new Boolean(environment['spring.profiles.active']=='dev'}")
private boolean isDev;

# Bean Scope
- Singletons (default)
- Prototype
- Session -> Web only
- Request -> Web only

-> Definition is stored in bean factory, instances are not

### Prototype Bean
Prototype beans are not impacted by the destruction phase either. Because a prototype bean no longer is handled by the application context once it's constructed, they go out of scope immediately when the application class itself no longer needs them
https://stackoverflow.com/questions/50681027/do-spring-prototype-beans-need-to-be-destroyed-manually

```
There is one quite important thing to be aware of when deploying a bean in the prototype scope, in that the lifecycle of the bean changes slightly. Spring does not manage the complete lifecycle of a prototype bean: the container instantiates, configures, decorates and otherwise assembles a prototype object, hands it to the client and then has no further knowledge of that prototype instance. This means that while initialization lifecycle callback methods will be called on all objects regardless of scope, in the case of prototypes, any configured destruction lifecycle callbacks will not be called. It is the responsibility of the client code to clean up prototype scoped objects and release any expensive resources that the prototype bean(s) are holding onto. (One possible way to get the Spring container to release resources used by prototype-scoped beans is through the use of a custom bean post-processor which would hold a reference to the beans that need to be cleaned up.)

In some respects, you can think of the Spring containers role when talking about a prototype-scoped bean as somewhat of a replacement for the Java 'new' operator. All lifecycle aspect past that point have to be handled by the client. (The lifecycle of a bean in the Spring container is further described in the section entitled Section 4.5.1, “Lifecycle callbacks”.)

```


How to config? 
@Bean
@Scope("singleton")
@Scope("prototype")

# Proxies
Everything is a Proxy since Spring 4.0

