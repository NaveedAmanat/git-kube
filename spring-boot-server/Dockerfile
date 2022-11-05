# our base build image
FROM maven:3.5-jdk-8 as maven

# copy the project files
COPY ./pom.xml ./pom.xml

# build all dependencies
RUN mvn dependency:go-offline -B

# copy your other files
COPY ./src ./src

# build for release
RUN mvn clean install #package

# our final base image
FROM openjdk:8-jdk-alpine

# set deployment directory
WORKDIR /my-project

# copy over the built artifact from the maven image
COPY --from=maven target/*.jar app.jar

# set the startup command to run your binary
CMD ["java", "-jar", "app.jar"]



#COPY ./target/spring-boot-jpa-h2-0.0.1-SNAPSHOT.jar /app
EXPOSE 8080
#CMD ["java", "-jar", "spring-boot-jpa-h2-0.0.1-SNAPSHOT.jar"]

