        '||''|.                  '||      '||
         ||   || ... ..    ...    || ...   ||    ....  .. .. ..    ....
         ||...|'  ||' '' .|  '|.  ||'  ||  ||  .|...||  || || ||  ||. '
         ||       ||     ||   ||  ||    |  ||  ||       || || ||  . '|..
        .||.     .||.     '|..|'  '|...'  .||.  '|...' .|| || ||. |'..|'






        -- Discovery :: Spring Cloud Eureka Client --

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
















































































slide 036
