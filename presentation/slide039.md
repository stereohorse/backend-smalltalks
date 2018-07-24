        '||''|.                  '||      '||
         ||   || ... ..    ...    || ...   ||    ....  .. .. ..    ....
         ||...|'  ||' '' .|  '|.  ||'  ||  ||  .|...||  || || ||  ||. '
         ||       ||     ||   ||  ||    |  ||  ||       || || ||  . '|..
        .||.     .||.     '|..|'  '|...'  .||.  '|...' .|| || ||. |'..|'






        -- Load balancing :: Ribbon + Feign (SB 1) --

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
















































































slide 039
