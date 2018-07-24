        '||''|.                  '||      '||
         ||   || ... ..    ...    || ...   ||    ....  .. .. ..    ....
         ||...|'  ||' '' .|  '|.  ||'  ||  ||  .|...||  || || ||  ||. '
         ||       ||     ||   ||  ||    |  ||  ||       || || ||  . '|..
        .||.     .||.     '|..|'  '|...'  .||.  '|...' .|| || ||. |'..|'






        -- Discovery :: Spring Cloud Eureka Client --

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
















































































slide 036
