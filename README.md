# raspberrypi-pilot

A small collection of services and apps to run a Raspberry Pi–based pilot project: APIs, MQTT broker, a websocket gateway, and a Next.js frontend.

This repository contains multiple components; most are runnable via Docker Compose from the repository root.

## Quick overview

- `db_api_raspi/` — Python-based database API and synchronization service (has `requirements.txt`, `Dockerfile`, and a `create_db.py`/`robot.db`).
- `mqtt_broker/` — Mosquitto MQTT broker configuration and persistent data.
- `mqtt_websocket/` — Websocket gateway for MQTT (Python app + Dockerfile).
- `nautica_app/` — Next.js frontend app (TypeScript, TailwindCSS).

## Prerequisites

- Docker & Docker Compose
- Node.js (for local development of `nautica_app`)
- Python 3.10+ (for running Python services locally)

## Quickstart (recommended)

From the repository root, start all services with Docker Compose:

```bash
docker compose up -d
```

This will start the services defined in the top-level `docker-compose.yml` (which references the subprojects). Logs can be tailed with:

```bash
docker compose logs -f
```

## Running components individually

- db_api_raspi: build and run the service or use the included `docker-compose.yml` in `db_api_raspi/`.
  - To install Python dependencies locally: `python -m venv .venv && source .venv/bin/activate && pip install -r db_api_raspi/requirements.txt`.
- mqtt_broker: Mosquitto configuration is in `mqtt_broker/mosquitto/config/`. Persistent data and logs are in `mqtt_broker/mosquitto/data/` and `mqtt_broker/mosquitto/log/`.
- mqtt_websocket: see `mqtt_websocket/requirements.txt` and `mqtt_websocket/Dockerfile`.
- nautica_app: frontend located in `nautica_app/`. Install deps and run locally:

```bash
cd nautica_app
npm install
npm run dev
```

## Project layout

See top-level folders for per-component README or Docker configuration. High-level mapping:

- `db_api_raspi/` — backend API and DB sync utilities
- `mqtt_broker/` — MQTT broker files
- `mqtt_websocket/` — MQTT over WebSocket gateway
- `nautica_app/` — Next.js web application

## Development notes

- Use the top-level `docker-compose.yml` for integration testing and running everything locally.
- For frontend changes: edit files under `nautica_app/app/` and the components in `nautica_app/app/components/`.
- For backend Python services, use a virtual environment and lint/test where applicable.

## Contributing

Open issues and pull requests. Describe changes and include how to run/test them.

## License

Specify your license here (e.g. MIT). Add a `LICENSE` file if you choose a license.

---

If you'd like, I can also:

- Commit this `README.md` to git (I can stage & commit it locally). Currently the todo list includes that step and it's waiting to be run.
- Expand the README with per-component usage or add badges, examples, and a `CONTRIBUTING.md`.
