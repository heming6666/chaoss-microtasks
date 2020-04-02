# Microtask 4
Set up a dev environment to work on GrimoireLab.

Here's the [Reference](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/Getting-Started.md#getting-started-).

In this task, We will use the method of `docker-compose`to set up the GrimoireLab developer environment. It is really powerful and convenient.

All we need to do is configure a [`docker-compose.yml`](./docker-compose.yml). A version of `docker-compose` with SearchGuard may looks like: 

 ```docker-compose
version: '2.2'

services:
    elasticsearch:
      image: docker.elastic.co/elasticsearch/elasticsearch-oss:6.1.4
      command: /elasticsearch/bin/elasticsearch -E network.bind_host=0.0.0.0
      ports:
        - 9200:9200
      environment:
        - ES_JAVA_OPTS=-Xms2g -Xmx2g

    kibiter:
      restart: on-failure:5
      image: bitergia/kibiter:optimized-v6.1.4-3
      environment:
        - PROJECT_NAME=Demo
        - NODE_OPTIONS=--max-old-space-size=1000
        - ELASTICSEARCH_URL=http://elasticsearch:9200
      links:
        - elasticsearch
      ports:
        - 5601:5601

    mariadb:
      restart: on-failure:5
      image: mariadb:10.0
      expose:
        - "3306"
      ports:
        - "3306:3306"
      environment:
        - MYSQL_ROOT_PASSWORD=
        - MYSQL_ALLOW_EMPTY_PASSWORD=yes
        - MYSQL_DATABASE=test_sh
      command: --wait_timeout=2592000 --interactive_timeout=2592000 --max_connections=300
 ```   

Then run `docker-compose up -d` to get ElasticSearch, Kibiter and MariaDB.
```bash
docker-compose up -d
```

We can use `netstat` to show the ports:

![setup-dev-env](./images/setup-dev-env.png)

