# Cloudflared Docker Setup

This Docker Compose setup runs a `cloudflared` tunnel in a Docker container using the `cloudflare/cloudflared:latest` image.

## Configuration

The `docker-compose.yml` file is configured as follows:

```yaml
version: '3.7'

services:
  cloudflared:
    container_name: cloudflared-tunnel
    image: cloudflare/cloudflared:latest
    command: tunnel --no-autoupdate run --protocol quic --token ${CLOUDFLARED_TOKEN}
    volumes:
      - /etc/localtime:/etc/localtime:ro
    networks:
      - racksync
    #environment:
    #  TZ: "Asia/Bangkok"
    restart: always

networks:
  racksync:
    driver: bridge
```

## Parameters

```container_name```: Specifies the name of the container.
```image```: The Docker image used to create the container.
```command```: The command executed when the container starts.
```volumes```: Binds the host's timezone data to the container.
```networks```: Specifies the network that the container connects to.
```restart```: Determines the restart policy.

## How to Use

### Prerequisites

```bash
git clone https://github.com/smilexth/cloudflared-tunnel-docker
cd cloudflared-tunnel-docker
```

### Setup

1. Move `default.env` to `.env` file in the same directory as the `docker-compose.yml` file.
2. Edit the `.env` file and set the `CLOUDFLARED_TOKEN` variable to your Cloudflare Tunnel token.
3. Run `docker-compose up -d` to start the container.

### Logs

To view the logs, run `docker-compose logs -f`.

### Support and Contributions

- For issues, please open an issue or seek support in relevant forums.
- Contributions are welcome! Create a pull request to contribute.


