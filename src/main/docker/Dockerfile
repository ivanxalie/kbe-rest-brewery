FROM openjdk:11-jre-slim as builder
WORKDIR app
ADD maven/${project.build.finalName}.jar .
RUN java -Djarmode=layertools -jar ${project.build.finalName}.jar extract

FROM openjdk:11-jre-slim
WORKDIR app

COPY --from=builder app/dependencies .
COPY --from=builder app/spring-boot-loader .
COPY --from=builder app/snapshot-dependencies .
COPY --from=builder app/application .
ENTRYPOINT ["java", "-Djava.security.edg=file:/dev/./urandom", "org.springframework.boot.loader.JarLauncher"]