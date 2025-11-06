# ./back/Dockerfile (option B - recommandée)
# --- build stage (maven + jdk) ---
FROM maven:3.8.8-openjdk-11-slim AS build
WORKDIR /workspace

# copier d'abord pom.xml pour profiter du cache Docker
COPY pom.xml .
COPY src ./src

# Build (skip tests ici)
RUN mvn -B -f pom.xml clean package -DskipTests

# --- runtime stage (plus léger, Temurin) ---
FROM eclipse-temurin:11-jre-jammy
WORKDIR /app

# Copier le jar depuis la phase de build
COPY --from=build /workspace/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
