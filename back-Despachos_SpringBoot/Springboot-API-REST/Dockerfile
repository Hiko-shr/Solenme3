# Etapa 1: Compilación usando una imagen oficial de Maven
FROM maven:3.8.5-eclipse-temurin-17 AS build
WORKDIR /app

# Copiamos solo el pom.xml y el código fuente (¡Adiós .mvn!)
COPY pom.xml ./
COPY src ./src

# Compilamos el proyecto usando el Maven oficial
RUN mvn clean package -DskipTests

# Etapa 2: Imagen final ligera
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8082
ENTRYPOINT ["java", "-jar", "app.jar"]
