        '||''|.                  '||      '||
         ||   || ... ..    ...    || ...   ||    ....  .. .. ..    ....
         ||...|'  ||' '' .|  '|.  ||'  ||  ||  .|...||  || || ||  ||. '
         ||       ||     ||   ||  ||    |  ||  ||       || || ||  . '|..
        .||.     .||.     '|..|'  '|...'  .||.  '|...' .|| || ||. |'..|'






        -- Discovery :: Zuul --

        @SpringBootApplication
        @EnableZuulProxy
        public class ZuulServer {

          public static void main(String... args) {
            SpringApplication.run(ZuulServer.class, args);
          }
        }

        --
        zuul:
          routes:
            rule1:
              path: "/some/service/**"
              serviceId: another-service-name
















































































slide 042
