# Firefly III Docker Setup

This repository contains the Docker configuration for running Firefly III.

> **Note:** The Tailscale setup is a work in progress (WIP) and is currently commented out in the docker-compose files.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Firefly III Setup

### Create Volumes

Run the following command to create the necessary volumes:

```bash
mkdir -p volumes/db volumes/firefly/data volumes/firefly/uploads volumes/tailscale/state volumes/tailscale/serveconfig
```

### Running the Containers

To start the production environment:

```bash
docker-compose -f docker-compose.yml up -d
```

For development, use:

```bash
docker-compose -f docker-compose.dev.yml up -d
```

### Configuration

- **Database:** Configured via `env/.env.db` using PostgreSQL.
- **Firefly III:** Configured via `env/.env.firefly`.
- **Cron Jobs:** Run in the `firefly-cron` service.

  **Important:** In the `firefly-cron` service of `docker-compose.yml`, you will find two "REPLACEME" placeholders:
  
  - One for the timezone (TZ) value. Replace this with your desired timezone (e.g., "Europe/London").
  - One for the cron URL token. Replace this with your `STATIC_CRON_TOKEN` (must be exactly 32 characters long).

- **Tailscale:** Configuration is available in `env/.env.tailscale` and `env/.env.sample.tailscale`, but the service is still a work in progress.

### Health Checks

- **Firefly III**: Accessible at [http://127.0.0.1:8080](http://127.0.0.1:8080).
- **Database**: Uses `pg_isready` for PostgreSQL.

### Logs and Data

- **Logs**: Check container logs via `docker logs <container_name>`.
- **Data Volumes**: Data is persisted in the `volumes/` directory.

### Additional Information

For more details on each configuration variable, refer to the `.env` sample files.

Happy budgeting!