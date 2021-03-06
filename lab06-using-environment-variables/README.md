# Lab6 - Using environment variables
This document is the lab related to Docker environment variables

## Starting MariaDB container

- Try to start a mariadb conainer

```
[vagrant@node1 ~]$ docker run --rm mariadb
Unable to find image 'mariadb:latest' locally
Trying to pull repository docker.io/library/mariadb ...
latest: Pulling from docker.io/library/mariadb
32802c0cfa4d: Pull complete
da1315cffa03: Pull complete
fa83472a3562: Pull complete
f85999a86bef: Pull complete
a2434d5c8419: Pull complete
181debc3d23d: Pull complete
7b5b2b6de4ee: Pull complete
6f830a8cb936: Pull complete
c6becfb25371: Pull complete
a57998e3e98d: Pull complete
26444682043c: Pull complete
9bbb07a72de5: Pull complete
84b75eddf6b1: Pull complete
9f45ae7e5c8d: Pull complete
Digest: sha256:12e32f8d1e8958cd076660bc22d19aa74f2da63f286e100fb58d41b740c57006
Status: Downloaded newer image for docker.io/mariadb:latest
error: database is uninitialized and password option is not specified
  You need to specify one of MYSQL_ROOT_PASSWORD, MYSQL_ALLOW_EMPTY_PASSWORD and MYSQL_RANDOM_ROOT_PASSWORD
```
Note! It is expected that container fails with an error message

- Open container documentation using the following link

```
https://hub.docker.com/_/mariadb
```

- Scroll down to the "Environment Variables" chapter

- Try to start a mariadb container by passing MYSQL_ROOT_PASSWORD environment variable

```
[vagrant@node1 ~]$ docker run -d --name mariadb -e MYSQL_ROOT_PASSWORD=qwerty mariadb
6c0ea35a6c28ce1269217bceae2edc396087db75d375d8456daea3e1b6b63175
[vagrant@node1 ~]$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
6c0ea35a6c28        mariadb             "docker-entrypoint..."   2 seconds ago       Up 1 second         3306/tcp            mariadb
```

- Check container logs

