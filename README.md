# Perpl Test Docker Environment

Run Perpl tests with Docker.

Mount your Perpl directory into a PHP container and run static analysis, linters, or tests, typically using another container running MySql or Postgres.

## Installation

Checkout repository and cd into directory.

## Environment Variables

Communication between host and container is configured through environment variables:

| Variable | Description |
|---|---|
| `PERPL_HOME` | Path to Perpl repo, will be mounted at same location in the container and set as workdir. | `/home/me/repos/Perpl`
| `HOST_IP` | IP address of host for XDebug |


Note: When running Docker in rootless mode, host is accessed from container using host's external network IP:
```bash
HOST_IP=$(hostname -I | cut -d ' ' -f1) docker compose ...
```
When host's external network IP changes, restart the container.
## Run containers

- run with MySql:
```bash
docker compose -f docker-compose-mysql.yml -f docker-compose-php.yml up
```
- run with Postgres:
```bash
docker compose -f docker-compose-postgres.yml -f docker-compose-php.yml up
```

- run with both Postgres & MySql:
```bash
docker compose -f docker-compose-postgres.yml -f docker-compose-mysql.yml -f docker-compose-php.yml up
```
## Exec into container
```bash
docker exec -it propel-test-php /bin/bash
```

## Set up environment

Note that composer libraries and test schema classes are installed into the Perpl folder mounted from host, same as running the commands directly in host.

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

## Help & Support

Developed on Linux with rootless docker. If you run into issues or find this documentation could have made things easier, please open an issue or create a PR.
