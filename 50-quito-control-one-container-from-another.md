# Scenario
Description: You have a running container named docker-access. Another container nginx is present but in a stopped state. Your goal is to start the nginx container from inside the docker-access container.

You must not start the nginx container from the host system or any other container that is not docker-access. You can restart this docker-access container.

# Solution
```
docker rm -f docker-access

docker run -d --name docker-access -v /var/run/docker.sock:/var/run/docker.sock docker-access sleep infinity

docker exec docker-access docker run --name nginx nginx
```