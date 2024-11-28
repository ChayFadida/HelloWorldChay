# Stage 1: Build the application using Maven
FROM maven:3.8.4-openjdk-11-slim AS build
WORKDIR /app
COPY pom.xml /app/
COPY src /app/src
RUN mvn package -DskipTests


# Stage 2: Build the final image
FROM adoptopenjdk:11-jre-hotspot
WORKDIR /app
RUN groupadd -r appuser && useradd -r -g appuser appuser
COPY --from=build /app/target/myapp*.jar /app/myapp.jar
RUN chown appuser:appuser /app/myapp.jar
RUN chmod 755 /app/myapp.jar
USER appuser
EXPOSE 8080
CMD ["java", "-jar", "/app/myapp.jar"]
