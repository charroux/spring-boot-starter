# spring-boot-starter

If you work in a company that develops shared libraries, or if you work on an open-source or commercial library, you might want to develop your own auto-configuration. Auto-configuration classes can be bundled in external jars and still be picked-up by Spring Boot: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html

## The library

Here is an example of a library you want to distribute: https://github.com/charroux/spring-boot-starter/tree/master/me-library

The main code of the library: https://github.com/charroux/spring-boot-starter/blob/master/me-library/src/main/java/me/Me.java

## Use the library in another project

The project is there: https://github.com/charroux/spring-boot-starter/tree/master/me-spring-boot-sample-app

Note how the library (class Me) is used in the main program (the library is injected with autoqired): https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-sample-app/src/main/java/me/MeApplication.java

The library is configured via a configuration file: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-sample-app/src/main/resources/application.properties

This project include a Spring Boot starter: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-sample-app/build.gradle

Note that the library is a local library (compile project(':me-spring-boot-starter')) and once it will be distrited as a maven library, you will use it through usual maven dependency like compile('...:me-spring-boot-starter-0.0.1-SNAPSHOT').

Easy to use, isn't it ?

Now let's have a look at the magic behind the scene.

## The auto configuration of the library

The configuration of the library is in another project: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-autoconfigure/src/main/java/MeAutoConfiguration.java

It tests if the library class is present: @ConditionalOnClass(Me.class)
And then the library is configured via properties: @EnableConfigurationProperties(MeProperties.class)

This last class is given along with the configuration: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-autoconfigure/src/main/java/me/MeProperties.java

This configuration is just a programmatic view of the property file: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-sample-app/src/main/resources/application.properties

## The starter

Finally the sarter is just a project: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-sample-app/src/main/resources/application.properties

with an empty jar file and a gradle file: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-sample-app/src/main/resources/application.properties
