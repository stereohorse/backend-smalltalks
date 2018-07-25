## Backend smalltalks

# Intro


# Context

```clojure
(def speaker {:name "Viet"
              :type ["java developer",
                     "infrastructure engineer"]})
```


# Context

```clojure
(def speaker {:name "Viet"
              :type ["java developer",
                     "infrastructure engineer"]})
```

- ololo
- Infrastructure components


# Context

```clojure
(def speaker {:name "Viet"
              :type ["java developer",
                     "infrastructure engineer"]})
```

- ololo
- Infrastructure components
- Applications specifics


# Infrastructure


# Infrastructure

- 3 Datacenters


# Infrastructure

- 3 Datacenters
- X Servers


# Infrastructure

- 3 Datacenters
- X Servers
- Y Apps


# Infrastructure

- 3 Datacenters
- X Servers
- Y Apps
- Z Teams


# Infrastructure

- 3 Datacenters
- X Servers
- Y Apps
- Z Teams

1 cluster -> 1 ops team


# Troubles!


# Troubles!

- how to distribute resources?


# Troubles!

- how to distribute resources?
- separate failure zones?


# Troubles!

- how to distribute resources?
- separate failure zones?
- keep services running?


# Troubles!

- how to distribute resources?
- separate failure zones?
- keep services running?
- coordinate rollouts?


# Troubles!

