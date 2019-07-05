This repository contains a Docker Compose definition to set up the authorization server required for OAuth2. It relies on [Ory Hydra](https://github.com/ory/hydra).

# Requirements
* Docker

# Set up
1. Copy .env.example to .env
2. In .env:
	* Set `SECRETS_SYSTEM` and `OIDC_SUBJECT_IDENTIFIERS_PAIRWISE_SALT` to random and secure strings
	* If you use a test environment without HTTPS, set `SERVE_PARAMS=--dangerous-force-http`
	* If you use HTTP for last mile, set `HTTPS_ALLOW_TERMINATION_FROM` to the SSL server's subnet
	* Set `SC_FRONTEND` to the client's URLs
	* Set Postgres credentials and update them inside `DSN`
3. If not running, start your external network
4. Set the network in docker-compose.yml
5. Run the database via `docker run --name 'hydra-postgres' -v data-hydra:/var/lib/postgresql/data -e POSTGRES_USER=hydra -e POSTGRES_PASSWORD=secret -e POSTGRES_DB=hydra --network schulcloudserver_schulcloud-server-network --expose 5432:5432 postgres:9.6`
6. Run `docker-compose up`

# Development
For development there is a docker-compose-test which already contains the Postgres Docker container.
You can use it with `docker-compose -f docker-compose-test.yml up`