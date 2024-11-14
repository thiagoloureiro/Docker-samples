# Use the official NGINX image from Docker Hub
FROM nginx:latest

# Copy custom HTML file into the NGINX container
# This is your custom webpage that NGINX will serve
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80 to allow external access
EXPOSE 80

# The default command for NGINX is already set to start the server, so no need to specify CMD
# However, we can explicitly add it if desired:
CMD ["nginx", "-g", "daemon off;"]
