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

This simple example define only one auto configuration but a more realistic one will combine many autoconfigurations. All the configurations should be listed in the spring factories file : https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-autoconfigure/src/main/resources/META-INF/spring.factories

## The starter

Finally the starter is another project: https://github.com/charroux/spring-boot-starter/tree/master/me-spring-boot-starter

with an empty jar file and a just gradle file: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-starter/build.gradle

## The main project

All those projects are linked together is the main one: https://github.com/charroux/spring-boot-starter

Note that the sample project using the library is just there for testing purpose and it should not be part of the whole library.

The gradle file of this main project is: https://github.com/charroux/spring-boot-starter/blob/master/build.gradle

It contains only the main Spring Boot library.

All the projects are configured there: https://github.com/charroux/spring-boot-starter/blob/master/settings.gradle

## Build all the project

Use gradlew build or ./gradlew build from a terminal opened from the root folder.

Then import this multiple project inside Eclipse or Intellij and launch the main program: https://github.com/charroux/spring-boot-starter/blob/master/me-spring-boot-sample-app/src/main/java/me/MeApplication.java

Enjoy ;-)
