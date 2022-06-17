# Node.js Rest APIs with Express, Sequelize & MySQL
Building this with Docker-Compose, everything seems running fine, DB was created on mysql container correctly and API site was running fine on port 8080 but issue for there is no data could be saved from API sequelized site to DB, tested with Postman ( https://i.imgur.com/VYOPSpi.png )


$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                                  NAMES
947672021d78   session4_api   "docker-entrypoint.s…"   7 seconds ago   Up 4 seconds   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp              session4_api_1
5c3d50b94135   mysql:5.7      "docker-entrypoint.s…"   8 seconds ago   Up 6 seconds   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   session4_mysqldb_1

+++++++

$ docker logs 947

> nodejs-express-sequelize-mysql@1.0.0 start /api
> node server.js

(node:20) [SEQUELIZE0004] DeprecationWarning: A boolean value was passed to options.operatorsAliases. This is a no-op with v5 and should be removed.
(Use `node --trace-deprecation ...` to show where the warning was created)
Server is running on port 8080.
Executing (default): CREATE TABLE IF NOT EXISTS `tutorials` (`id` INTEGER NOT NULL auto_increment , `title` VARCHAR(255), `description` VARCHAR(255), `published` TINYINT(1), `createdAt` DATETIME NOT NULL, `updatedAt` DATETIME NOT NULL, PRIMARY KEY (`id`)) ENGINE=InnoDB;
Executing (default): SHOW INDEX FROM `tutorials`

+++++++

$ docker logs 5c3
2022-06-17 16:50:43+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 5.7.38-1debian10 started.
2022-06-17 16:50:43+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2022-06-17 16:50:43+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 5.7.38-1debian10 started.
2022-06-17T16:50:43.844612Z 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
2022-06-17T16:50:43.845509Z 0 [Note] mysqld (mysqld 5.7.38) starting as process 1 ...
2022-06-17T16:50:43.847125Z 0 [Note] InnoDB: PUNCH HOLE support available
2022-06-17T16:50:43.847149Z 0 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
2022-06-17T16:50:43.847152Z 0 [Note] InnoDB: Uses event mutexes
2022-06-17T16:50:43.847153Z 0 [Note] InnoDB: GCC builtin __atomic_thread_fence() is used for memory barrier
2022-06-17T16:50:43.847154Z 0 [Note] InnoDB: Compressed tables use zlib 1.2.11
2022-06-17T16:50:43.847155Z 0 [Note] InnoDB: Using Linux native AIO
2022-06-17T16:50:43.847267Z 0 [Note] InnoDB: Number of pools: 1
2022-06-17T16:50:43.847338Z 0 [Note] InnoDB: Using CPU crc32 instructions
2022-06-17T16:50:43.848303Z 0 [Note] InnoDB: Initializing buffer pool, total size = 128M, instances = 1, chunk size = 128M
2022-06-17T16:50:43.852796Z 0 [Note] InnoDB: Completed initialization of buffer pool
2022-06-17T16:50:43.862273Z 0 [Note] InnoDB: If the mysqld execution user is authorized, page cleaner thread priority can be changed. See the man page of setpriority().
2022-06-17T16:50:43.873395Z 0 [Note] InnoDB: Highest supported file format is Barracuda.
2022-06-17T16:50:43.909385Z 0 [Note] InnoDB: Creating shared tablespace for temporary tables
2022-06-17T16:50:43.909459Z 0 [Note] InnoDB: Setting file './ibtmp1' size to 12 MB. Physically writing the file full; Please wait ...
2022-06-17T16:50:43.967466Z 0 [Note] InnoDB: File './ibtmp1' size is now 12 MB.
2022-06-17T16:50:43.967790Z 0 [Note] InnoDB: 96 redo rollback segment(s) found. 96 redo rollback segment(s) are active.
2022-06-17T16:50:43.967806Z 0 [Note] InnoDB: 32 non-redo rollback segment(s) are active.
2022-06-17T16:50:43.968706Z 0 [Note] InnoDB: Waiting for purge to start
2022-06-17T16:50:44.018932Z 0 [Note] InnoDB: 5.7.38 started; log sequence number 12664650
2022-06-17T16:50:44.019113Z 0 [Note] InnoDB: Loading buffer pool(s) from /var/lib/mysql/ib_buffer_pool
2022-06-17T16:50:44.019218Z 0 [Note] Plugin 'FEDERATED' is disabled.
2022-06-17T16:50:44.020434Z 0 [Note] InnoDB: Buffer pool(s) load completed at 220617 16:50:44
2022-06-17T16:50:44.022340Z 0 [Note] Found ca.pem, server-cert.pem and server-key.pem in data directory. Trying to enable SSL support using them.
2022-06-17T16:50:44.022362Z 0 [Note] Skipping generation of SSL certificates as certificate files are present in data directory.
2022-06-17T16:50:44.022365Z 0 [Warning] A deprecated TLS version TLSv1 is enabled. Please use TLSv1.2 or higher.
2022-06-17T16:50:44.022367Z 0 [Warning] A deprecated TLS version TLSv1.1 is enabled. Please use TLSv1.2 or higher.
2022-06-17T16:50:44.022658Z 0 [Warning] CA certificate ca.pem is self signed.
2022-06-17T16:50:44.022688Z 0 [Note] Skipping generation of RSA key pair as key files are present in data directory.
2022-06-17T16:50:44.022987Z 0 [Note] Server hostname (bind-address): '*'; port: 3306
2022-06-17T16:50:44.023084Z 0 [Note] IPv6 is available.
2022-06-17T16:50:44.023105Z 0 [Note]   - '::' resolves to '::';
2022-06-17T16:50:44.023114Z 0 [Note] Server socket created on IP: '::'.
2022-06-17T16:50:44.052764Z 0 [Warning] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
2022-06-17T16:50:44.056340Z 0 [Note] Event Scheduler: Loaded 0 events
2022-06-17T16:50:44.056589Z 0 [Note] mysqld: ready for connections.
Version: '5.7.38'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)

