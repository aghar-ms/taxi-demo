FROM vegardit/graalvm-maven:latest-java25 as builder

WORKDIR /trip

COPY pom.xml /trip/
COPY src /trip/src/
COPY mvnw /trip/
RUN chmod +x mvnw
RUN mvn package -Dmaven.test.skip
RUN chmod +x /trip/target/

FROM apache/beam_java25_sdk

COPY src/main/resources/application.properties ./
COPY --from=builder /trip/target/trip-0.0.1-SNAPSHOT.jar /trip/target/trip-0.0.1-SNAPSHOT.jar


CMD ["java", "-jar", "trip/target/trip-0.0.1-SNAPSHOT.jar", "--spring.config.location=/trip/target/application.properties,/trip/target/application.yml"]