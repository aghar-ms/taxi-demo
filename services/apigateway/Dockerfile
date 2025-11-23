FROM vegardit/graalvm-maven:latest-java25 as builder

WORKDIR /apigateway

COPY pom.xml /apigateway/
COPY src /apigateway/src/
COPY mvnw /apigateway/
RUN chmod +x mvnw
RUN mvn package -Dmaven.test.skip
RUN chmod +x /apigateway/target/

FROM apache/beam_java25_sdk

COPY src/main/resources/application.properties ./
COPY --from=builder /apigateway/target/apigateway-0.0.1-SNAPSHOT.jar /apigateway/target/apigateway-0.0.1-SNAPSHOT.jar


CMD ["java", "-jar", "apigateway/target/apigateway-0.0.1-SNAPSHOT.jar", "--spring.config.location=/apigateway/target/application.properties,/apigateway/target/application.yml"]
