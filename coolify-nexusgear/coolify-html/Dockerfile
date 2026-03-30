FROM nginx:alpine

# Copy the store HTML file into nginx
COPY index.html /usr/share/nginx/html/index.html

# Optional: copy any assets if you have them
# COPY assets/ /usr/share/nginx/html/assets/

# Custom nginx config for single-page app
RUN echo 'server { \
    listen 80; \
    root /usr/share/nginx/html; \
    index index.html; \
    location / { \
        try_files $uri $uri/ /index.html; \
    } \
    gzip on; \
    gzip_types text/html text/css application/javascript; \
}' > /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
