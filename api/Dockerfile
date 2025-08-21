FROM --platform=${BUILDPLATFORM} maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY ./src /src
RUN mvn clean package -DskipTests

FROM openjdk:11-ea-17-jre
WORKDIR /app
COPY --from=Build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]