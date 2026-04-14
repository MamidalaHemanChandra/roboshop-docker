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

# ---- Stage 1: Build dependencies ----
FROM python:3.9-slim AS builder

WORKDIR /opt/server

# Install build tools (if needed for compiling packages)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential gcc \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for caching
COPY requirements.txt .

# Install dependencies into a temporary folder
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# ---- Stage 2: Final runtime image ----
FROM python:3.9-slim

# Create roboshop user
RUN useradd -m roboshop

WORKDIR /opt/server

# Copy application files
COPY payment.ini .
COPY *.py .

# Copy installed dependencies from builder
COPY --from=builder /install /usr/local

# Environment variables
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

EXPOSE 8080

# Switch to non-root user
USER roboshop

CMD ["uwsgi", "--ini", "payment.ini"]

