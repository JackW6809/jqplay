# ![Alt text](assets/images/logo.png) (PostgreSQL)
[jqplay](https://jqplay.jackoxi.systems) is a playground for [jq](https://github.com/stedolan/jq).

## Development
### Dependencies
To develop `jqplay` you must have the following tools:\
[Go development environment](http://golang.org/doc/install).\
[Node.js](https://nodejs.org)\
[yarn](https://yarnpkg.com/)\
[mySQL](https://www.mysql.com/) or [MariaDB](https://mariadb.org/)
### Makefile
Running `make` will build the `jqplay` binary and the frontend assets.

## Deployment
You can make use of one of the following methods to deploy `jqplay`:\
### Docker-Compose
You are able to make use of the [`docker-compose.yml`](docker-compose.yml) file to deploy `jqplay` with a database meaning little setup is required with the following command:
```bash
docker-compose up -d
```
It is recommended that you change the database credentials in the [`docker-compose.yml`](docker-compose.yml) file to something more secure.
```yml
version: "3.9"

services:
  jqplay:
    image: registry.jackoxi.systems/public-images/jq-play-server:latest
    depends_on:
      - db
    restart: always
    ports:
      - "8080"
    environment:
      DATABASE_URL: "postgres://jqplay-user:jqplay-pass@db/jqplay-db?sslmode=disable"
  db:
    image: postgres:latest
    restart: always
    environment:
      POSTGRES_USER: jqplay-user
      POSTGRES_PASSWORD: jqplay-pass
      POSTGRES_DB: jqplay-db
 ```

### Docker
If you already have a postgreSQL database running, you can make use of my public Docker image to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
docker run -d -p 8080:8080 -e DATABASE_URL="postgres://jqplay-user:jqplay-pass@postegresql-host/jqplay-db?sslmode=disable" registry.jackoxi.systems/public-images/jq-play-server:latest-mysql
```

### Dockerfile
If you have a postgreSQL running, you can make use of the [`Dockerfile`](Dockerfile) to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
docker build -t jqplay --build-arg DATABASE_URL="postgres://jqplay-user:jqplay-pass@postegresql-host/jqplay-db?sslmode=disable" .
docker run -d -p 8080:8080 jqplay
```

### Binary
If you have a postgreSQL database running, you can make use of the jqplay binary to deploy `jqplay` with the following command, replacing the `DATABASE_URL` environment variable with your database credentials:
```bash
DATABASE_URL="postgres://jqplay-user:jqplay-pass@postegresql-host/jqplay-db?sslmode=disable" ./jqplay
```

# License
jqplay is released under the MIT license. See [LICENSE.md](https://github.com/owenthereal/jqplay/blob/master/LICENSE.md).
