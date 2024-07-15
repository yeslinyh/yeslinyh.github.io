```yaml
version: "2.4"
services:
    talebook:
        container_name: talebook
        image: talebook/talebook:latest
        restart: always
        ports:
            - 8081:80
        volumes:
            - /volume4/docker/talebook:/data
        environment:
            - PUID=1000
            - PGID=1000
            - TZ=Asia/Shanghai
            - SSR=ON
    douban-api-rs:
        container_name: douban-api-rs
        image: ghcr.io/cxfksword/douban-api-rs:latest
        restart: always
        ports:
            - 10080:80
```