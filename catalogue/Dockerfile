FROM node:20-alpine AS build
WORKDIR /opt/server
COPY *.json .
COPY *.js .
RUN npm install


FROM node:20-alpine
WORKDIR /opt/server
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=build /opt/server /opt/server
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node", "server.js"]