# Dockerized WordPress sites

You can start your own WordPress service within a few minutes by copy and paste.

- WordPress 7 (Apache) + MySQL 8.4 LTS, managed by Docker Compose
- WordPress core comes from the image; only `themes`, `plugins`, `uploads` and the MySQL data directory live on the host
- MySQL runs as your host user and Apache runs as a `www-data` remapped to your host uid/gid, so the files under `wordpress/` and `mysql/data/` stay owned by you

## Screenshot

<img width="1083" alt="image" src="https://github.com/matsubo/wordpress-docker/assets/98103/87cdd704-5cb5-48ce-91dc-8864748404e3">

## Requirements

- Docker with the Compose plugin (`docker compose`)
- `openssl` (used only to generate passwords)

## Setup

Create the `.env` file by copying and pasting the following code.

```sh
cat > .env <<EOF
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_ROOT_PASSWORD=$(openssl rand -hex 12)
MYSQL_PASSWORD=$(openssl rand -hex 12)
EXPOSE_PORT=8080
UID=$(id -u)
GID=$(id -g)
EOF
```

Example `.env` file:

```
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_ROOT_PASSWORD=3f9c0d6b1a7e2c4d8b5a6e0f
MYSQL_PASSWORD=9a1b7c3e5d2f8a6b4c0e1d7f
EXPOSE_PORT=8080
UID=1001
GID=1001
```

`docker compose` stops with an error if `MYSQL_ROOT_PASSWORD` or `MYSQL_PASSWORD` is missing.

## Start

```sh
docker compose up -d --wait
```

The first run builds a small WordPress image (`docker/wordpress/Dockerfile`) that remaps `www-data` to your `UID`/`GID`. `--wait` returns once MySQL accepts connections and WordPress serves pages; with the images already pulled this takes about 15 seconds.

## Usage

```sh
open "http://localhost:8080/"
```

The WordPress installer opens on the first access.

## Stop

```sh
docker compose down
```

## Update

```sh
docker compose pull --ignore-buildable
docker compose build --pull
docker compose up -d --wait
```

The base images are pinned to major versions (`wordpress:7-apache`, `mysql:8.4`), so this picks up minor and security releases only. WordPress core is re-copied from the new image when the container is recreated. Change the tags in `docker-compose.yml` and `docker/wordpress/Dockerfile` to move to a new major version.

## Backup

```sh
docker compose down
tar jcf /path/to/backup.tar.bz2 .
```

## Restore

```sh
tar xf /path/to/backup.tar.bz2
docker compose up -d --wait
```

## Import from an existing WordPress

```sh
cp -ra /old/wordpress/wp-content/{plugins,themes,uploads} wordpress/
mysqldump -u ${OLD_MYSQL_USER} --password=${OLD_MYSQL_PASSWORD} ${OLD_MYSQL_DB_NAME} | bzip2 > dump.sql.bz2
docker compose cp dump.sql.bz2 mysql:/tmp/dump.sql.bz2
docker compose exec mysql bash -c 'bzcat /tmp/dump.sql.bz2 | mysql -u "$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE"'
docker compose exec mysql rm /tmp/dump.sql.bz2
```

If the old site used a different URL, update `siteurl` and `home` in the `wp_options` table after the import.

## Configuration

| File | Purpose |
|---|---|
| `php/custom.ini` | PHP settings (upload size limits) |
| `mysql/conf/custom.cnf` | MySQL settings (`performance_schema` is disabled to save memory) |
| `docker/wordpress/Dockerfile` | WordPress image with `www-data` remapped to your `UID`/`GID` |

If you change `UID` or `GID` in `.env`, rebuild with `docker compose build`.

## Notes

- The WordPress container is not run with `user:` on purpose. As a non-root user the entrypoint cannot copy WordPress core next to the bind-mounted directories (`tar: Cannot change mode`, exit 2), and `APACHE_RUN_USER=#<uid>` without a matching `/etc/passwd` entry leaves Apache workers running as root.
- `mysql:8.4` cannot open a data directory created by a newer MySQL (9.x or later). If `mysql/data/` was created by an older version of this template that used `mysql:latest`, dump the database with the old image first, then restore it into a fresh `mysql/data/`.
