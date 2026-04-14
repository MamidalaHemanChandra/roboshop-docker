# -------- Stage 1: Builder --------
FROM python:3.9-slim AS builder

WORKDIR /build

# Install build dependencies (only needed during build)
RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

# Install dependencies into a separate directory
RUN pip install --upgrade pip && \
    pip install --prefix=/install -r requirements.txt


# -------- Stage 2: Runtime --------
FROM python:3.9-slim

# Create non-root user
RUN useradd -m -r roboshop

WORKDIR /opt/server

# Copy only installed dependencies from builder
COPY --from=builder /install /usr/local

# Copy application code
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

# Set permissions
RUN chown -R roboshop:roboshop /opt/server

# Switch to non-root user
USER roboshop

EXPOSE 8080

# Start application
CMD ["uwsgi", "--ini", "payment.ini"]



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