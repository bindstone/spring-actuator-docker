FROM maven:3.6-jdk-8-alpine as server-builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:resolve
COPY . .
RUN mvn clean install

FROM openjdk:8-jdk-alpine
WORKDIR /app
VOLUME /tmp
COPY --from=server-builder /app/target/actuator-server.jar /app/actuator-server.jar
ENTRYPOINT ["java","-jar","./actuator-server.jar"]