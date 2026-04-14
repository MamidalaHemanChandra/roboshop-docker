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

# Copy only requirements first (better caching)
COPY requirements.txt .

# Install build dependencies
RUN pip install --user --no-cache-dir -r requirements.txt

# ---- Stage 2: Final runtime image ----
FROM python:3.9-slim

# Create roboshop user and group
RUN useradd -m roboshop

WORKDIR /opt/server

# Copy application files
COPY payment.ini .
COPY *.py .

# Copy installed dependencies from builder
COPY --from=builder /root/.local /root/.local

# Ensure Python can find the installed packages
ENV PATH=/root/.local/bin:$PATH

# Environment variables for services
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

# Switch to roboshop user
USER roboshop

EXPOSE 8080

# Run the service
CMD ["uwsgi", "--ini", "payment.ini"]