+++++++
Network
+++++++
$ docker network inspect 709
[
    {
        "Name": "session4_backend",
        "Id": "709c1de7ab12b11944e58eda133f3e5be874f071244c25bd8bb66ca17c32e9b8",
        "Created": "2022-06-18T00:50:00.86546543+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "192.168.192.0/20",
                    "Gateway": "192.168.192.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": true,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "5c3d50b9413524c77754b9961ef6d424a0ef4656c94073aa5aefdc58c389b96d": {
                "Name": "session4_mysqldb_1",
                "EndpointID": "113c5501bc328213cb98eb59d549c369815c079d903aa90aa9a1898ba1feacb6",
                "MacAddress": "02:42:c0:a8:c0:02",
                "IPv4Address": "192.168.192.2/20",
                "IPv6Address": ""
            },
            "947672021d78b01b46a4a77f2b05a22391990f3238bf2693d54e2b80f387901b": {
                "Name": "session4_api_1",
                "EndpointID": "027df4096f12659b83215a59a90f859e43e537098c4dc08b6fb7863b7a228bac",
                "MacAddress": "02:42:c0:a8:c0:03",
                "IPv4Address": "192.168.192.3/20",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {
            "com.docker.compose.network": "backend",
            "com.docker.compose.project": "session4",
            "com.docker.compose.version": "1.29.2"
        }
    }
]

++++++++++++++++++++++
Check telnet dari API container ke MySQL container, gak ada masalah di port 3306:

# telnet 192.168.192.2 3306
Trying 192.168.192.2...
Connected to 192.168.192.2.
Escape character is '^]'.
J
5.7.387hK\
          2mD*(W~c~dmysql_native_password
          
+++++++++++++++++++++

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| data               |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)

mysql> use data;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+----------------+
| Tables_in_data |
+----------------+
| tutorials      |
+----------------+
1 row in set (0.00 sec)

mysql> select * from tutorials;
Empty set (0.00 sec)
