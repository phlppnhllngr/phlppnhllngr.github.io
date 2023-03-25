---
title: Build
parent: Spring
grand_parent: Java
---

# Build

## Maven-Plugin
- <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/>
- <https://www.baeldung.com/spring-boot-repackage-vs-mvn-package>
- Goals
  - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#?> 
  - run
    - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#goals-run> 
  - build-image
    - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#goals-build-image>
    - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#build-image.customization>
    - <https://www.baeldung.com/spring-boot-docker-images#buildpacks> 
  - repackage
    - *Repackage existing JAR and WAR archives so that they can be executed from the command line using java -jar. With layout=NONE can also be used simply to package a JAR with nested dependencies (and no main class, so not executable).*
    - `mvn clean package spring-boot:repackage`
- <https://odedia.org/production-considerations-for-spring-on-kubernetes>
  - custom layers 


## Cloud Native Buildpacks
- <https://www.heise.de/hintergrund/Container-Images-Abschied-vom-Dockerfile-5997535.html?seite=3>
  - layered Jar, Buildpacks, beides in Kombination
- <https://dev.to/sabyasachi/buildpack-with-spring-boot-300o>
  - erklärt Builder, Buildpacks
  - *Spring uses Packeto buildpack*
  - *By default packeto uses bellsoft-liberica java distribution*
  - native-image
  - Buildpack-Parameter
  - *Buildpacks are opinionated and like any opinionated tech it gives us some defaults*
- <https://www.heise.de/hintergrund/Container-Images-Abschied-vom-Dockerfile-5997535.html?seite=2>
  - Spring Boot, Paketo-CLI (pack), Paketo-Konfig (buildpack.yaml), Bindings
- <https://eggboy.medium.com/creating-spring-boot-images-with-cloud-native-buildpacks-for-azure-container-platforms-62c7a6f187de>
  - Buildpacks+JMX, Java-Version
- <https://odedia.org/production-considerations-for-spring-on-kubernetes>
  - *On container startup, it will set production-ready defaults for JAVA_TOOL_OPTIONS, taking into account user-provided environment variables and the memory calculation*
  - *If you're still using Spring Boot 2.3, the resulting image will not use the layered approach. In Spring Boot 2.4 and later, this is the default. In order to gain the benefits of better OCI layering in 2.3, you'll need to provide the following configuration in your pom.xml: <layers><enabled>true...*
  - *In Spring Boot 2.4 and above, there's an additional enhancement you get for free: The build-image process will also remove all the spring-boot-starter jars from the target image. These are really only needed at compilation time and not at runtime, so removing them results in smaller images and in better performance.*
  - *In Spring Boot 2.4 and above, you can configure your own custom registry for the target resulting image. Spring Boot will push the image to the remote registry for you as part of the build process*
  - *Starting in Spring Boot 2.5 and later - you can also customize the buildpack that is used to create the resulting image.*
- <https://github.com/jonashackt/spring-boot-buildpack>
  - *Example project showing how to use Buildpacks.io together with Spring Boot & it's layered jar feature*

### Konfig
- **build command** (Maven, Gradle)
  - <https://paketo.io/docs/howto/java/#specify-the-build-command>
- **remote debugging**
  - <https://paketo.io/docs/howto/java/#enable-remote-debugging>
- **jmx**
  - <https://paketo.io/docs/howto/java/#enable-jmx>
- **java**
  - *`BP_JVM_VERSION` Defaults to the latest 11.x version at the time of release.*
  - <https://paketo.io/docs/howto/java/#install-a-specific-jvm-version>
- **jlink**
  - *`BP_JVM_JLINK_ENABLED` - this defaults to false, set to true to enable JLink`
  - <https://paketo.io/docs/howto/java/#install-a-minimal-jre-with-jlink>
- **run args**
  - <https://paketo.io/docs/howto/java/#append-arguments-to-the-apps-start-command>
