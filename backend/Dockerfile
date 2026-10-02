FROM maven:3.9-eclipse-temurin-17 AS build
ARG BRANCH=v3.9.5
WORKDIR /src
RUN git clone --depth 1 --branch ${BRANCH} https://github.com/jeecgboot/JeecgBoot.git .
WORKDIR /src/jeecg-boot
RUN mvn -q clean package -DskipTests -pl jeecg-module-system/jeecg-system-start -am

FROM eclipse-temurin:17-jre
ENV TZ=Asia/Shanghai
WORKDIR /jeecg-boot
COPY --from=build /src/jeecg-boot/jeecg-module-system/jeecg-system-start/target/jeecg-system-start-*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
