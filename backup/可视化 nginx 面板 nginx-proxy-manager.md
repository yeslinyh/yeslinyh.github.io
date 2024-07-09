![](https://img.pcdiy.xyz/file/97b89af62e8e85de001e8.png)

# 更新系统环境

```powershell
apt update -y && apt install -y curl socat wget sudo
```

# 打开 `BBR PLUS`​ 脚本

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

# 创建 `docker`​ 配置文件

1. 首先选择一个专门存放 `Nginx Proxy Manager`​ 文件的目录 (下方以 `/home/npm`​ 为例)

    ```bash
    cd /home/
    ```

    ```bash
    mkdir npm
    ```

    ```bash
    cd npm
    ```

2. 在该目录下创建一个 `docker-compose.yml`​ 文件

    ```bash
    nano docker-compose.yml
    ```

    其中，`docker-compose.yml`​ 文件的内容如下：

    ```bash
    version: '3.8'
    services:
     app:
      image: 'jc21/nginx-proxy-manager:latest'
      restart: unless-stopped
      ports:
       \- '80:80'
       \- '81:81'
       \- '443:443'
      volumes:
       \- /home/npm/data:/data
       \- /home/npm/letsencrypt:/etc/letsencrypt
    ```

    ​`81`​ 为 `web`​ 访问端口，可自定义；`80`​ 和 `443`​ **不能修改**

# 启动 `docker-compose`​

```x86asm
docker-compose up -d
```

# 登录 `web`​ 后台

* 地址: `127.0.0.1:81`​

* Email: `admin@example.com`​
* Password: `changeme`​

‍
