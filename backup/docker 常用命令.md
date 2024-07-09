![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/1469bf11f58177cd49c3c.png)​

# 安装

1. [Ubuntu](https://www.runoob.com/docker/ubuntu-docker-install.html)

    ```powershell
     curl -fsSL https://test.docker.com -o test-docker.sh
     sudo sh test-docker.sh
    ```
2. [Debian](https://www.runoob.com/docker/debian-docker-install.html)

    ```powershell
     curl -fsSL https://get.docker.com -o get-docker.sh
     sudo sh get-docker.sh
    ```
3. [CentOS](https://tutorials.tinkink.net/zh-hans/linux/how-to-install-docker-on-centos-7.html)

    ```powershell
    yum install -y yum-utils
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    ```

    ```powershell
    yum install docker-ce docker-ce-cli containerd.io
    ```
4. [Windows](https://www.runoob.com/docker/windows-docker-install.html)
5. [MacOS](https://www.runoob.com/docker/macos-docker-install.html)

# 容器

1. ​`docker run`​

    创建并启动容器

    * ​`docker run -d`​

      表示以后台守护进程 (detached) 模式运行容器，即容器在后台运行
    * ​`docker run -i`​

      表示以交互模式运行容器，即保持标准输入 (stdin) 打开
    * ​`docker run -t`​

      表示为容器分配一个伪终端 (pseudo-TTY) ，即为容器分配一个虚拟终端
    * ​`docker run -it`​

      创建一个新的容器，并在其中启动一个交互式的终端。这个命令会将当前的终端连接到容器内部的终端，使得用户可以直接与容器进行交互。当退出容器时，容器也会停止运行
    * ​`docker run -itd`​

      在后台创建一个新的容器，并在其中启动一个交互式的终端。不同于前一个命令，这个命令不会将当前的终端连接到容器内部的终端，而是在后台运行容器。这样做的好处是，即使当前终端关闭或断开连接，容器仍然会继续运行。
    * ​`docker run -v /file:/file`​

      存储映射，左为主机路径，右为容器内路径
    * ​`docker run -p 8080:8080`​

      端口映射，左为主机端口，右为容器内端口
    * ​`docker run -e XXX="XXX"`​

      设置环境变量
    * ​`docker run --name XXX`​

      设置容器名
    * ​`docker run --restart=XXX`​

      * ​`docker run --restart=no`​

        为默认值，表示容器退出时，docker不自动重启容器
      * ​`docker run --restart=on-failure`​

        若容器的退出状态非0，则docker自动重启容器,还可以指定重启次数，若超过指定次数未能启动容器则放弃
      * ​`docker run --restart=always`​

        只要容器退出，则docker将自动重启容器
    * ​`docker run --net=XXX`​

      指定容器的网络连接类型

      * ​`docker run --net=bridge`​
      * ​`docker run --net=host`​
      * ​`docker run --net=none`​

        让 Docker 将新容器放到隔离的网络栈中，但是不进行网络配置。之后，用户可以自己进行配置
      * ​`docker run --net=container:NAME_or_ID`​

        让 Docker 将新建容器的进程放到一个已存在容器的网络栈中，新容器进程有自己的文件系统、进程列表和资源限制，但会和已存在的容器共享 IP 地址和端口等网络资源，两者进程可以直接通信
    * ​`docker run author/image:label`​

      作者名/镜像名:标签

      * ​`linuxserver/qbittorrent:latest`​

        最新版本
      * ​`linuxserver/qbittorrent:1.26.0`​

        指定版本
2. ​`docker start`​ / `docker stop`​ / `docker restart`​

    启动容器 / 终止容器 / 重启容器
3. ​`docker ps`​

    查看容器
4. ​`docker attach`​ / `docker exec`​

    进入容器
5. ​`docker export`​ / `docker import`​

    导出容器 / 导入容器快照
6. ​`docker rm`​

    删除容器
7. ​`docker logs`​

    查看日志

# 服务

1. ​`docker version`​

    查看 docker 版本详细信息
2. ​`docker -v`​

    查看 docker 简要信息
3. ​`systemctl start docker`​ / `systemctl stop docker`​

    启动 docker / 关闭 docker
4. ​`systemctl enable docker`​

    设置 docker 开机启动
5. ​`service docker restart`​ / `service docker stop`​

    重启 docker 服务 / 关闭 docker 服务

# 镜像

1. ​`docker search`​

    检索镜像
2. ​`docker pull`​

    拉取镜像
3. ​`docker images`​ / `docker image ls`​

    列出镜像
4. ​`docker rmi`​ / `docker image rm`​  
    删除镜像
5. ​`docker save`​ / `docker load`​

    导出镜像 / 导入镜像

​![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/020770b73ba7940a784cb.png)​
