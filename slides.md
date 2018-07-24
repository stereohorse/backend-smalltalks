## Backend smalltalks

# Intro


# Context


# Context

- Infrastructure components


# Context

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

Examples:

- Google's Kubernetes
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


# Concepts

- Agents & masters govern all cluster resources
- Masters offer resources to frameworks


# Problems

-- Communications --

- Discovery
- Load Balancing
- Circuit breaker
- Ingress routing
- Rate limiting
- Collocation


# Problems

-- Communications :: Discovery --

- Consul + Nginx
- Marathon-lb
- Spring Cloud Eureka


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

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaServer {
  
  public static void main(String... args) {
    SpringApplication.run(ApplicationDelivery.class, args);
  }
}
```


# Problems

-- Discovery :: Spring Cloud Eureka Client --

```java
@SpringBootApplication
@EnableDiscoveryClient
@RestController
public class EurekaServer {

  @Autowired
  private DiscoveryClient discoveryClient;

  @PostMapping
  public void callService() {
    this.discoveryClient.getInstances("another-service-name");
  }
  
  public static void main(String... args) {
    SpringApplication.run(ApplicationDelivery.class, args);
  }
}
```

