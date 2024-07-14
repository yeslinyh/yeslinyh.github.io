![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/1469bf11f58177cd49c3c.png)

# 安装 docker-compose

```powershell
$ sudo curl -L "https://github.com/docker/compose/releases/download/v2.2.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

```

# yaml 配置文件

1. `version` 为 `docker-compose` 版本号
2. `services` 下可以定义多个 `docker` 服务，如

    ```yaml
    services:
      nginx:
        xxx
        xxx
      plex:
        xxx
        xxx
    ```
3. `container_name` 定义容器名
4. `image` 定义容器镜像名
5. `ports` 定义端口映射
6. `volumes` 定义目录映射
7. `environment` 定义环境变量
8. `restart` 定义重启条件，可以选择 `unless-stopped` `always`
9. `networks` 定义容器网络，`networkname` 为网络名，需要定义，例如 `host` 模式可以如下定义：

    ```yaml
    networks:
        networkname:
          driver: host
    ```

```yaml
version: '3'
services:

  nginx:
    image: nginx:latest
    container_name: nginx
    restart: unless-stopped
    ports:
      - 8080:80
    volumes:
      - /opt/nginx:/opt/nginx/html
    networks:
      - networkname
    environment:
      - PUID=0
networks:
    networkname:
      driver: host
```

# 容器命令

在 docker-compose 所在目录执行

1. 启动容器

    ```
    docker-compose up -d
    ```
2. 停止容器

    ```
    docker-compose down
    ```
3. 重启容器

    ```
    docker-compose restart
    ```
4. 重载 docker-compose.yml

    ```
    docker-compose up --force-recreate -d
    ```