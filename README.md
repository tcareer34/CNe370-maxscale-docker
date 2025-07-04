# MariaDB MaxScale Docker image

This Docker image runs the latest Docker version 26.1.3-0ubuntu1~24.04.1 version:

-	Tim Nguyen:  
	(https://github.com/tcareer34/CNe370-maxscale-docker/tree/master/maxscale)

## Running
https://github.com/tcareer34/CNe370-maxscale-docker/blob/master/maxscale/docker-compose.yml) contains maxscale
configured with a three node maxscale-master1-master2 cluster. To start it, run the
following commands in this directory.

```
docker-compose build
docker-compose up -d
```

After MaxScale and the servers have started (takes a few minutes), you can find
the readwritesplit router on port 4000 . The
user `maxuser` with the password `maxpwd` can be used to test the cluster.
Assuming the mariadb client is installed on the host machine:
```
$ mysql -umaxuser -pmaxpwd -h 127.0.0.1 -P 4000
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 5

```
You can edit the [`https://github.com/tcareer34/CNe370-maxscale-docker/tree/master/maxscale/maxscale.cnf.d]
example.cnf file and recreate the MaxScale container to change the configuration.

To stop the containers, execute the following command. Optionally, use the -v
flag to also remove the volumes.

To run maxctrl in the container to see the status of the cluster:
```
Tim@Ubuntu:~/CNE370-maxscale-docker/maxscale$ sudo docker-compose exec maxscale maxctrl list servers

┌─────────┬──────────┬──────┬─────────────┬─────────────────┬──────┬─────────────────┐

│ Server  │ Address  │ Port │ Connections │ State           │ GTID │ Monitor         │

├─────────┼──────────┼──────┼─────────────┼─────────────────┼──────┼─────────────────┤

│ server1 │ master1 │ 3306 │ 0           │ Master, Running │      │ MariaDB-Monitor │

├─────────┼──────────┼──────┼─────────────┼─────────────────┼──────┼─────────────────┤

│ server2 │ master2 │ 3306 │ 0           │ Running         │      │ MariaDB-Monitor │

└─────────┴──────────┴──────┴─────────────┴─────────────────┴──────┴─────────────────┘



```

The cluster is configured Python3 . 
Tim@Ubuntu:~/CNE370-maxscale-docker/maxscale$ nano main.py
 
Then run the code wit the command:
Tim@Ubuntu:~/CNE370-maxscale-docker/maxscale$ python3 main.py

```
Run the command to chech the MariaDB server: sudo docker inspect maxscale-maxscale-1
"Gateway": "172.22.0.1",
"IPAddress": "172.22.0.4",
"IPPrefixLen": 16,
                    
```

Once complete, to remove the cluster and maxscale containers:

```
docker-compose down -v
```
