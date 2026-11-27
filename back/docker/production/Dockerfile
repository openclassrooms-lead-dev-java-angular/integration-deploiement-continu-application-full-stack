# ==================================================
# BACKEND BUILD
# ==================================================
FROM gradle:jdk17 AS build

WORKDIR /src

# Copy of the backend project
COPY . ./

RUN sed -i 's/\r$//' ./gradlew

# Compiling and generating the JAR
RUN chmod +x ./gradlew \
    && ./gradlew clean bootJar --no-daemon


# ==================================================
# BACKEND RUNTIME
# ==================================================
FROM eclipse-temurin:17-jre-jammy

WORKDIR /app

# Compiled JAR copy
COPY --from=build --chown=10001:10001 \
    /src/build/libs/microcrm-0.0.1-SNAPSHOT.jar \
    /app/app.jar

# Execution without root privileges
USER 10001:10001

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app/app.jar"]