FROM eclipse-temurin:17 AS builder
WORKDIR workspace
ARG JAR_FILE=target/serviceB-0.0.1-SNAPSHOT.jar
COPY ${JAR_FILE} serviceB.jar
RUN java -Djarmode=layertools -jar serviceB.jar extract

FROM eclipse-temurin:17
RUN useradd spring
USER spring
WORKDIR workspace
COPY --from=builder workspace/dependencies/ ./
COPY --from=builder workspace/spring-boot-loader/ ./
COPY --from=builder workspace/snapshot-dependencies/ ./
COPY --from=builder workspace/application/ ./
ENTRYPOINT ["java", "org.springframework.boot.loader.JarLauncher"]