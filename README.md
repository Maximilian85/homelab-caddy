# homelab-caddy

Custom Caddy image for the homelab reverse proxy.

It contains the official Caddy server plus the `caddy-dns/cloudflare` module required for Cloudflare DNS-01 ACME challenges and wildcard certificates.

## Image

```text
ghcr.io/maximilian85/homelab-caddy:latest
```

The image is built by GitHub Actions on changes to the Dockerfile/workflow, manually via `workflow_dispatch`, and weekly to pick up newer upstream Caddy base images.

The Cloudflare API token is **not** stored in this repository or baked into the image. Supply `CLOUDFLARE_API_TOKEN` only at runtime on the server.

## Verify module

```bash
docker run --rm ghcr.io/maximilian85/homelab-caddy:latest caddy list-modules | grep cloudflare
```

Expected output:

```text
dns.providers.cloudflare
```

## Server update

After the image has been published:

```bash
docker compose pull
docker compose up -d
```

Keep `/data` persistent so Caddy retains its ACME account and certificate state.
