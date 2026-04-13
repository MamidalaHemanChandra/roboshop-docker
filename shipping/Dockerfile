FROM maven:3.9.11 AS builder
WORKDIR /opt/server
COPY pom.xml .
COPY src ./src
RUN mvn clean package 


FROM alpine:3.20
RUN apk add --no-cache openjdk17-jre
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /home/roboshop
COPY --from=builder /opt/server/target/shipping-1.0.jar shipping.jar
LABEL project="roboshop" \
      environment="dev" \
      created_by="heman"
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
RUN chown -R roboshop:roboshop /home/roboshop
USER roboshop
EXPOSE 8080
CMD ["java", "-jar", "shipping.jar"]
# FROM eclipse-temurin:17-jdk-alpine
# CMD ["sh", "-c", "sleep 30 && java -jar shipping.jar"]


# FROM maven:3.9.11
# EXPOSE 8080
# WORKDIR /opt/server
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package 
# RUN mv target/shipping-1.0.jar shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD ["java","-jar","shipping.jar"]