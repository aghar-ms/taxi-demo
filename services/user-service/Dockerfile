FROM vegardit/graalvm-maven:latest-java25 as builder

WORKDIR /user

COPY pom.xml /user/
COPY src /user/src/
COPY mvnw /user/
RUN chmod +x mvnw
RUN mvn package -Dmaven.test.skip
RUN chmod +x /user/target/

FROM apache/beam_java25_sdk

COPY src/main/resources/application.properties ./
COPY --from=builder /user/target/user-0.0.1-SNAPSHOT.jar /user/target/user-0.0.1-SNAPSHOT.jar


CMD ["java", "-jar", "user/target/user-0.0.1-SNAPSHOT.jar", "--spring.config.location=/user/target/application.properties,/user/target/application.yml"]