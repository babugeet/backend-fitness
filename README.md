# jwt-auth

Fitness Tracker API with JWT authentication.

## Run locally

Requirements: Go 1.22+ and Docker with Docker Compose.

1. Start the local PostgreSQL database from this directory:

```sh
docker compose up -d db
```

2. Start the API:

```sh
export JWT_SECRET="$(openssl rand -hex 32)"
go run .
```

The API listens on `http://localhost:8080`. `JWT_SECRET` is required and
should be a private random value. The default database settings match the
Compose service. Override them with `DB_HOST`, `DB_USER`,
`DB_PASSWORD`, `DB_NAME`, and `DB_PORT` when needed. The browser app origin
defaults to `http://localhost:8081`; override `CORS_ALLOWED_ORIGINS` with a
comma-separated list to use another origin.

3. In another terminal, serve the standalone browser app:

```sh
cd ../frontend-fitness
python3 -m http.server 8081
```

4. Open `http://localhost:8081` and create an account.

Stop the database with `docker compose down`. Add `-v` only when you also want
to delete its local data volume.

## Container image

Build the API image with `docker build -t backend-fitness .`. Provide
`JWT_SECRET` and the database environment variables when running the container.
