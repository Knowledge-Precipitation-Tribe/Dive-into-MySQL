# Docker

对Docker不太熟悉的朋友可以看此文档：[动手学Docker](https://docs.docker.knowledge-precipitation.site/)

这里我们使用Docker-Compose的方式安装MySQL

{% code title="docker-compose.yml" %}
```text
version: "3"
services:
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: 'db'
      # So you don't have to use root, but you can if you like
      MYSQL_USER: 'user'
      # You can use whatever password you like
      MYSQL_PASSWORD: 'password'
      # Password for root access
      MYSQL_ROOT_PASSWORD: 'password'
    ports:
      # <Port exposed> : < MySQL Port running inside container>
      - '3306:3306'
    expose:
      # Opens port 3306 on the container
      - '3306'
      # Where our data will be persisted
    volumes:
      - my-db:/var/lib/mysql
# Names our volume
volumes:
  my-db:
```
{% endcode %}

接下来使用命令启动MySQL服务

```text
docker-compose up -d
```

接下来我们可以进入到容器当中

```text
docker-compose exec db bash
```

在容器中我们就可以对MySQL进行各种操作了

