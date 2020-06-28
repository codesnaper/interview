Microservices are a way of breaking large software projects into loosely coupled modules, which communicate with each other through simple Application Programming Interfaces (APIs).
Simply stated, microservices are really nothing more than another architectural solution for designing complex – mostly web-based – applications. Microservices have gained most importance as an evolution from SOA (Service Oriented Architecture), an approach that was designed to overcome the disadvantages of traditional monolithic architectures

### Advantage
-   **Improved fault isolation**: Larger applications can remain mostly unaffected by the failure of a single module.
-   **Eliminate vendor or technology lock-in**: Microservices provide the flexibility to try out a new technology stack on an individual service as needed. There won’t be as many dependency concerns and rolling back changes becomes much easier. With less code in play, there is more flexibility.
-   **Ease of understanding:** With added simplicity, developers can better understand the functionality of a service.
-   **Smaller and faster deployments**: Smaller codebases and scope = quicker deployments, which also allow you to start to explore the benefits of Continuous Deployment.****
-   **Scalability**: Since your services are separate, you can more easily scale the most needed ones at the appropriate times, as opposed to the whole application. When done correctly, this can impact cost savings.****

### Disadvantage:
-   **Communication between services is complex**: Since everything is now an independent service, you have to carefully handle requests traveling between your modules. In one such scenario, developers may be forced to write extra code to avoid disruption. Over time, complications will arise when remote calls experience latency.
-   **More services equals more resources**: Multiple databases and transaction management can be painful.
-   **Global testing is difficult**: Testing a microservices-based application can be cumbersome. In a monolithic approach, we would just need to launch our WAR on an application server and ensure its connectivity with the underlying database. With microservices, each dependent service needs to be confirmed before testing can occur.
-   **Debugging problems can be harder**: Each service has its own set of logs to go through. Log, logs, and more logs.
-   **Deployment challengers**: The product may need coordination among multiple services, which may not be as straightforward as deploying a WAR in a container.
-   **Large vs small product companies**: Microservices are great for large companies, but can be slower to implement and too complicated for small companies who need to create and iterate quickly, and don’t want to get bogged down in complex orchestration.


# Design Pattern:

## Service Discovery:
**Problem**: How can clients find microservices and their instances?
Microservices instances are typically assigned dynamically allocated IP addresses when they start up, for example, when running in containers. This makes it difficult for a client to make a request to a microservice that,

**Solution**
-   Automatically register/unregister microservices and their instances as they come and go.
-   The client must be able to make a request to a logical endpoint for the microservice. The request will be routed to one of the microservices available instances.
-   Requests to a microservice must be load-balanced over the available instances.
-   We must be able to detect instances that are not currently healthy; that is, requests will not be routed to them.

**Note**
-   **Client-side routing**: The client uses a library that communicates with the service discovery service to find out the proper instances to send the requests to.
-   **Server-side routing**: The infrastructure of the service discovery service also exposes a reverse proxy that all requests are sent to. The reverse proxy forwards the requests to a proper microservice instance on behalf of the client.

###   Spring cloud : *Netflix Eureka* as a discovery service

#### Problem WIth DNS-Based service discovery
If i set up two instance of service with 2 different IP and map to DNS name and if we call with DNS name and hit the url we will always get response from first of service. A DNS client typically caches the resolved IP addresses and hangs on to the first working IP address it tries out when it receives a list of IP addresses that have been resolved for a DNS name. Neither the DNS servers nor the DNS protocol is well-suited for handling volatile microservices instances that come and go all of the time. Because of this, DNS-based service discovery isn't very appealing from a practical standpoint.

#### few Challenges:
-   New instances can start up at any point in time.
-   Existing instances can stop responding and eventually crash at any point in time.
-   Some of the failing instances might be okay after a while and should start to receive traffic again, while others will not and should be removed from the service registry.
-   Some microservice instances might take some time to start up; that is, just because they can receive HTTP requests doesn't mean that traffic should be routed to them.
-   Unintended network partitioning and other network-related errors can occur at any time.

