# Kuma for Docker

## Install

To start using this container, start by cloning the repository:

```bash
git clone https://github.com/hawara-es/kuma-for-docker.git
cd kuma-for-docker
```

## Configure

Once you have cloned the repository, create a new `.env` file and set your safe passwords there.

```bash
cp env.example .env
```

## Docker Container

To start the container with minimum settings, just run:

```bash
docker compose up -d
```

Which is equivalent to loading the default `docker-compose.yml`:

```bash
docker compose -f docker-compose.yml up -d
```

To start the container with the 3306 port binded to the host, use the `docker-compose.port.yml` file:

```bash
docker compose -f docker-compose.yml -f docker-compose.port.yml up -d
```

To start the container with Traefik support, use the `docker-compose.traefik.yml` file:

```bash
docker compose -f docker-compose.yml -f docker-compose.traefik.yml up -d
```

Traefik support works very well with its corresponding sibling project: [traefik-for-docker](https://github.com/estudio-hawara/traefik-for-docker).

### The `dc` Helper

To standardize calling Docker from the project root, the `dc` filename has been added to this project's `.gitignore`.

You are encouraged to create it either if you will be only using the standard file:

```bash
#!/bin/bash
docker compose -f docker-compose.yml "$@"
```

... or if you will also be using the open port file:

```bash
#!/bin/bash
docker compose -f docker-compose.yml -f docker-compose.port.yml "$@"
```

... or for usage with Traefik:

```bash
#!/bin/bash
docker compose -f docker-compose.yml -f docker-compose.traefik.yml "$@"
```

Thanks to this, and after giving executing permissions to the new file, you will be able to use this short hand:

```bash
# chmod +x dc
./dc up -d
```
