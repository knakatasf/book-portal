# ---- Build (multi-arch) ----
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /usr/src/app
COPY pom.xml .
RUN mvn -B -q -DskipTests dependency:go-offline
COPY src ./src
RUN mvn -B -q -DskipTests clean package

# ---- Run (multi-arch) ----
FROM eclipse-temurin:17-jre
WORKDIR /usr/app
COPY --from=build /usr/src/app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/app/app.jar"]

#FROM maven:3.8-openjdk-18 AS build
#COPY src /usr/src/app/src
#COPY pom.xml /usr/src/app
#RUN mvn -f /usr/src/app/pom.xml clean package
#
#FROM openjdk:18-alpine
#COPY --from=build /usr/src/app/target/BookPortal-0.0.1-SNAPSHOT.jar /usr/app/BookPortal-0.0.1-SNAPSHOT.jar
#EXPOSE 8080
#ENTRYPOINT ["java","-jar","/usr/app/BookPortal-0.0.1-SNAPSHOT.jar"]