####  Netflix Eureka working:
1.  Whenever a microservice instance starts up—for example, the  **Review**  service—it registers itself to one of the Eureka servers.
2.  On a regular basis, each microservice instance sends a heartbeat message to the Eureka server, telling it that the microservice instance is okay and is ready to receive requests.
3.  Clients service—use a client library that regularly asks the Eureka service for information about available services.
4.  When the client needs to send a request to another microservice, it already has a list of available instances in its client library and can pick one of them without asking the discovery server. Typically available instances are chosen in a round-robin fashion; that is, they are called one after another before the first one is called once more. 

Spring Cloud comes with an abstraction of how to communicate with a discovery service such as Netflix Eureka and provides an interface called **DiscoveryClient**.
Spring Cloud also has  **DiscoveryClient implementations** that support the use of either Apache Zookeeper or HashiCorp Consul as a discovery server.
Spring Cloud also comes with an abstraction—the **LoadBalancerClient  interface**for clients that want to make requests through a load balancer to registered instances in the discovery service

#### Configuration Eureka Server with service:
1. Add dependency: `spring-cloud-starter-netflix-eureka-server`
2. Add the `@EnableEurekaServer` annotation to the application class.
3. Add the project to Docker file project Name: spring-cloud/eureka-server
```markup
eureka:
  build: spring-cloud/eureka-server
  mem_limit: 350m
  ports:
      - "8761:8761"
```
#### Connecting microservices to a Netflix Eureka server
1. Add a dependency to `spring-cloud-starter-netflix-eureka-client`
2. Add a load balancer-aware WebClient builder in the client.
	```
	@Bean  
	@LoadBalanced  
	public WebClient.Builder loadBalancedWebClientBuilder() {  
	   final WebClient.Builder builder = WebClient.builder();  
	 return builder;  
	}
	```
	The @LoadBalanced  annotation will, as described previously,  result in that Spring will inject a load balancer-aware filter into the  WebClient.Builder  bean
3. We have to create a webclient which is going to create an outgoing Http request
	```
	private WebClient getWebClient() {  
	    if (webClient == null) {  
	        webClient = webClientBuilder.build();  
		  }  
	    return webClient;  
	}
	```
4. Whenever we want to send any get or post request we can do be getWebClient()
	```
		private Mono<Health> getHealth(String url) {  
	    url += "/actuator/health";  
		LOG.debug("Will call the Health API on URL: {}", url);  
		 return getWebClient().get().uri(url).retrieve().bodyToMono(String.class)  
        .map(s -> new Health.Builder().up().build())  
        .onErrorResume(ex -> Mono.just(new Health.Builder().down(ex).build()))  
        .log();  
	}
	```
5. we will no longer have to keep ip and port of the service we can remove instead we will only keep the virtual hostname which is been used by microservice to register with eureka server which is value of `the spring.application.name property`.
	`http://${spring.application.name}`

**Configuring EurekaCLient Setting**
```
eureka:
  client:
      serviceUrl: 
  defaultZone: http://localhost:8761/eureka/
  initialInstanceInfoReplicationIntervalSeconds: 5 
  registryFetchIntervalSeconds: 5
  instance:
  leaseRenewalIntervalInSeconds: 5 
  leaseExpirationDurationInSeconds: 5

	---
spring.profiles: docker
eureka.client.serviceUrl.defaultZone: http://eureka:8761/eureka/


ribbon.ServerListRefreshInterval:5000
ribbon.NFLoadBalancerPingInterval: 5
```

**Configuring Eureka Server**
```
eureka:  
  instance:  
    hostname: localhost  
  client:  
    registerWithEureka: false  
    fetchRegistry: false  
    serviceUrl:  
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/  
  # from: https://github.com/spring-cloud-samples/eureka/blob/master/src/main/resources/application.yml  
  server:  
    waitTimeInMsWhenSyncEmpty: 0  
    response-cache-update-interval-ms: 5000  
  
management.endpoints.web.exposure.include: "*"
```

## Edge Server
### Problem:
In a system landscape of microservices, it is in many cases desirable to expose some of the microservices to the outside of the system landscape and hide the remaining microservices from external access. The  exposed microservices must be protected against requests from malicious clients.

### Solution:
-   Hide internal services that should not be exposed outside their context; that is, only route requests to microservices that are configured to allow external requests.
-   Expose external services and protect them from malicious requests; that is, use standard protocols and best practices such as OAuth, OIDC, JWT tokens, and API keys to ensure that the clients are trustworthy.