```
[vagrant@node1 ~]$ docker logs mariadb
Initializing database
PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !
To do so, start the server, then issue the following commands:
'/usr/bin/mysqladmin' -u root password 'new-password'
'/usr/bin/mysqladmin' -u root -h  password 'new-password'
Alternatively you can run:
'/usr/bin/mysql_secure_installation'
which will also give you the option of removing the test
databases and anonymous user created by default.  This is
strongly recommended for production servers.
See the MariaDB Knowledgebase at http://mariadb.com/kb or the
MySQL manual for more instructions.
Please report any problems at http://mariadb.org/jira
The latest information about MariaDB is available at http://mariadb.org/.
You can find additional information about the MySQL part at:
http://dev.mysql.com
Consider joining MariaDB's strong and vibrant community:
https://mariadb.org/get-involved/
Database initialized
MySQL init process in progress...
2018-12-04  5:32:58 0 [Note] mysqld (mysqld 10.3.11-MariaDB-1:10.3.11+maria~bionic) starting as process 100 ...
2018-12-04  5:32:58 0 [Note] InnoDB: Using Linux native AIO
2018-12-04  5:32:58 0 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
2018-12-04  5:32:58 0 [Note] InnoDB: Uses event mutexes
2018-12-04  5:32:58 0 [Note] InnoDB: Compressed tables use zlib 1.2.11
2018-12-04  5:32:58 0 [Note] InnoDB: Number of pools: 1
2018-12-04  5:32:58 0 [Note] InnoDB: Using SSE2 crc32 instructions
2018-12-04  5:32:58 0 [Note] InnoDB: Initializing buffer pool, total size = 256M, instances = 1, chunk size = 128M
2018-12-04  5:32:58 0 [Note] InnoDB: Completed initialization of buffer pool
2018-12-04  5:32:58 0 [Note] InnoDB: If the mysqld execution user is authorized, page cleaner thread priority can be changed. See the man page of setpriority().
2018-12-04  5:32:58 0 [Note] InnoDB: 128 out of 128 rollback segments are active.
2018-12-04  5:32:58 0 [Note] InnoDB: Creating shared tablespace for temporary tables
2018-12-04  5:32:58 0 [Note] InnoDB: Setting file './ibtmp1' size to 12 MB. Physically writing the file full; Please wait ...
2018-12-04  5:32:58 0 [Note] InnoDB: File './ibtmp1' size is now 12 MB.
2018-12-04  5:32:58 0 [Note] InnoDB: Waiting for purge to start
2018-12-04  5:32:59 0 [Note] InnoDB: 10.3.11 started; log sequence number 1630815; transaction id 21
2018-12-04  5:32:59 0 [Note] InnoDB: Loading buffer pool(s) from /var/lib/mysql/ib_buffer_pool
2018-12-04  5:32:59 0 [Note] Plugin 'FEEDBACK' is disabled.
2018-12-04  5:32:59 0 [Warning] 'user' entry 'root@6c0ea35a6c28' ignored in --skip-name-resolve mode.
2018-12-04  5:32:59 0 [Warning] 'user' entry '@6c0ea35a6c28' ignored in --skip-name-resolve mode.
2018-12-04  5:32:59 0 [Warning] 'proxies_priv' entry '@% root@6c0ea35a6c28' ignored in --skip-name-resolve mode.
2018-12-04  5:32:59 0 [Note] InnoDB: Buffer pool(s) load completed at 181204  5:32:59
2018-12-04  5:32:59 0 [Note] Reading of all Master_info entries succeded
2018-12-04  5:32:59 0 [Note] Added new Master_info '' to hash table
2018-12-04  5:32:59 0 [Note] mysqld: ready for connections.
Version: '10.3.11-MariaDB-1:10.3.11+maria~bionic'  socket: '/var/run/mysqld/mysqld.sock'  port: 0  mariadb.org binary distribution
Warning: Unable to load '/usr/share/zoneinfo/leap-seconds.list' as time zone. Skipping it.
2018-12-04  5:33:01 10 [Warning] 'proxies_priv' entry '@% root@6c0ea35a6c28' ignored in --skip-name-resolve mode.
2018-12-04  5:33:01 0 [Note] mysqld (initiated by: unknown): Normal shutdown
2018-12-04  5:33:01 0 [Note] Event Scheduler: Purging the queue. 0 events
2018-12-04  5:33:01 0 [Note] InnoDB: FTS optimize thread exiting.
2018-12-04  5:33:01 0 [Note] InnoDB: Starting shutdown...
2018-12-04  5:33:01 0 [Note] InnoDB: Dumping buffer pool(s) to /var/lib/mysql/ib_buffer_pool
2018-12-04  5:33:01 0 [Note] InnoDB: Buffer pool(s) dump completed at 181204  5:33:01
2018-12-04  5:33:02 0 [Note] InnoDB: Shutdown completed; log sequence number 1630824; transaction id 24
2018-12-04  5:33:02 0 [Note] InnoDB: Removed temporary tablespace data file: "ibtmp1"
2018-12-04  5:33:02 0 [Note] mysqld: Shutdown complete
MySQL init process done. Ready for start up.
2018-12-04  5:33:03 0 [Note] mysqld (mysqld 10.3.11-MariaDB-1:10.3.11+maria~bionic) starting as process 1 ...
2018-12-04  5:33:03 0 [Note] InnoDB: Using Linux native AIO
2018-12-04  5:33:03 0 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
2018-12-04  5:33:03 0 [Note] InnoDB: Uses event mutexes
2018-12-04  5:33:03 0 [Note] InnoDB: Compressed tables use zlib 1.2.11
2018-12-04  5:33:03 0 [Note] InnoDB: Number of pools: 1
2018-12-04  5:33:03 0 [Note] InnoDB: Using SSE2 crc32 instructions
2018-12-04  5:33:03 0 [Note] InnoDB: Initializing buffer pool, total size = 256M, instances = 1, chunk size = 128M
2018-12-04  5:33:03 0 [Note] InnoDB: Completed initialization of buffer pool
2018-12-04  5:33:03 0 [Note] InnoDB: If the mysqld execution user is authorized, page cleaner thread priority can be changed. See the man page of setpriority().
2018-12-04  5:33:03 0 [Note] InnoDB: 128 out of 128 rollback segments are active.
2018-12-04  5:33:03 0 [Note] InnoDB: Creating shared tablespace for temporary tables
2018-12-04  5:33:03 0 [Note] InnoDB: Setting file './ibtmp1' size to 12 MB. Physically writing the file full; Please wait ...
2018-12-04  5:33:03 0 [Note] InnoDB: File './ibtmp1' size is now 12 MB.
2018-12-04  5:33:03 0 [Note] InnoDB: Waiting for purge to start
2018-12-04  5:33:03 0 [Note] InnoDB: 10.3.11 started; log sequence number 1630824; transaction id 21
2018-12-04  5:33:03 0 [Note] InnoDB: Loading buffer pool(s) from /var/lib/mysql/ib_buffer_pool
2018-12-04  5:33:03 0 [Note] Plugin 'FEEDBACK' is disabled.
2018-12-04  5:33:03 0 [Note] Server socket created on IP: '::'.
2018-12-04  5:33:03 0 [Note] InnoDB: Buffer pool(s) load completed at 181204  5:33:03
2018-12-04  5:33:03 0 [Warning] 'proxies_priv' entry '@% root@6c0ea35a6c28' ignored in --skip-name-resolve mode.
2018-12-04  5:33:03 0 [Note] Reading of all Master_info entries succeded
2018-12-04  5:33:03 0 [Note] Added new Master_info '' to hash table
2018-12-04  5:33:03 0 [Note] mysqld: ready for connections.
Version: '10.3.11-MariaDB-1:10.3.11+maria~bionic'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  mariadb.org binary distribution
```

Note! Container was started successfully this time.

- Try to access mariadb application using container tools

```
[vagrant@node1 ~]$ docker exec -it mariadb mysql -uroot -pqwerty
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 12
Server version: 10.3.11-MariaDB-1:10.3.11+maria~bionic mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.001 sec)

MariaDB [(none)]> exit
Bye
```

- Delete all containers

```
docker rm -f $(docker ps -aq)
```

- Start a mariadb container with the following settings

Parameter           | Value
------------------- | -----
MYSQL_ROOT_PASSWORD | secret
MYSQL_USER          | dbuser
MYSQL_PASSWORD      | dbpassword
MYSQL_DATABASE      | db1

```
docker run -d --name mariadb \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_USER=dbuser \
  -e MYSQL_PASSWORD=dbpassword \
  -e MYSQL_DATABASE=db1 \
  mariadb
```

- Check container status

```
[vagrant@node1 ~]$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
12483ee9d4e0        mariadb             "docker-entrypoint..."   2 seconds ago       Up 1 second         3306/tcp            mariadb
```

- Try to access MariaDB service using dbuser

```
[vagrant@node1 ~]$ docker exec mariadb mysql -udbuser -pdbpassword -e "show databases;" db1
Database
db1
information_schema
```

Note! you should be able to access the mariadb service using dbuser
