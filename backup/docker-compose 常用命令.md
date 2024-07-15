![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/1469bf11f58177cd49c3c.png)

# 安装 docker-compose

安装或更新 docker-compose

```powershell
sudo curl -L "https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

给可执行权限

```powershell
sudo chmod +x /usr/local/bin/docker-compose
```

创建软链接以便于在终端中使用 docker-compose 命令

```powershell
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

检查版本

```powershell
docker-compose --version
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
9. `network_mode` 定义容器网络
10. `privileged` 定义特权

```yaml
version: '3'
services:
  nginx:
    image: nginx:latest
    container_name: nginx
    restart: always
    network_mode: host
    privileged: true
    ports:
      - 8080:80
    volumes:
      - /opt/nginx:/opt/nginx/html
    environment:
      - PUID=0
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