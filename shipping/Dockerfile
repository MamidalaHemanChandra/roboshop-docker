# FROM maven:3.9.11 AS builder
# WORKDIR /opt/server
# COPY pom.xml . 
# COPY src ./src
# RUN mvn clean package 


# FROM eclipse-temurin:17-jdk-alpine
# WORKDIR /opt/server
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop \
#     && chown -R roboshop:roboshop /opt/server
# # COPY --from=builder /opt/server/target/shipping-1.0.jar shipping.jar
# COPY --from=builder /opt/server/target/*.jar shipping.jar
# USER roboshop
# EXPOSE 8080
# LABEL project="roboshop" \
#       environment="dev" \
#       created_by="heman"
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# # CMD ["java", "-jar", "shipping.jar"]
# CMD ["sh", "-c", "sleep 30 && java -jar shipping.jar"]


FROM maven:3.9.11
EXPOSE 8080
WORKDIR /opt/server
COPY pom.xml .
COPY src ./src
RUN mvn clean package 
RUN mv target/shipping-1.0.jar shipping.jar
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
CMD ["java", "-jar", "shipping.jar"]