FROM node:20-alpine AS builder
WORKDIR /opt/server
COPY package.json *.js .
RUN npm install


FROM node:20-alpine
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL project="roboshop" \
      component="user" \
      created="heman"
ENV MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
COPY --from=builder --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop
ENTRYPOINT ["node"]
CMD ["server.js"]


# FROM node:20
# EXPOSE 8080
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true" \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD ["node", "server.js"]