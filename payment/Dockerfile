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

# ---------- Stage 1: Build ----------
FROM python:3.9-slim AS builder

WORKDIR /build

# Install build dependencies only here
RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

# Install dependencies into a custom directory
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt


# ---------- Stage 2: Runtime ----------
FROM python:3.9-slim

# Create non-root user
RUN useradd -m -r roboshop

WORKDIR /opt/server

# Copy installed dependencies from builder
COPY --from=builder /install /usr/local

# Copy app files
COPY payment.ini .
COPY *.py .

# Set environment variables
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

# Change ownership to roboshop user
RUN chown -R roboshop:roboshop /opt/server

# Switch to non-root user
USER roboshop

EXPOSE 8080

CMD ["uwsgi", "--ini", "payment.ini"]