# Scenario
Description: You're setting up a PostgreSQL database with replication, you decided to use Docker along with Docker Compose to make it easier to manage and test, after a few hours of work you finished the job and the master database is up and running, but you're having trouble with the replica.

You need to figure out what's wrong with the replica and fix it.

Since you are using Docker Compose, you can check the status of the running containers using docker compose ps or docker ps will do the job too). You may also want to check the logs of the containers.

All definition for the containers are inside the docker-compose.yml file. You can stand up the environment by running docker compose up -d and set it down by running `docker compose down`.

If you make any change to the docker-compose.yml file, you can restart the containers by running docker compose up -d --force-recreate.

# Solution
```
docker compose ps
docker compose logs -f

cp ./postgres/master/postgres.conf ./postgres/replica/postgres.conf

docker compose up -d --force-recreate
```