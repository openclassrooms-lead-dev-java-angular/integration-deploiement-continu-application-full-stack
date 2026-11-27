# ==================================================
# BACKEND DEVELOPMENT
# ==================================================
FROM gradle:jdk17

WORKDIR /src

# Gradle files copy for prepare dependencies
COPY gradlew ./
COPY gradle ./gradle
COPY build.gradle ./
COPY settings.gradle ./

RUN sed -i 's/\r$//' ./gradlew
RUN chmod +x ./gradlew

# Source code copy
COPY src ./src

# Spring Boot Port
EXPOSE 8080

# Start dévelopment mode
CMD ["./gradlew", "bootRun", "--no-daemon"]