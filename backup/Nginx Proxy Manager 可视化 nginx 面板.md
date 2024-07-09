# 更新系统环境

```powershell
apt update -y && apt install -y curl socat wget sudo
```

# 打开 `BBR PLUS`​ 脚本

```bash
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

# 创建目录一个专门存放 `Nginx Proxy Manager`​ 文件的目录，并在该目录下创建一个 `docker-compose.yml`​ 文件

```bash
cd /home/
```

```bash
mkdir npm
```

```bash
cd npm
```

```bash
nano docker-compose.yml
```

其中，`docker-compose.yml`​ 文件的内容如下：

​`81`​ 为访问端口，可自定义，`80`​，`443`​ **不能修改**

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
   \- ./data:/data
   \- ./letsencrypt:/etc/letsencrypt
```

# 启动 `docker-compose`​

```x86asm
docker-compose up -d
```

‍
