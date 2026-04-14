FROM python:3.9-alpine AS builder
WORKDIR /opt/server
RUN apk add --no-cache \
    gcc \
    musl-dev \
    python3-dev \
    linux-headers
RUN pip install --upgrade pip
COPY requirements.txt .
RUN pip install --prefix=/install -r requirements.txt


FROM python:3.9-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder /install /usr/local
COPY payment.ini .
COPY *.py .
EXPOSE 8080
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]

# FROM python:3.9-alpine AS builder
# WORKDIR /opt/server
# RUN apk add --no-cache \
#     build-base \
#     python3-dev \
#     linux-headers
# COPY requirements.txt .
# RUN python -m venv /opt/venv
# ENV PATH="/opt/venv/bin:$PATH"
# RUN pip3 install --upgrade pip && \
#     pip3 install -r requirements.txt


# FROM python:3.9-alpine
# WORKDIR /opt/server
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123" \
#     PATH="/opt/venv/bin:$PATH"
# COPY --from=builder /opt/venv /opt/venv
# COPY --chown=roboshop:roboshop payment.ini .
# COPY --chown=roboshop:roboshop *.py .
# EXPOSE 8080
# LABEL project="roboshop" \
#       component="payment" \
#       created="heman"
# USER roboshop
# ENTRYPOINT ["uwsgi", "--ini", "payment.ini"]


# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123" 
# CMD ["uwsgi", "--ini", "payment.ini"]