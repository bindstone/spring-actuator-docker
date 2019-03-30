FROM maven:3.6-jdk-8-alpine as client-builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:resolve
COPY . .
RUN mvn clean install

FROM openjdk:8-jdk-alpine
WORKDIR /app
VOLUME /tmp
COPY --from=client-builder /app/target/actuator-client.jar /app/actuator-client.jar
ENTRYPOINT ["java","-jar","./actuator-client.jar"]