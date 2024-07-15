```yaml
version: '3'
services:
  qinglong:
    container_name: qinglong
    image: whyour/qinglong:latest
    restart: always
    ports:
      - 5700:5700
    volumes:
      - /volume4/docker/crontab/qinglong:/ql/data
    environment:
      - QlBaseUrl=/
      - QlPort=5700

  qiandao:
    container_name: qiandao
    image: a76yyyy/qiandao:latest
    restart: always
    ports:
      - 80:80
    volumes:
      - /volume4/docker/crontab/qiandao:/usr/src/app/config
    environment:
      - PORT=80
      - TZ=Asia/Shanghai
```