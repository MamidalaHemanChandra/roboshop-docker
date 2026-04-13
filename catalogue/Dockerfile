FROM node:20-alpine AS build
WORKDIR /opt/server
COPY package*.json ./ \
     && *.js ./
RUN npm install



FROM node:20-alpine
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop \
    && chown -R roboshop:roboshop /opt/server
WORKDIR /opt/server
COPY --from=build /opt/server /opt/server
USER roboshop
EXPOSE 8080
LABEL project="roboshop" \
      environment="dev" \
      created_by="heman"
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node", "server.js"]