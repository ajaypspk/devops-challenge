FROM openjdk:11-jdk
ADD target/spring-boot-rest-1.0-SNAPSHOT.jar /code/app.jar
WORKDIR /code/
EXPOSE 8080
ENV MYSQL_DATABASE=""
CMD ["java", "-jar", "/code/app.jar"]
