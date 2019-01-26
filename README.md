# Repository to Start Symfony 4
Repository with Docker to Start Symfony 4

## Requirements

Docker and docker-compose

## Installation

Run:

```
docker-compose up -d
```
and
```
docker-compose run php composer install
```

If you already apache server in your environment, change the ports in the `.env`

```
PORT_HTTP=80
PORT_HTTPS=443
PORT_ELK=81
```