# Install Docker

The following command lines are done inside the `docker` directory. The files
with `docker-compose` and `Dockerfile` will build and run docker containers for
respective services.

### PostgreSQL

```bash
docker run -e POSTGRES_PASSWORD=postgres --publish 5433:5432 -d --name postgres-dev postgres:14.0-alpine
docker exec -it postgres-dev psql -h localhost -p 5432 -d postgres -U postgres
```

```sql
CREATE USER $user_name WITH PASSWORD $password;
ALTER USER $user_name WITH SUPERUSER;
CREATE DATABASE $db_name OWNER $user_name;
GRANT ALL PRIVILEGES ON DATABASE $db_name TO $user_name;
```

### Docker Run

```bash
docker run --name server-dev server -p 8000:8000 --env-file .env.dev
docker exec -it server-dev bash
```

### Docker Compose

```bash
docker-compose -f config/docker-compose.dev.yml up -d --build
```
