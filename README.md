# Dockerized Wordpress sites

You can start your own WordPress service within a few minutes by copy and paste.

## Screenshot

<img width="1083" alt="image" src="https://github.com/matsubo/wordpress-docker/assets/98103/87cdd704-5cb5-48ce-91dc-8864748404e3">


## Setup

Create `.env` file by copy and paste following code.

```
echo -n > .env
echo "MYSQL_DATABASE=wordpress" >> .env
echo "MYSQL_USER=wordpress" >> .env
echo "MYSQL_ROOT_PASSWORD=$(tr -dc A-Za-z0-9 </dev/urandom | head -c 15)" >> .env
echo "MYSQL_PASSWORD=$(tr -dc A-Za-z0-9 </dev/urandom | head -c 15)" >> .env
echo "EXPOSE_PORT=8080" >> .env
echo "UID=$(id -u)" >> .env
echo "GID=$(id -g)" >> .env
```

Example `.env` file
```
% cat .env
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_ROOT_PASSWORD=sEluuSP3rr61SE4
MYSQL_PASSWORD=On7qkFuaf9ZcP5V
EXPOSE_PORT=8080
UID=1001
GID=1001
````


## Start

```
% docker compose up -d
```

Output example.
```
% docker compose up
[+] Running 3/3
 ✔ Network wordpress-docker-template_default        Created                                                                                                                             0.3s
 ✔ Container wordpress-docker-template-mysql-1      Created                                                                                                                             0.2s
 ✔ Container wordpress-docker-template-wordpress-1  Created                                                                                                                             0.1s
