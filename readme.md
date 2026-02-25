# Ignition 8.3 Showcase & Testing Ground

A showcase and testing environment for Ignition 8.3 features and custom third-party modules. This project demonstrates various 8.3 capabilities and serves as a development playground for exploring new features and custom module integration.

## Quick Start

1. **Initialize submodules:**
   ```bash
   git submodule update --init --recursive
   ```

2. **Start the services:**
   ```bash
   docker network create proxy
   docker compose -f services/traefik/docker-compose.yaml up -d
   docker compose up -d
   ```

3. **Access the services:**
   - Ignition Gateway: http://ignition83.localtest.me
   - pgAdmin: http://postgres-pgadmin.localtest.me

> **Without Traefik:** If you prefer direct port access instead, skip the Traefik compose step and uncomment the `ports` sections in `docker-compose.yaml` for the services you need (e.g., `8088:8088` for Ignition, `5432:5432` for PostgreSQL).

## What's Included

- **Ignition 8.3** gateway for feature exploration
- **PostgreSQL** database with Liquibase migrations
- **pgAdmin** for database management
- **Traefik** integration for local development
- **Demo Project** showcasing 8.3 features
- **Custom Third-Party Modules** for extended functionality testing

### Pre-enabled Modules

- Event Stream
- Historian
- Perspective
- PostgreSQL Driver
- Web Development
- OPC UA
- Custom modules (see `services/third-party-modules/`)

## Services

| Service   | Description             | Access                                            |
|-----------|-------------------------|---------------------------------------------------|
| gateway   | Ignition 8.3 Gateway    | http://ignition83.localtest.me                    |
| database  | PostgreSQL              | Internal, or `localhost:5432` if port uncommented |
| pgadmin   | Database administration | http://postgres-pgadmin.localtest.me              |
| traefik   | Reverse proxy           | `services/traefik/docker-compose.yaml`            |
| liquibase | Database migrations     | Runs once on startup                              |

## Database Setup

The template includes Liquibase for database version control:

- **Main changelog:** `services/postgres/liquibase/main.yaml`
- **Table definitions:** `services/postgres/tables/`
- **Simulated data:** `services/postgres/simulated-data/`
- **Init scripts:** `services/postgres/init-sql/`

## Configuration

### Database Connection
- **Host:** postgres (internal) or localhost:5432 (external)
- **Database:** `postgres`
- **Username:** `postgres`
- **Password:** `P@ssword1!`

### pgAdmin Access
- **Email:** `admin@admin.com`
- **Password:** `root`

### Ignition Access
- **Username:** `admin`
- **Password:** `P@ssword1!`

## Prerequisites

- Docker and Docker Compose

## Purpose

This environment is designed for:
- **Exploring Ignition 8.3 features** - Test and demonstrate new capabilities
- **Custom module development** - Load and test third-party modules
- **Feature experimentation** - Safe environment for trying new approaches
- **Demo scenarios** - Showcase Ignition capabilities and integrations

## Local Development

The gateway is configured with:
- Quickstart disabled
- EULA automatically accepted
- A local development deployment mode enabled (`-Dignition.config.mode=local-dev`)
- Commissioning skipped
- Custom module loading from `services/third-party-modules/`

## File Structure

```
├── services/
│   ├── ignition/           # Gateway configuration and projects
│   │   └── projects/Demo/  # Demo project with 8.3 examples
│   ├── postgres/           # Database setup and migrations
│   ├── pgadmin/           # pgAdmin configuration
│   ├── traefik/           # Traefik reverse proxy
│   └── third-party-modules/ # Custom modules for testing
├── scripts/               # Utility scripts
└── docker-compose.yaml    # Main service definitions
```

## Customization

- **Add custom modules:** Place `.modl` files in `services/third-party-modules/`
- **Test new features:** Modify the Demo project in `services/ignition/projects/Demo/`
- **Configure gateway:** Update settings in `services/ignition/config/`
- **Modify modules:** Edit `docker-compose.yaml` to add/remove built-in modules
- **Database changes:** Update credentials in the compose file or add migrations to `services/postgres/liquibase/`
