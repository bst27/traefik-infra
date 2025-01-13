# About
This example uses Traefik to work as a reverse proxy for three example Docker apps.

# Getting started
1. On first run you have to create three external docker networks. Every application has its own
   network which is only shared between the application and Traefik. By giving every application a dedicated network which is
   shared only with Traefik but not with other applications you make sure you get no naming conflicts,
   e.g. when two different applications use a docker container called "mysql" for the database.
   To create these three docker networks execute:
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
   docker compose -f app1/docker-compose.yml up -d &&
   docker compose -f app2/docker-compose.yml up -d &&
   docker compose -f app3/docker-compose.yml up -d
   ```
4. Make sure you to configure the following in your hosts file depending on your operating system:
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