Attaching to wordpress-docker-template-mysql-1, wordpress-docker-template-wordpress-1
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:03+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.3.0-1.el8 started.
wordpress-docker-template-wordpress-1  | WordPress not found in /var/www/html - copying now...
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:05+00:00 [Note] [Entrypoint]: Initializing database files
wordpress-docker-template-wordpress-1  | tar: .: Cannot change mode to rwxrwxrwx: Operation not permitted
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:05.180845Z 0 [System] [MY-015017] [Server] MySQL Server Initialization - start.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:05.184041Z 0 [System] [MY-013169] [Server] /usr/sbin/mysqld (mysqld 8.3.0) initializing of server in progress as process 41
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:05.189415Z 0 [Warning] [MY-010122] [Server] One can only use the --user switch if running as root
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:05.209714Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
wordpress-docker-template-wordpress-1  | tar: ./wp-content: Cannot change mode to rwxrwxrwx: Operation not permitted
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:06.150469Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:08.352792Z 6 [Warning] [MY-010453] [Server] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
wordpress-docker-template-wordpress-1  | tar: Exiting with failure status due to previous errors
wordpress-docker-template-wordpress-1 exited with code 0
wordpress-docker-template-wordpress-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.3. Set the 'ServerName' directive globally to suppress this message
wordpress-docker-template-wordpress-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.3. Set the 'ServerName' directive globally to suppress this message
wordpress-docker-template-wordpress-1  | [Mon Apr 29 17:00:12.542881 2024] [mpm_prefork:notice] [pid 1] AH00163: Apache/2.4.59 (Debian) PHP/8.2.18 configured -- resuming normal operations
wordpress-docker-template-wordpress-1  | [Mon Apr 29 17:00:12.542975 2024] [core:notice] [pid 1] AH00094: Command line: 'apache2 -D FOREGROUND'
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:12.985961Z 0 [System] [MY-015018] [Server] MySQL Server Initialization - end.
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:13+00:00 [Note] [Entrypoint]: Database files initialized
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:13+00:00 [Note] [Entrypoint]: Starting temporary server
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:13.368311Z 0 [System] [MY-015015] [Server] MySQL Server - start.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:13.775850Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.3.0) starting as process 83
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:13.828080Z 0 [Warning] [MY-010122] [Server] One can only use the --user switch if running as root
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:13.848358Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:14.452674Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:15.106149Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:15.106313Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:15.115528Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:15.179175Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Socket: /var/run/mysqld/mysqlx.sock
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:15.179738Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.3.0'  socket: '/var/run/mysqld/mysqld.sock'  port: 0  MySQL Community Server - GPL.
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:15+00:00 [Note] [Entrypoint]: Temporary server started.
wordpress-docker-template-mysql-1      | '/var/lib/mysql/mysql.sock' -> '/var/run/mysqld/mysqld.sock'
wordpress-docker-template-mysql-1      | Warning: Unable to load '/usr/share/zoneinfo/iso3166.tab' as time zone. Skipping it.
wordpress-docker-template-mysql-1      | Warning: Unable to load '/usr/share/zoneinfo/leap-seconds.list' as time zone. Skipping it.
wordpress-docker-template-mysql-1      | Warning: Unable to load '/usr/share/zoneinfo/leapseconds' as time zone. Skipping it.
wordpress-docker-template-mysql-1      | Warning: Unable to load '/usr/share/zoneinfo/tzdata.zi' as time zone. Skipping it.
wordpress-docker-template-mysql-1      | Warning: Unable to load '/usr/share/zoneinfo/zone.tab' as time zone. Skipping it.
wordpress-docker-template-mysql-1      | Warning: Unable to load '/usr/share/zoneinfo/zone1970.tab' as time zone. Skipping it.
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:18+00:00 [Note] [Entrypoint]: Creating database wordpress
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:18+00:00 [Note] [Entrypoint]: Creating user wordpress
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:18+00:00 [Note] [Entrypoint]: Giving user wordpress access to schema wordpress
wordpress-docker-template-mysql-1      |
wordpress-docker-template-mysql-1      |
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:18+00:00 [Note] [Entrypoint]: Stopping temporary server
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:18.624702Z 13 [System] [MY-013172] [Server] Received SHUTDOWN from user root. Shutting down mysqld (Version: 8.3.0).
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:20.046188Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.3.0)  MySQL Community Server - GPL.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:20.046213Z 0 [System] [MY-015016] [Server] MySQL Server - end.
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:20+00:00 [Note] [Entrypoint]: Temporary server stopped
wordpress-docker-template-mysql-1      |
wordpress-docker-template-mysql-1      |
wordpress-docker-template-mysql-1      | 2024-04-29 17:00:20+00:00 [Note] [Entrypoint]: MySQL init process done. Ready for start up.
wordpress-docker-template-mysql-1      |
wordpress-docker-template-mysql-1      |
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:20.651923Z 0 [System] [MY-015015] [Server] MySQL Server - start.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:20.985357Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.3.0) starting as process 1
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:20.987793Z 0 [Warning] [MY-010122] [Server] One can only use the --user switch if running as root
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:20.996677Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:21.371206Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:21.705983Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:21.706266Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:21.710082Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:21.752676Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Bind-address: '::' port: 33060, socket: /var/run/mysqld/mysqlx.sock
wordpress-docker-template-mysql-1      | 2024-04-29T17:00:21.753029Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.3.0'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.

```


## Usage

```
% open 'http://localhost:8080/'
```

## Stop

```
% docker compose down
```

## Backup

```
% docker compose down
% tar jcf /path/to/backup.tar.bz2 .
```

## Restore

```
% tar xf /path/to/backup.tar.bz2
```


## Import from existing wordpress

```
% cp -ra /old/wordpress/wp-content/{plugins,themes,uploads} wordpress/
% mysqldump -u ${OLD_MYSQL_USER} --password=${OLD_MYSQL_PASSWORD} ${OLD_MYSQL_DB_NAME} | bzip2 > dump.sql.bz2
% docker compose cp dump.sql.bz2 mysql:/dump.sql.bz2
% docker compose exec mysql bash -c 'bzcat /dump.sql.bz2 | mysql -u $MYSQL_USER -p$MYSQL_PASSWORD $MYSQL_DATABASE'
% docker compose exec mysql bash rm /dump.sql.bz2
```

