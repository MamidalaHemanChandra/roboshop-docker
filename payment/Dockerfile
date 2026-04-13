# FROM python:3.9-alpine AS builder
# WORKDIR /opt/server
# RUN apk add --no-cache \
#     build-base \
#     linux-headers \
#     pcre-dev \
#     musl-dev \
#     libffi-dev
# COPY requirements.txt .
# RUN pip install --no-cache-dir --prefix=/install -r requirements.txt


# FROM python:3.9-alpine
# WORKDIR /opt/server
# RUN apk add --no-cache \
#     libstdc++ \
#     pcre
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# COPY --from=builder /install /usr/local
# COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt .
# USER appuser
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
COPY *.txt .
RUN pip3 install -r requirements.txt
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123" 
CMD ["/usr/local/bin/uwsgi", "--ini", "payment.ini"]