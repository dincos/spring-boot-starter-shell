spring-boot-start-shell
=======================
Spring Shell with Spring Boot Driven

### How to use

* Add spring-boot-starter-shell dependency in application's pom.xml: 

```xml
    <dependency>
       <groupId>org.mvnsearch.spring.boot</groupId>
       <artifactId>spring-boot-starter-shell</artifactId>
       <version>1.0.0-SNAPSHOT</version>
    </dependency>
```

* Add Spring Boot Maven Plugin in your pom.xml: 

```xml
   <plugin>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-maven-plugin</artifactId>
       <version>1.4.0.RELEASE</version>
       <executions>
           <execution>
               <goals>
                   <goal>repackage</goal>
               </goals>
           </execution>
       </executions>
       <configuration>
           <!-- do not enable it, this will creats a non standard jar and cause autoconfig to fail -->
           <executable>false</executable>
       </configuration>
   </plugin>
```

* Add following code in your Spring Boot Application main method:

```
    @SpringBootApplication
    public class DemoApplication {
    
        public static void main(String[] args) {
            SpringShellApplication.run(DemoApplication.class, args);
        }
    }
```

* Of course, create your Spring Shell commands.

```
@Component
public class HelloCommands implements CommandMarker {
    @CliCommand(value = "hello", help = "CMS ")
    public String hello() {
        return "hello";
    }
}
```

* Build your application and run it.

```
   $ mvn -DskipTests clean package
   $ java -jar target/xxxx.jar
```

### Tips

* Possible Configuration in your application.properties: 

```properties
spring.main.banner-mode=off
```

* logback-spring.xml configuration to mute some log: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

    <!--stdout appender-->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="ERROR">
        <appender-ref ref="CONSOLE"/>
    </root>

</configuration>
```


### Todo

Migrate to: https://github.com/spring-cloud/spring-cloud-dataflow/blob/master/spring-cloud-dataflow-shell-core/src/main/java/org/springframework/cloud/dataflow/shell/autoconfigure/BaseShellAutoConfiguration.java

### References

* Spring Shell Document: http://docs.spring.io/spring-shell/docs/current/reference/htmlsingle/
* ASCII Generator: http://www.network-science.de/ascii/
