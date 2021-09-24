# local-postgres-using-docker
The simple and clean way to run Postgres on local using docker

### Pre-requisites:
- Docker

### Download, configure and run Postgres:
- Download image: `docker pull postgres`
- Create data dir: `mkdir postgres-data`
- Absolute path to data dir: `export DATA_DIR_PATH="$(pwd)/postgres-data"`
- Run Postgres:
  `docker run -d \
  --name dev-postgres \
  -e POSTGRES_PASSWORD=Pass2020! \
  -v ${DATA_DIR_PATH}:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres`
- Check that the container is running: `docker ps`

### Download, configure and run pgAdmin instance

- Download image: `docker pull dpage/pgadmin4`
- Run pgAdmin:
  `docker run \
  -p 80:80 \
  -e 'PGADMIN_DEFAULT_EMAIL=user@domain.local' \
  -e 'PGADMIN_DEFAULT_PASSWORD=SuperSecret' \
  --name dev-pgadmin \
  -d dpage/pgadmin4`
- Check that the container is running: `docker ps`
- Capture `IPAddress` of Postgres instance:
  `docker inspect dev-postgres -f "{{json .NetworkSettings.Networks }}"`
- Visit http://localhost:80 and login with username: `user@domain.local` & password: `SuperSecret`
- `Add New Server` with details in Connection tab:
 Host name/address: `IPAdress`
 Port: 5432
 Maintenance database: postgres
 Username: postgres
 Password: Pass2020!

### Cleanup commands

##### Postgres container:
- Stop container: `docker stop dev-postgres`
- Delete container: `docker rm dev-postgres`

##### pgAdmin container:
- Stop container: `docker stop dev-pgadmin`
- Delete container: `docker rm dev-pgadmin`

### References
https://towardsdatascience.com/local-development-set-up-of-postgresql-with-docker-c022632f13ea

