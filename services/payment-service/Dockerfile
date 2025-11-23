FROM vegardit/graalvm-maven:latest-java25 as builder

WORKDIR /payment

COPY pom.xml /payment/
COPY src /payment/src/
COPY mvnw /payment/
RUN chmod +x mvnw
RUN mvn package -Dmaven.test.skip
RUN chmod +x /payment/target/

FROM apache/beam_java25_sdk

COPY src/main/resources/application.properties ./
COPY --from=builder /payment/target/payment-0.0.1-SNAPSHOT.jar /payment/target/payment-0.0.1-SNAPSHOT.jar


CMD ["java", "-jar", "payment/target/payment-0.0.1-SNAPSHOT.jar", "--spring.config.location=/payment/target/application.properties,/payment/target/application.yml"]