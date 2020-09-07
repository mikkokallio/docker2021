#TBA

FROM openjdk:8
COPY . /usr/src/myapp
WORKDIR /usr/src/myapp
RUN ./mvnw package && java -jar ./target/docker-example-1.1.3.jar
EXPOSE 8080 