- how to distribute resources?
- separate failure zones?
- keep services running?
- coordinate rollouts?
- :(


# Troubles!

- how to distribute resources?
- separate failure zones?
- keep services running?
- coordinate rollouts?
- :(

Solution:

- Automate resources management! :D


# Resource managers


# Resource managers

Examples:

- Kubernetes


# Resource managers

Examples:

- Kubernetes
- Apache Mesos


# Resource managers

Examples:

- Kubernetes
- Apache Mesos
- Hashicorp Nomad


# Resource managers

Examples:

- Kubernetes
- Apache Mesos
- Hashicorp Nomad
- YARN


# Resource managers

Examples:

- Kubernetes
- Apache Mesos
- Hashicorp Nomad
- YARN
- Docker Swarm


# Resource managers

Examples:

- Kubernetes
- Apache Mesos
- Hashicorp Nomad
- YARN
- Docker Swarm
- Borg


# Resource managers

Examples:

- Kubernetes
- Apache Mesos
- Hashicorp Nomad
- YARN
- Docker Swarm
- Borg

Like Java memory management in large scale!


# RM components

- Agents on every computing node
- Masters for orchestration
- Storage


# Apache Mesos

```
   
      
 
 
 
+------------------+    +------------------+    +------------------+
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
    
    
    
    
     
+------------------+    +------------------+    +------------------+
|   +----------+   |    |   +----------+   |    |   +----------+   |
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |
|   +----------+   |    |   +----------+   |    |   +----------+   |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
     
                         +----------------+
                         | Masters Quorum |
                         +----------------+

+------------------+    +------------------+    +------------------+
|   +----------+   |    |   +----------+   |    |   +----------+   |
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |
|   +----------+   |    |   +----------+   |    |   +----------+   |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
     
                         +----------------+
          ...............| Masters Quorum |................
          :              +----------------+               :
          :                       :                       :
+---------:--------+    +---------:--------+    +---------:--------+
|   +----------+   |    |   +----------+   |    |   +----------+   |
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |
|   +----------+   |    |   +----------+   |    |   +----------+   |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
                                                                        
                         +----------------+
          ...............| Masters Quorum |................
          :              +----------------+               :                +-----------+  
          :                       :                       :                | Scheduler | 
+---------:--------+    +---------:--------+    +---------:--------+       +-----------+
|   +----------+   |    |   +----------+   |    |   +----------+   |
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |
|   +----------+   |    |   +----------+   |    |   +----------+   |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
                                                                        
                         +----------------+.......................................
          ...............| Masters Quorum |................                      :
          :              +----------------+               :                +-----------+  
          :                       :                       :                | Scheduler | 
+---------:--------+    +---------:--------+    +---------:--------+       +-----------+
|   +----------+   |    |   +----------+   |    |   +----------+   |
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |
|   +----------+   |    |   +----------+   |    |   +----------+   |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
                                                                       
                         +----------------+.......................................        
          ...............| Masters Quorum |................                      :        
          :              +----------------+               :                +-----------+  
          :                       :                       :                | Scheduler |  
+---------:--------+    +---------:--------+    +---------:--------+       +-----------+  
|   +----------+   |    |   +----------+   |    |   +----------+   | 
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   | 
|   +----------+   |    |   +----------+   |    |   +----------+   | 
|                  |    |                  |    |                  |
|   +----------+   |    |   +----------+   |    |   +----------+   | 
|   | Executor |   |    |   | Executor |   |    |   | Executor |   | 
|   +----------+   |    |   +----------+   |    |   +----------+   | 
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
                                                                       
                         +----------------+.......................................        
          ...............| Masters Quorum |................                      :        
          :              +----------------+               :                +-----------+  
          :                       :                       :                | Scheduler |  
+---------:--------+    +---------:--------+    +---------:--------+       +-----------+  
|   +----------+   |    |   +----------+   |    |   +----------+   | 
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   | 
|   +----------+   |    |   +----------+   |    |   +----------+   | 
|         :        |    |         :        |    |         :        |
|   +-----:----+   |    |   +-----:----+   |    |   +-----:----+   | 
|   | Executor |   |    |   | Executor |   |    |   | Executor |   | 
|   +----------+   |    |   +----------+   |    |   +----------+   | 
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
                                                                        ...................
                         +----------------+.............................:.........        :
          ...............| Masters Quorum |................             :        :        :
          :              +----------------+               :             :  +-----------+  :
          :                       :                       :             :  | Scheduler |  :
+---------:--------+    +---------:--------+    +---------:--------+    :  +-----------+  :
|   +----------+   |    |   +----------+   |    |   +----------+   |    :                 :
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |    :                 :
|   +----------+   |    |   +----------+   |    |   +----------+   |    :                 :
| ........:........|....|.........:........|....|.........:........|....:                 :
| : +-----:----+   |    |   +-----:----+   |    |   +-----:----+   |                      :
| : | Executor |   |    |   | Executor |   |    |   | Executor |   |                      :
| : +----------+   |    |   +----------+   |    |   +----------+   |                      :
| :................|....|..................|....|..................|..........[Framework].:
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
                                                                        ...................
                         +----------------+.............................:.........        :
          ...............| Masters Quorum |................             :        :        :
          :              +----------------+               :             :  +-----------+  :
          :                       :                       :             :  | Scheduler |  :
+---------:--------+    +---------:--------+    +---------:--------+    :  +-----------+  :
|   +----------+   |    |   +----------+   |    |   +----------+   |    :                 :
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |    :                 :
|   +----------+   |    |   +----------+   |    |   +----------+   |    :                 :
| ........:........|....|.........:........|....|.........:........|....:                 :
| : +-----:----+   |    |   +-----:----+   |    |   +-----:----+   |                      :
| : | Executor |   |    |   | Executor |   |    |   | Executor |   |                      :
| : +----------+   |    |   +----------+   |    |   +----------+   |                      :
| :................|....|..................|....|..................|..........[Framework].:
|   +----------+   |    |   +----------+   |    |                  |
|   | App 1    |   |    |   | App 2    |   |    |                  |
|   +----------+   |    |   +----------+   |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```


# Apache Mesos

```
                                                                        ...................
                         +----------------+.............................:.........        :
          ...............| Masters Quorum |................             :        :        :
          :              +----------------+               :             :  +-----------+  :
          :                       :                       :             :  | Scheduler |  :
+---------:--------+    +---------:--------+    +---------:--------+    :  +-----------+  :
|   +----------+   |    |   +----------+   |    |   +----------+   |    :                 :
|   | Agent 1  |   |    |   | Agent 2  |   |    |   | Agent 3  |   |    :                 :
|   +----------+   |    |   +----------+   |    |   +----------+   |    :                 :
| ........:........|....|.........:........|....|.........:........|....:                 :
| : +-----:----+   |    |   +-----:----+   |    |   +-----:----+   |                      :
| : | Executor |   |    |   | Executor |   |    |   | Executor |   |                      :
| : +----------+   |    |   +----------+   |    |   +----------+   |                      :
| :................|....|..................|....|..................|..........[Framework].:
|   +----------+   |    |   +----------+   |    |                  |
|   | App 1    |   |    |   | App 2    |   |    |                  |
|   +----------+   |    |   +----------+   |    |                  |
|                  |    |                  |    |                  |
+---------[Node 1]-+    +---------[Node 2]-+    +---------[Node 3]-+
```

- ololo
- Storage & Leader election -> Zookeeper


# Concepts


# Concepts

- Agents & masters govern all cluster resources


# Concepts

- Agents & masters govern all cluster resources
- Masters offer resources to frameworks


# Problems


# Problems 

-- Communications --


# Problems

-- Communications --

- Discovery


# Problems

-- Communications --

- Discovery
- Load Balancing


# Problems

-- Communications --

- Discovery
- Load Balancing
- Circuit breaker


# Problems

-- Communications --

- Discovery
- Load Balancing
- Circuit breaker
- Ingress routing


# Problems

-- Communications --

- Discovery
- Load Balancing
- Circuit breaker
- Ingress routing
- Rate limiting


# Problems

-- Communications --

- Discovery
- Load Balancing
- Circuit breaker
- Ingress routing
- Rate limiting
- ...


# Problems

-- Communications :: Discovery --


# Problems

-- Communications :: Discovery --

- Consul + Nginx


# Problems

-- Communications :: Discovery --

- Consul + Nginx
- Marathon-lb


# Problems

-- Communications :: Discovery --

- Consul + Nginx
- Marathon-lb
- Spring Cloud Eureka


# Spring Cloud


# Spring Cloud

```groovy
dependencies {
  compile 'org.springframework.cloud:spring-cloud-starter-config'
  compile 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-client'
  compile 'org.springframework.cloud:spring-cloud-starter-netflix-ribbon'

  compile 'org.springframework.cloud:spring-cloud-stream-binder-kafka-streams'
  compile 'org.springframework.cloud:spring-cloud-starter-stream-kafka'
  compile 'org.springframework.cloud:spring-cloud-starter-bus-kafka'

  // ...
}
```


# Spring Cloud

- Config
- Netflix
- Bus
- Stream
- Sleuth
- ...


# Spring Cloud

-- Release Trains --

- Spring Boot 1 -> Edgware.SR4
- Spring Boot 2 -> Finchley.RELEASE


# Problems

-- Discovery :: Spring Cloud Eureka Server --


# Problems

-- Discovery :: Spring Cloud Eureka Server --

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaServer {
  
  public static void main(String... args) {
    SpringApplication.run(EurekaServer.class, args);
  }
}
```


# Problems

-- Discovery :: Spring Cloud Eureka Client --

```java
@SpringBootApplication
@EnableDiscoveryClient
@RestController
public class EurekaClient {

  @Autowired
  private DiscoveryClient discoveryClient;

  @PostMapping
  public void logFirstService() {
    List<ServiceInstance> instances = this.discoveryClient.getInstances("another-service-name");

    ServiceInstance firstInstance = instances.get(0);
    log.info("service host: {}", firstInstance.getHost());
    log.info("service port: {}", firstInstance.getPort());
  }
  
  public static void main(String... args) {
    SpringApplication.run(EurekaClient.class, args);
  }
}
```


# Problems

-- Communications --

- Discovery
- Load Balancing
- Ingress routing
- Circuit breaker
- Rate limiting


# Problems

-- Communications --

- Discovery          :: Eureka
- Load Balancing
- Ingress routing
- Circuit breaker
- Rate limiting


# Problems

-- Load balancing :: Ribbon + Feign (SB 1) --

```java
@FeignClient("another-service-name")
public interface SomeClient {

  @GetMapping("/some/endpoint")
  Data getData();
}

@RestController
public class EurekaServer {

  @Autowired
  private SomeClient someClient;

  @PostMapping
  public void callService() {
    someClient.getData();
  }
}
```


# Problems

-- Communications --

- Discovery          :: Eureka
- Load Balancing
- Ingress routing
- Circuit breaker
- Rate limiting


# Problems

-- Communications --

- Discovery          :: Eureka
- Load Balancing     :: Ribbon + Feign
- Ingress routing
- Circuit breaker
- Rate limiting


# Problems

-- Discovery :: Zuul --

```java
@SpringBootApplication
@EnableZuulProxy
public class ZuulServer {
  
  public static void main(String... args) {
    SpringApplication.run(ZuulServer.class, args);
  }
}
```

```yaml
--
zuul:
  routes:
    rule1:
      path: "/some/service/**"
      serviceId: another-service-name
```


# Problems

-- Communications --

- Discovery          :: Eureka
- Load Balancing     :: Ribbon + Feign
- Ingress routing
- Circuit breaker
- Rate limiting


# Problems

-- Communications --

- Discovery          :: Eureka
- Load Balancing     :: Ribbon + Feign
- Ingress routing    :: Zuul
- Circuit breaker
- Rate limiting


# Problems

-- Circuit breaker :: Hystrix --

```java
@Service
public class HystrixExample {

  @Autowired
  private SomeClient someClient;

  @HystrixCommand(fallbackMethod = "reliable")
  public Data callService() {
    return someClient.getData(); 
  }

  public String reliable() {
    return "Cloud Native Java (O'Reilly)";
  }
}
```


# Problems

-- Rate limiting :: Hystrix --

```yaml
hystrix.command:
  SomeAction:
    hystrix.threadpool.default:
      coreSize: 10
      maximumSize: 13
      maxQueueSize: 1000
```


# Problems

-- Communications --

- Discovery          :: Eureka
- Load Balancing     :: Ribbon + Feign
- Ingress routing    :: Zuul
- Circuit breaker
- Rate limiting


# Problems

-- Communications --

- Discovery          :: Eureka
- Load Balancing     :: Ribbon + Feign
- Ingress routing    :: Zuul
- Circuit breaker    :: Hystrix
- Rate limiting      :: Hystrix


# Problems

-- Configuration --

- Config storage
- Properties overload
- Reload


# Problems

-- Configuration :: Spring Cloud Config Server --

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerExample {
  
  public static void main(String... args) {
    SpringApplication.run(ConfigServerExample.class, args);
  }
}
```


# Problems

-- Configuration :: Spring Cloud Config Client --

```java
@Service
public class SomeService {
  
  @Value("${awesome.config.value}")
  private String configValue;

  public void doSomething() {
    log.info("config value: {}", configValue);
  }
}
```


# Problems

-- Configuration --

- Config storage
- Properties overload
- Reload


# Problems

-- Configuration --

- Config storage        :: Config Server
- Properties overload   :: Config Client
- Reload


# Problems

-- Configuration --

- Config storage        :: Config Server
- Properties overload   :: Config Client
- Reload                :: Bus


# Problems

-- Configuration --

- Config storage        :: Config Server
- Properties overload   :: Config Client
- Reload                :: Just restart!


# Problems

- Communications


# Problems

- Communications
- Configuration


# Problems

- Communications
- Configuration
- Visibility
- Security
- Deployments
- Resilency
- State storage
- API design
- ...

