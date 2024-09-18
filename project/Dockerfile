FROM wordpress:php-fpm
 
# Install additional PHP extensions if needed
RUN docker-php-ext-install pdo_mysql
 
# Copy custom config files if needed
# COPY custom.ini /usr/local/etc/php/conf.d/
 
FROM nginx:latest
 
# Copy your custom nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf
 
# Copy custom static files if needed
# COPY ./static /usr/share/nginx/html