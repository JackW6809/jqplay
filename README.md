# ![Alt text](assets/images/logo.png)
[jqplay](https://jqplay.jackoxi.systems) is a playground for [jq](https://github.com/stedolan/jq).

## Table of Contents
- [Development](#development)
   - [Dependencies](#dependencies)
      - [PostgreSQL](#postgresql)
      - [MySQL](#mysql)
   - [Makefile](#makefile)
- [Deployment - PostgreSQL](#deployment---postgresql)
   - [Environment Variables](#environment-variables)
   - [Docker-Compose](#docker-compose)
   - [Docker](#docker)
   - [Dockerfile](#dockerfile)
   - [Binary](#binary)
- [Deployment - MySQL](#deployment---mysql)
   - [Environment Variables](#environment-variables-1)
   - [Docker-Compose](#docker-compose-1)
   - [Docker](#docker-1)
   - [Dockerfile](#dockerfile-1)
   - [Binary](#binary-1)
- [License](#license)

## Development
### Dependencies
To develop `jqplay` you must have the following tools:\
[Go development environment](http://golang.org/doc/install)\
[Node.js](https://nodejs.org)\
[yarn](https://yarnpkg.com/)
#### PostgreSQL
You must have a [PostgreSQL](https://www.postgresql.org/) database running.
#### MySQL
You must have a [MySQL](https://www.mysql.com/) or [MariaDB](https://mariadb.org/) database running.
### Makefile
Running `make build` will build the `jqplay` binary and the frontend assets.

## Deployment - PostgreSQL
### Environment Variables
The following environment variables are required to run `jqplay`:\
`DATABASE_URL` - The database URL to connect to, in the format `postgres://user:pass@host:port/database`.\
`DATABASE_DRIVER` - The database driver to use, this must be set to `postgres`.

### Docker-Compose
You are able to make use of the [`docker-compose-postgres.yml`](docker-compose-postgres.yml) file to deploy `jqplay` with a database meaning little setup is required with the following command:
```bash
docker-compose -f docker-compose-postgres.yml up -d
```
It is recommended that you change the database credentials in the [`docker-compose-postgres.yml`](docker-compose-postgres.yml) file to something more secure.

### Docker
If you already have a postgreSQL database running, you can make use of my public Docker image to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
docker run -d -p 8080:8080 -e DATABASE_URL="postgres://jqplay-user:jqplay-pass@postegresql-host/jqplay-db?sslmode=disable" DATABASE_DRIVER="postgres" registry.jackoxi.systems/public-images/jq-play-server:latest
```

### Dockerfile
If you have a postgreSQL running, you can make use of the [`Dockerfile`](Dockerfile) to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
docker build -t jqplay --build-arg DATABASE_URL="postgres://jqplay-user:jqplay-pass@postegresql-host/jqplay-db?sslmode=disable" DATABASE_DRIVER="postgres".
docker run -d -p 8080:8080 jqplay
```

### Binary
If you have a postgreSQL database running, you can make use of the jqplay binary to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
DATABASE_URL="postgres://jqplay-user:jqplay-pass@postegresql-host/jqplay-db?sslmode=disable" DATABASE_DRIVER="postgres"./jqplay
```

## Deployment - MySQL
### Environment Variables
The following environment variables are required to run `jqplay`:\
`DATABASE_URL` - The database URL to connect to, in the format `user:pass@tcp(host:port)/database`.\
`DATABASE_DRIVER` - The database driver to use, this must be set to `mysql`.

### Docker-Compose
You are able to make use of the [`docker-compose-mysql.yml`](docker-compose-mysql.yml) file to deploy `jqplay` with a database meaning little setup is required with the following command:
```bash
docker-compose -f docker-compose-mysql.yml up -d
```
It is recommended that you change the database credentials in the [`docker-compose-mysql.yml`](docker-compose-mysql.yml) file to something more secure.

### Docker
If you already have a MySQL database running, you can make use of my public Docker image to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
docker run -d -p 8080:8080 -e DATABASE_URL="jqplay_user:jqplay_pass@tcp(db:3306)/jqplay_db" registry.jackoxi.systems/public-images/jq-play-server:latest
```

### Dockerfile
If you have a MySQL running, you can make use of the [`Dockerfile`](Dockerfile) to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
docker build -t jqplay --build-arg DATABASE_URL="jqplay_user:jqplay_pass@tcp(db:3306)/jqplay_db" .
docker run -d -p 8080:8080 jqplay
```

### Binary
If you have a MySQL database running, you can make use of the jqplay binary to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
DATABASE_URL="jqplay_user:jqplay_pass@tcp(db:3306)/jqplay_db" DATABASE_DRIVER="mysql" ./jqplay
```

# License
jqplay is released under the MIT license. See [LICENSE.md](https://github.com/owenthereal/jqplay/blob/master/LICENSE.md).
