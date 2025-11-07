## Environment Variables

| Variable | Description |
|---|---|
| `PERPL_HOME` | Path to Perpl repo, will be mounted at same location in the container and set as workdir. | `/home/me/repos/Perpl`
| `HOST_IP` | IP address of host for XDebug |


Note: When running Docker in rootless mode, host is accessed from container using host external network IP:
```bash
HOST_IP=$(hostname -I | cut -d ' ' -f1) docker compose ...
```
## Startup

- run with MySql:
```bash
docker compose -f docker-compose-mysql.yml -f docker-compose-php.yml up`
```
- run with Postgres:
```bash
docker compose -f docker-compose-postgres.yml -f docker-compose-php.yml up
```

- run with both Postgres & MySql:
```bash
docker compose -f docker-compose-postgres.yml -f docker-compose-mysql.yml -f docker-compose-php.yml up`
```
## Exec into container
```bash
docker exec -it propel-test-php /bin/bash
```

## Setup
- install dependencies
```bash
composer update
```
- setup database and build fixtures
```
init-mysql
init-postgres
init-sqlite
```

## Run tests
```bash
testagnostic
testmysql
testpostgres
testsqlite
```

## Code style and static analysis

```bash
stan
psalm
lint-clean
lint
```
- on edited files only (`git add` new files before running)
```
stan-edited
lint-clean-edited
lint-edited
```
## Other aliases

To find out about other aliases, enter `aliases` or check `/root/bash_aliases`

## XDebug Server Configuration

Example configuration (VSCode, Docker in rootless mode): 
```json
    "configurations": [
        {
            "name": "...",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "hostname": "0.0.0.0",
        },
```
