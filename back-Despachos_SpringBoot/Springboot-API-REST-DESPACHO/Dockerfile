# Etapa 1: construcción del proyecto con Maven y Java 17
FROM maven:3.9.9-eclipse-temurin-17 AS build

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

# Etapa 2: imagen final liviana para ejecutar la aplicación
FROM eclipse-temurin:17-jre

WORKDIR /app

# Crear usuario no root por seguridad
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser

COPY --from=build /app/target/*.jar app.jar

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]