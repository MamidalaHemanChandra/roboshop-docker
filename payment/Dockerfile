# FROM python:3.9-alpine AS builder
# WORKDIR /install
# RUN apk add --no-cache gcc musl-dev libffi-dev
# COPY requirements.txt .
# RUN pip install --prefix=/install/deps -r requirements.txt


# FROM python:3.9-alpine
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# WORKDIR /opt/server
# COPY --from=builder /install/deps /usr/local
# COPY payment.ini .
# COPY *.py .
# RUN chown -R roboshop:roboshop /opt/server
# USER roboshop
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# EXPOSE 8080
# CMD ["uwsgi", "--ini", "payment.ini"]



FROM python:3.9
EXPOSE 8080
WORKDIR /opt/server
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip3 install -r requirements.txt
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123" 
CMD ["uwsgi", "--ini", "payment.ini"]