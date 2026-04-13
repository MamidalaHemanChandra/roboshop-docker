# FROM node:20-alpine AS build
# WORKDIR /opt/server
# COPY package*.json ./
# COPY *.js ./
# RUN npm install



# FROM node:20-alpine
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop \
#     && mkdir -p /opt/server \
#     && chown -R roboshop:roboshop /opt/server
# WORKDIR /opt/server
# COPY --from=build /opt/server /opt/server
# USER roboshop
# EXPOSE 8080
# LABEL project="roboshop" \
#       environment="dev" \
#       created_by="heman"
# ENV REDIS_HOST="redis" \
#     CATALOGUE_HOST="catalogue" \
#     CATALOGUE_PORT="8080"
# CMD ["node", "server.js"]

FROM node:20
EXPOSE 8080
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install
ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"
CMD ["node", "server.js"]