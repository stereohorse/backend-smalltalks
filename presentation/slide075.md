        
        ,---.          |    |
        |---',---.,---.|---.|    ,---.,-.-.,---.
        |    |    |   ||   ||    |---'| | |`---.
        `    `    `---'`---'`---'`---'` ' '`---'

        -- Configuration :: Spring Cloud Config Client --

        @Service
        public class SomeService {

          @Value("${awesome.config.value}")
          private String configValue;

          public void doSomething() {
            log.info("config value: {}", configValue);
          }
        }
















































































slide 075
