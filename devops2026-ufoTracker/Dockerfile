# MISSÃO 3 - Dockerfile da aplicação ufoTracker
# Java 21 + Spring Boot + Maven


# ETAPA 1: Build da aplicação
FROM eclipse-temurin:21-jdk-alpine AS build

WORKDIR /app

# Copia os arquivos do Maven
COPY .mvn/ .mvn/
COPY mvnw pom.xml ./

# Baixa as dependências primeiro (cache)
RUN ./mvnw dependency:go-offline -B

# Copia o código fonte
COPY src ./src

# Gera o JAR
RUN ./mvnw clean package -DskipTests


# ETAPA 2: Imagem final (mais leve)
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# Copia apenas o JAR gerado na etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Porta da aplicação Spring Boot
EXPOSE 8080

# Inicia a aplicação
ENTRYPOINT ["java", "-jar", "app.jar"]
