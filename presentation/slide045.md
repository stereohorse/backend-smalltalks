        '||''|.                  '||      '||
         ||   || ... ..    ...    || ...   ||    ....  .. .. ..    ....
         ||...|'  ||' '' .|  '|.  ||'  ||  ||  .|...||  || || ||  ||. '
         ||       ||     ||   ||  ||    |  ||  ||       || || ||  . '|..
        .||.     .||.     '|..|'  '|...'  .||.  '|...' .|| || ||. |'..|'






        -- Circuit breaker & Rate limiting :: Hystrix --

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
















































































slide 045
