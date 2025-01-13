# About
This is example app 2. To run this application follow these steps:

1. Make sure an external docker network called "app2-network" for this application exists:
   ```
   docker network inspect app2-network
   ```
2. If network already exists, skip this step, otherwise create it:
   ```
   docker network create app2-network
   ```
3. Use docker compose to start the application:
   ```
   docker compose up -d
   ```