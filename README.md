# raspberrypi-pilot

A collection of services and apps for a Raspberry Pi–based pilot project, including APIs, an MQTT broker, a WebSocket gateway, and a Next.js frontend.

This repository contains multiple components, most runnable via Docker Compose from the repository root.

## Overview

- `db_api_raspi/` — Python-based database API and synchronization service (includes `requirements.txt`, `Dockerfile`, and `create_db.py`/`robot.db`).
- `mqtt_broker/` — Mosquitto MQTT broker configuration and persistent data.
- `mqtt_websocket/` — WebSocket gateway for MQTT (Python app with `Dockerfile`).
- `nautica_app/` — Next.js frontend app (TypeScript, TailwindCSS).

## Prerequisites

- Docker & Docker Compose
- Node.js (for local development of `nautica_app`)
- Python 3.10+ (for running Python services locally)

## Quickstart

From the repository root, start all services with Docker Compose:

```bash
docker compose up -d
```

Tail logs with:

```bash
docker compose logs -f
```

**Important**: Before starting, modify the `.env` file in the repository root (or create one from the example) and set the correct IP addresses for your Raspberry Pi and robot. Typical entries:

```env
# IP of the Raspberry Pi running edge services
RASPI_IP=192.168.x.x

# IP of the robot to monitor
ROBOT_IP=192.168.y.y
```

Ensure these addresses are reachable from your Docker Compose machine. Services read these from the environment to configure API/MQTT endpoints.

Additionally, update the address in [`nautica_app/app/constants.ts`](nautica_app/app/constants.ts) with the correct Raspberry Pi details.

## Running Components Individually

- **db_api_raspi**: Build and run the service or use the included `docker-compose.yml` in `db_api_raspi/`.
  - To install Python dependencies locally: `python -m venv .venv && source .venv/bin/activate && pip install -r db_api_raspi/requirements.txt`.
- **mqtt_broker**: Mosquitto config in `mqtt_broker/mosquitto/config/`. Persistent data and logs in `mqtt_broker/mosquitto/data/` and `mqtt_broker/mosquitto/log/`.
- **mqtt_websocket**: See `mqtt_websocket/requirements.txt` and `mqtt_websocket/Dockerfile`.
- **nautica_app**: Frontend in `nautica_app/`. Install dependencies and run locally:

  ```bash
  cd nautica_app
  npm install
  npm run dev
  ```

## Project Layout

See top-level folders for per-component README or Docker configs. High-level mapping:

- `db_api_raspi/` — Backend API and DB sync utilities
- `mqtt_broker/` — MQTT broker files
- `mqtt_websocket/` — MQTT over WebSocket gateway
- `nautica_app/` — Next.js web application

## Development Notes

- Use the top-level `docker-compose.yml` for integration testing and local runs.
- For frontend changes: Edit files under `nautica_app/app/` and components in `nautica_app/app/components/`.
- For backend Python services: Use a virtual environment and lint/test where applicable.

## Contributing

Open issues and pull requests. Describe changes and include run/test instructions.

## License

Specify your license here (e.g., MIT). Add a `LICENSE` file if you choose one.
