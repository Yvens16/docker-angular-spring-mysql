FROM eclipse-temurin:21-jdk as base

WORKDIR /workspace/app
VOLUME /tmp

COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src
RUN ./mvnw dependency:resolve

FROM base as dev
CMD ["./mvnw", "spring-boot:run"]

# To add at the end of the presentation
FROM base as test
CMD ["./mvnw", "test"]

FROM base as build
RUN ./mvnw package

FROM eclipse-temurin:21-jre-jammy as production
COPY --from=build /workspace/app/target/backend-0.0.1-SNAPSHOT.jar backend.jar
CMD ["java", "-jar", "/backend.jar"]