### Spring Cloud Gateway
![Spring Cloud Gateway Architecture](https://docs.google.com/drawings/d/1komYs1pERhc1G8OXxn1-NMGuY2T_CRP9FaqRkTbjFho/edit?usp=sharing)

1. Add a dependency to  `spring-cloud-starter-gateway`
2. Since the edge server will handle all incoming traffic, we will move the composite health check from the other composite service to the edge server. This is described in _Adding a composite health check_ section.
```
package se.magnus.springcloud.gateway;  
  
import org.slf4j.Logger;  
import org.slf4j.LoggerFactory;  
import org.springframework.beans.factory.annotation.Autowired;  
import org.springframework.boot.actuate.health.*;  
import org.springframework.context.annotation.Bean;  
import org.springframework.context.annotation.Configuration;  
import org.springframework.web.reactive.function.client.WebClient;  
import reactor.core.publisher.Mono;  
  
import java.util.LinkedHashMap;  
  
@Configuration  
public class HealthCheckConfiguration {  
  
    private static final Logger LOG = LoggerFactory.getLogger(HealthCheckConfiguration.class);  
  
 private HealthAggregator healthAggregator;  
  
 private final WebClient.Builder webClientBuilder;  
  
 private WebClient webClient;  
  
  @Autowired  
    public HealthCheckConfiguration(  
        WebClient.Builder webClientBuilder,  
  HealthAggregator healthAggregator  
    ) {  
        this.webClientBuilder = webClientBuilder;  
 this.healthAggregator = healthAggregator;  
  }  
  
    @Bean  
    ReactiveHealthIndicator healthcheckMicroservices() {  
  
        ReactiveHealthIndicatorRegistry registry = new DefaultReactiveHealthIndicatorRegistry(new LinkedHashMap<>());  
  
  registry.register("product", () -> getHealth("http://product"));  
  registry.register("recommendation", () -> getHealth("http://recommendation"));  
  registry.register("review", () -> getHealth("http://review"));  
  registry.register("product-composite", () -> getHealth("http://product-composite"));  
  
 return new CompositeReactiveHealthIndicator(healthAggregator, registry);  
  }  
  
    private Mono<Health> getHealth(String url) {  
        url += "/actuator/health";  
  LOG.debug("Will call the Health API on URL: {}", url);  
 return getWebClient().get().uri(url).retrieve().bodyToMono(String.class)  
            .map(s -> new Health.Builder().up().build())  
            .onErrorResume(ex -> Mono.just(new Health.Builder().down(ex).build()))  
            .log();  
  }  
  
    private WebClient getWebClient() {  
        if (webClient == null) {  
            webClient = webClientBuilder.build();  
  }  
        return webClient;  
  }  
}
```
3. Configure Spring cloud gateway:
```
  
management.endpoint.health.show-details: "ALWAYS"  
management.endpoints.web.exposure.include: "*"  
  
logging:  
  level:  
    root: INFO  
    org.springframework.cloud.gateway.route.RouteDefinitionRouteLocator: INFO  
    org.springframework.cloud.gateway: TRACE
spring.cloud.gateway.routes:  
  
- id: product-composite  
  uri: lb://product-composite  
  predicates:  
  - Path=/product-composite/**
- id: product-composite  
  uri: lb://product-composite  
  predicates:  
  - Path=/product-composite/**
  - Cookie=mycookie,mycookievalue
  - Header=X-Request-Id, \d+
  filters:
	- AddRequestParameter=red, blue
	- AddResponseHeader=X-Response-Red, Blue
```
Where in cloud gateway.route properties:
**Route**: The basic building block of the gateway. It is defined by an ID, a destination URI, a collection of predicates, and a collection of filters. A route is matched if the aggregate predicate is true.
**Predicate** : Similar to java 8 predicate function.This lets you match on anything from the HTTP request, such as headers or parameters.
**Filter**: These are instances of [Spring Framework  `GatewayFilter`](https://docs.spring.io/spring/docs/5.0.x/javadoc-api/org/springframework/web/server/GatewayFilter.html) that have been constructed with a specific factory. Here, you can modify requests and responses before or after sending the downstream request.

**Internal Implementation of cloud gateway**
![Internal Implementation of cloud gateway](https://docs.google.com/drawings/d/1x4VkizbSWpm_bDmXeyjNwIwjyws6jMecYIj56GPmynA/edit?usp=sharing)


## Central Configuration:
An application is, traditionally, deployed together with its configuration, for example, a set of environment variables and/or files containing configuration information.  Given a system landscape based on a microservice architecture, that is, with a large number of deployed microservice instances, some queries arise:

-   How do I get a complete picture of the configuration that is in place for all the running microservice instances?
-   How do I update the configuration and make sure that all the affected microservice instances are updated correctly?

### Solution:
Make it possible to store configuration information for a group of microservices in one place, with different settings for different environments

### Spring Cloud  Configuration  Server
![Diagram](https://docs.google.com/drawings/d/1oKNfLG27xUECrBaffbQFWi5MxidAa_lwPq8A1DDAfdQ/edit?usp=sharing)

While to setup config server there are lot of option to consider:
-   Selecting a storage type for the configuration repository
	 -   Git repository
	-   Local filesystem
	-   HashiCorp Vault
	-   A JDBC database
-   Deciding on the initial client connection, either to the config server or to the discovery server
	- By default, a client connects first to the config server to retrieve its configuration. Based on the configuration, it connects to the discovery server, that is, Netflix Eureka in our case, to register itself. It is also possible to do this the other way around, that is, the client first connects to the discovery server to find a config server instance and then connects to the config server to get its configuration. There are pros and cons to both approaches.

	- if the clients will first connect to the config server. With this approach, it will be possible to store the configuration of the discovery server, that is, Netflix Eureka, in the config server.
-   Securing the configuration, both against unauthorized access to the API and  avoiding storing sensitive information in plain text in the configuration repository


**Configuring the spring cloud configuration server**
1. Create a new project and include dependencies: `spring-cloud-config-server`
2. Add the annotation, `@EnableConfigServer`, to the application class
```
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {
```
3. Add the configuration:
```markup
spring.cloud.config.server.native.searchLocations: file:${PWD}/config-repo
```
4. *Optional* if we want To be able to access the API of the config server from outside the microservice landscape, we add a routing rule to the edge server
```markup
 - id: config-server
 - uri: http://${app.config-server}:8888
 - predicates:  - Path=/config/**
 - filters:  - RewritePath=/config/(?<segment>.*), /$\{segment}
```
The RewritePath filter in the preceding routing rule will remove the leading part, /config, from the incoming URL before it sends it to the config server.

5. Configure our service to get configuration from config server
	1. in our service add dependencies: `spring-cloud-starter-config` and `spring-retry`
	2. Move the configuration file, application.yml, to the config repository and rename it to the name of the client as specified by the property, spring.application.name.
	3. Add a file named bootstrap.yml to the src/main/resources  folder. This file holds the configuration required to connect to the config server. and provide the connection configuration:
	```
	cloud.config:
	    failFast: true    
	    retry:      
		    initialInterval: 3000      
		    multiplier: 1.3      
		    maxInterval: 10000      
		    maxAttempts: 20
	    uri: http://${CONFIG_SERVER_USR}:${CONFIG_SERVER_PWD}@${app.config-server}:8888
	```
	5. If to connect to config server we need any credential we can add them as an enviornment variable, so add the variable in docker file
	```
	product:  environment: -
		CONFIG_SERVER_USR=${CONFIG_SERVER_USR} - 	
		CONFIG_SERVER_PWD=${CONFIG_SERVER_PWD}
	```
Working:
1.  Connect to the config server using the  http://localhost:8888  URL when it runs outside Docker, and using the  http://config-server:8888  URL when running in a Docker container.
2.  Use HTTP basic authentication using the value of the CONFIG_SERVER_USR  and  CONFIG_SERVER_PWD properties, as its username and password.
3.  Try to reconnect to the config server during startup up to 20 times, if required.
4.  If the connection attempt fails, the client will initially wait for 3 seconds before trying to reconnect.
5.  The wait time for subsequent retries will increase by a factor of 1.3.
6.  The maximum wait time between connection attempts will be 10 seconds.
7.  If the client can't connect to the config server after 20 attempts, its startup will fail.		


## Circuit Breaker:
A system landscape of microservices that uses synchronous intercommunication can be exposed to a  _chain of failure_. If one microservice stops responding, its clients might get into problems as well and stop responding to requests from their clients. The problem can propagate recursively throughout a system landscape and take out major parts of it.

### Solution:
-   Open the circuit and fail fast (without waiting for a timeout) if problems with the service are detected.
-   Probe for failure correction (also known as a  **half-open circuit**); that is, allow a single request to go through on a regular basis to see if the service operates normally again.
-   Close the circuit if the probe detects that the service operates normally again. This capability is very important since it makes the system landscape resilient to these kinds of problems; that is, it self-heals.
![Circuit Breaker diagram](https://docs.google.com/drawings/d/1xbqLnbBH0Ko3VlXuKBZiaD1ai10FDsuzbSSVjtFIzSc/edit?usp=sharing)

### Resilience4j
Resilience4j can be used by all our microservices except for the edge server since Spring Cloud Gateway currently only supports the older circuit breaker, Netflix Hystrix.

Working:
![Daigram](https://docs.google.com/drawings/d/1620rLz59KkDf2sBbIHOkuePmszIriUjkdTOC6FDHC1k/edit?usp=sharing)
1. 1.  A circuit breaker starts as  **Closed**, that is, allowing requests to be processed.
2.  As long as the requests are processed successfully, it stays in the  **Closed**  state.
3.  If failures start to happen, a counter starts to count up.
4.  If a configured threshold of failures is reached, the circuit breaker will  **trip**, that is, go to the  **Open**  state, not allowing further requests to be processed.
5.  Instead, a request will **fast fail**, that is,  return immediately with an exception. This means that it doesn't wait for a new fault, for example, a timeout, to happen on subsequent calls. Instead, it directly redirects the call to a **fallback**  **method**. The fallback method can apply various business logic to produce the best effort response. For example, a fallback method can return data from a local cache or simply return an immediate error message. This will prevent a microservice from getting unresponsive if the services it depends on stop responding normally. This is specifically useful under high load.
6. 1.  After a configurable time, the circuit breaker will enter a **Half Open** state and allow one request to go through, such as a probe, to see whether the failure has been resolved.
7.  If the probe request fails, the circuit breaker goes back to the  **Open**  state.
8.  If the probe request succeeds, the circuit breaker goes to the initial  **Closed**  state, that is, allowing new requests to be processed.

#### Resilience4j  exposes information about circuit breakers at runtime in a number of ways:
-   The current state of a circuit breaker can be monitored using the microservice's actuator health  endpoint, /actuator/health.
-   The circuit breaker also publishes events on an  actuator  endpoint, for example, state transitions,  /actuator/circuitbreakerevents.
-   Finally, circuit breakers are integrated with Spring Boot's metrics system and can use it to publish metrics to monitoring tools such as Prometheus.

#### Resilience4J Configuration Parameter:
-   `ringBufferSizeInClosedState`: Number of calls in a closed state, which are used to determine whether the circuit shall be opened.
-   `failureRateThreshold`: The threshold, in percent, for failed calls that will cause the circuit to be opened.
-   `waitInterval`: Specifies how long  the circuit stays in an open state, that is, before it transitions to the half-open state.
-   `ringBufferSizeInHalfOpenState`: The number of calls in the half-open state that are used to determine whether the circuit shall be opened again or go back to the normal, closed state.
-   `automaticTransitionFromOpenToHalfOpenEnabled`: Determines whether the circuit automatically will transition to half-open once the wait period is over or wait for the first call after the waiting period until it transitions to the half-open state.
-   `ignoreExceptions`: Can be used to specify exceptions that should not be counted as faults. Expected business exceptions such as not found or invalid input are typical exceptions that the circuit breaker should ignore, that is, users that search for non-existing data or enter invalid input should not cause the circuit to open.

#### Introducing the retry mechanism
Resilience4j exposes retry information in the same way as it does for circuit breakers when it comes to events and metrics but does not provide any health information. Retry events are accessible on the  actuator  endpoint, /actuator/retryevents
-   `maxRetryAttempts`: Number of retries before giving up, including the first call
-   `waitDuration`: Wait time before the next retry attempt
-   `retryExceptions`: A list of exceptions that shall trigger a retry
