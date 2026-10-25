FROM wordpress:7-apache

# Run Apache as the host user so that files under ./wordpress stay owned by you.
# Apache only drops privileges to a user that exists in /etc/passwd, so remap
# www-data instead of using `user:` or APACHE_RUN_USER with a bare uid.
# -o allows ids that already exist in the image (e.g. gid 20 on macOS hosts).
ARG UID=1000
ARG GID=1000
RUN groupmod -o -g "${GID}" www-data \
 && usermod -o -u "${UID}" -g "${GID}" www-data \
 && chown www-data:www-data /var/www/html
