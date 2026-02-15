# Use lightweight Nginx
FROM nginx:alpine

# Copy the Landing Page
COPY index.html /usr/share/nginx/html/index.html

# Custom Nginx config for Port 7860 (Hugging Face / Hackathon Standard)
RUN echo 'server { \
    listen 7860; \
    location / { \
        root /usr/share/nginx/html; \
        index index.html index.htm; \
    } \
}' > /etc/nginx/conf.d/default.conf

# Permissions fix
RUN chmod -R 777 /var/cache/nginx /var/run /var/log/nginx

# Expose Port
EXPOSE 7860

# Start
CMD ["nginx", "-g", "daemon off;"]
