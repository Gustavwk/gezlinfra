# gezl-infra

Shared infrastructure for the gezl droplet. Runs Traefik as a reverse proxy with TLS termination via Let's Encrypt. All app stacks attach to the `gezl_traefik_net` Docker network and expose themselves through Traefik labels.

## Setup

```bash
cp .env.example .env
# Fill in ACME_EMAIL
```

## Start (dev / local)

```bash
docker compose up -d
```

## Start (production)

```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

## Network

Traefik creates and owns the `gezl_traefik_net` Docker network. App stacks must declare it as an external network:

```yaml
networks:
  default:
    external: true
    name: gezl_traefik_net
```

> **gezlholiday** currently references `gezlnomics_default`. Update it to `gezl_traefik_net` after deploying this repo.
