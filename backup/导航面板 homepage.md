```yaml
version: "3.3"
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    restart: always
    ports:
      - 3003:3000
    volumes:
      - /volume4/docker/homepage/config:/app/config
      - /volume4/docker/homepage/icons:/app/public/icons
      - /volume4/docker/homepage/images:/app/public/images
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - PUID=0
      - PGID=0
```