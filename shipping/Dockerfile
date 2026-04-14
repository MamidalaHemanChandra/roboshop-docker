FROM maven:3.9.11-eclipse-temurin-17 AS builder
WORKDIR /build
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests



FROM eclipse-temurin:17-jre-alpine
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=builder /build/target/shipping-1.0.jar app.jar
LABEL project="roboshop" \
      environment="dev" \
      created_by="heman"
ENV CART_ENDPOINT=cart:8080 \
    DB_HOST=mysql
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]



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