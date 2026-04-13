# FROM nginx:1.24-alpine
# RUN rm -rf /usr/share/nginx/html/* \
#     && rm -f /etc/nginx/nginx.conf \
#     && rm -f /etc/nginx/conf.d/default.conf
# COPY nginx.conf /etc/nginx/nginx.conf
# COPY static/ /usr/share/nginx/html/
# RUN chmod -R 755 /usr/share/nginx/html
# EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]

FROM nginx:1.24
RUN rm -rf /usr/share/nginx/html/* 
RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY static/ /usr/share/nginx/html/