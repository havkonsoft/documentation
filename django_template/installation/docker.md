# Install Docker & Docker Compose

### Table of Contents

- [Install Docker](#install-docker)
- [Install Docker Compose](#install-docker-compose)
- [Docker Postgres](#docker-postgres)

## Install Docker

First, update your existing list of packages:

```bash
sudo apt update
```

Next, install a few prerequisite packages which let `apt` use packages over
HTTPS:

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

Then add the GPG key for the official Docker repository to your system:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Add the Docker repository to APT sources:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update your existing list of packages again for the addition to be recognized:

```bash
sudo apt update
```

This will also update our package database with the Docker packages from the
newly added repo. Make sure you are about to install from the Docker repo
instead of the default Ubuntu repo:

```bash
apt-cache policy docker-ce
```

You'll see output like this, although the version number for Docker may be
different:

```bash
docker-ce:
  Installed: (none)
  Candidate: 5:20.10.14~3-0~ubuntu-jammy
  Version table:
     5:20.10.14~3-0~ubuntu-jammy 500
        500 https://download.docker.com/linux/ubuntu jammy/stable amd64 Packages
     5:20.10.13~3-0~ubuntu-jammy 500
        500 https://download.docker.com/linux/ubuntu jammy/stable amd64 Packages
```

Finally, install Docker:

```bash
sudo apt install docker-ce
```

Docker should now be installed, the daemon started, and the process enabled to
start on boot. Check that it's running:

```bash
sudo systemctl status docker
```

The output should be similar to the following, showing that the service is
active and running:

```bash
Output
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-04-01 21:30:25 UTC; 22s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 7854 (dockerd)
      Tasks: 7
     Memory: 38.3M
        CPU: 340ms
     CGroup: /system.slice/docker.service
             └─7854 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```

If you want to avoid typing sudo whenever you run the docker command, add your
username to the docker group.

```bash
sudo usermod -aG docker ${USER}
```

Since the user for vagrant is vagrant, we will use vagrant for ${USER}

```bash
sudo usermod -aG docker vagrant
```

Log out Ubuntu and log back in to see the result

```bash
docker --version
```

## Install Docker Compose

First, confirm the latest version available in their
[releases page](https://github.com/docker/compose/releases). At the time of this
writing, the most current stable version is 2.24.0.

The following command will download the 2.24.0 release and save the executable
file at /usr/local/bin/docker-compose, which will make this software globally
accessible as docker-compose:

```bash
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
```

Next, set the correct permissions so that the `docker-compose` command is
executable:

```bash
chmod +x ~/.docker/cli-plugins/docker-compose
```

To verify that the installation was successful, you can run:

```bash
docker compose version
```

You'll see output similar to this:

```bash
Output
Docker Compose version v2.3.3
```

The following command lines are done inside the `docker` directory. The files
with `docker compose` and `Dockerfile` will build and run docker containers for
respective services.

## Install PostgreSQL using Docker

### Docker Compose

You can install PostgresSQL using the `yml` format in `docker-compose.yml` file.
Run `docker compose -f docker-compose.yml up -d --build` to install the image
and spin up the container.

```yml
db:
  image: postgres:14.0-alpine
  container_name: postgres-${BUILD_ENV}
  volumes:
    - postgres_data:/var/lib/postgresql/data/
  ports:
    - 5432:5432
  networks:
    - local-network
  environment:
    - POSTGRES_USER=postgres
    - POSTGRES_PASSWORD=mysecretpassword
    - POSTGRES_DB=postgres
```

#### The first database in Postgres should name postgres for superuser access. If this is not set up properly, accessing the database with default user will be difficult.

## Docker Postgres

Using the Docker command lines can also install PostgreSQL in Docker.

```bash
docker run -e POSTGRES_PASSWORD=mysecretpassword --publish 5433:5432 -d --name postgres-dev postgres:14.0-alpine
docker exec -it postgres-dev psql -h localhost -p 5432 -d postgres -U postgres
```

On the PostgreSQL console, you can create new databaes and user for your
project.

```sql
CREATE USER $user_name WITH PASSWORD $password;
ALTER USER $user_name WITH SUPERUSER;
CREATE DATABASE $db_name OWNER $user_name;
GRANT ALL PRIVILEGES ON DATABASE $db_name TO $user_name;
```

#### Docker Run with Environment File

```bash
docker run --name server-dev server -p 8000:8000 --env-file .env.dev
docker exec -it server-dev bash
```

#### Backup Database

```bash
docker exec -t postgres-dev pg_dumpall -c -U postgres > dump_`date +%d-%m-%Y"_"%H_%M_%S`.sql
```

#### Restore Database

```bash
cat your_dump.sql | docker exec -i postgres-dev psql -d serverdb -U serverusr
```
