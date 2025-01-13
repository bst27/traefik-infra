# About
This example uses Traefik to work as a reverse proxy for three example Docker apps.

# Getting started
1. On first run you have to create three external Docker networks. Every application has its own
   network which is only shared between the application and Traefik. By giving every application a dedicated network which is
   shared only with Traefik but not with other applications you make sure you get no naming conflicts,
   e.g. when two different applications use a Docker container called "mysql" for the database.
   To create these three Docker networks execute:
    ```
    docker network create app1-network &&
    docker network create app2-network &&
    docker network create app3-network
    ```
2. Use docker compose to start Traefik:
   ```
   docker compose up -d
   ```
3. Use docker compose to start the three separate applications:
   ```
   docker compose -f ../app1/docker-compose.yml up -d &&
   docker compose -f ../app2/docker-compose.yml up -d &&
   docker compose -f ../app3/docker-compose.yml up -d
   ```
4. Make sure to configure the following in your hosts file depending on your operating system:
   ```
   127.0.0.1	app1.localhost
   127.0.0.1	app2.localhost
   127.0.0.1	app3.localhost
   ```
5. Use your web browser to access the three docker applications served by Traefik:

   | App | URL                                            |
   |-----|------------------------------------------------|
   | 1   | [http://app1.localhost](http://app1.localhost) |
   | 2   | [http://app2.localhost](http://app2.localhost) |
   | 3   | [http://app3.localhost](http://app3.localhost) |
6. Use your web browser to access the Traefik dashboard at [http://localhost:8080](http://localhost:8080/)

# Running in production
If you want to run this example setup in production with valid HTTPS certificates issued
for your domains from Lets Encrypt follow these steps. You probably want to do this on your web server:

1. Make sure to setup DNS A or CNAME records at your DNS registry for your three domains pointing to your web
   server and give them some time to propagate, at least a few minutes.
2. Make sure to create three Docker networks if not already existing:
   ```
   docker network create app1-network &&
   docker network create app2-network &&
   docker network create app3-network
   ```
3. Copy and customize the .env file for Traefik, e.g. fill in your email address for ACME:
   ```
   cp .env.production.example .env && nano .env
   ```
4. Use docker compose to start Traefik:
   ```
   docker compose -f docker-compose.production.yml up -d
   ```
5. Copy and customize the .env file for the three apps, e.g. fill in the domain names:
   ```
   cp ../app1/.env.production.example ../app1/.env && nano ../app1/.env &&
   cp ../app2/.env.production.example ../app2/.env && nano ../app2/.env &&
   cp ../app3/.env.production.example ../app3/.env && nano ../app3/.env
   ```
6. Use docker compose to start the three separate applications:
   ```
   docker compose -f ../app1/docker-compose.production.yml up -d &&
   docker compose -f ../app2/docker-compose.production.yml up -d &&
   docker compose -f ../app3/docker-compose.production.yml up -d
   ```
7. Use your web browser to access the three Docker applications served by Traefik at your domain
   names with valid HTTPS certificates.
