```yaml
version: "2.1"
services:
  qbittorrent:
    container_name: qbittorrent
    image: linuxserver/qbittorrent:latest
    restart: always
    network_mode: host
    volumes:
      - /path/to/qbittorrent/appdata:/config
      - /path/to/downloads:/downloads #optional
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
      - WEBUI_PORT=8080
      - TORRENTING_PORT=12345
```