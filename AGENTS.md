# Base44 Dev Environment

This is a CI/CD lab project: a minimal Flask app (`app/app.py`) that returns "Container Technologies", originally served via gunicorn on port 8000.

## Running in the Base44 sandbox

`docker compose -f docker-compose.base44.yml up -d` starts the app on host port 3000.

- Uses the `python:3.10-alpine3.21` base image with the `app/` directory bind-mounted.
- Runs the Flask dev server with `--reload` (live reload on edits to `app/app.py`).
- Dependencies are installed from `app/requirements.txt` on container startup.
- Healthcheck probes `http://localhost:3000/` (the root route).

## Notes

- No database, no external services, no secrets required.
- The repo's own `app/docker-compose.yml` builds a production image with gunicorn on port 8000 — not used for dev.
- `infra/` and `app/deploy/` contain Terraform/ECS deployment configs (not needed to run the app locally).
- Tests: `python app/test.py` (unittest, checks the root route returns 200 + "Container Technologies").
