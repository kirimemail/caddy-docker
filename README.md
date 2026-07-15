# kirimemail/caddy-docker

Custom [Caddy](https://caddyserver.com/) Docker image built with [xcaddy](https://github.com/caddyserver/xcaddy), bundling essential plugins for production use at Kirim.Email.

## Tags

| Tag | Base | Description |
|-----|------|-------------|
| `latest` | `scratch` | Minimal image with ca-certificates only |
| `alpine` | `alpine:3` | Alpine-based image with shell and package manager |

## Bundled Plugins

| Plugin | Purpose |
| -------- | --------- |
| [caddy-dns/cloudflare](https://github.com/caddy-dns/cloudflare) | ACME DNS-01 challenge via Cloudflare |
| [caddy-dns/powerdns](https://github.com/caddy-dns/powerdns) | ACME DNS-01 challenge via PowerDNS |
| [certmagic-s3](https://github.com/ss098/certmagic-s3) | Certificate storage on S3 |
| [caddy-storage-redis](https://github.com/pberkel/caddy-storage-redis) | Certificate storage on Redis |
| [caddy-mysql-storage](https://github.com/zhangjiayin/caddy-mysql-storage) | Certificate storage on MySQL |
| [postgres-storage](https://github.com/yroc92/postgres-storage) | Certificate storage on PostgreSQL |
| [caddy-storage-cf-kv](https://github.com/mentimeter/caddy-storage-cf-kv) | Certificate storage on Cloudflare KV |
| [caddy-ratelimit](https://github.com/mholt/caddy-ratelimit) | HTTP rate limiting |
| [transform-encoder](https://github.com/caddyserver/transform-encoder) | Log field transformation |
| [caddy-trapdoor](https://github.com/kassner/caddy-trapdoor) | IP-based access control |
| [caddy-l4](https://github.com/mholt/caddy-l4) | Layer 4 (TCP/UDP) proxying |
| [realip](https://github.com/kirsch33/realip) | Real IP header handling |
| [caddy-security](https://github.com/greenpau/caddy-security) | Auth portal, JWT, OAuth, MFA |
| [caddy-crowdsec-bouncer](https://github.com/hslatman/caddy-crowdsec-bouncer) | CrowdSec bouncer for blocking malicious IPs |
| [caddy-docker-proxy](https://github.com/lucaslorentz/caddy-docker-proxy) | Automatic reverse proxy from Docker labels |

## Usage

```sh
docker run -d \
  -p 80:80 -p 443:443 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v caddy_data:/data \
  -v caddy_config:/config \
  kirimemail/caddy-docker:latest
```

### Docker Compose

```yaml
services:
  caddy:
    image: kirimemail/caddy-docker:latest
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    environment:
      - CF_API_TOKEN=your-cloudflare-token
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - caddy_data:/data
      - caddy_config:/config
```

## Caddy Version

- **Caddy**: v2.11.4
- **Go builder**: golang:1.26-alpine
- **xcaddy**: latest

## Build

```sh
# scratch-based (minimal)
docker build -f Dockerfile -t caddy-docker .

# alpine-based
docker build -f Dockerfile.alpine -t caddy-docker:alpine .
```

## License

MIT
