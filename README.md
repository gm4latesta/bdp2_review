# BDP2-review

This repositery contains different files needed for creating a custom Jupiter Notebook Docker image and for building an application stack running multiple containers through docker-compose.

### .github/workflows 
Inside there is a docker-image.yml action used for connecting the GitHub repo to the DockerHub account. 

### docker 
Inside there is a Dockerfile that allow to install redis into the jupiter/minimal-notebook image. This avoid the problem of installis redis each time we need to use Jupyter. Indeed it is not needed to run the command `! pip install redis` each time, but just to `import redis`. 

For running the custom image use the command 
```
docker run -d --rm --name my_jupyter -v ~/review:/home/jovyan -p 80:8888 --network bdp2-net -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN="bdp2_password" --user root -e CHOWN_HOME=yes -e CHOWN_HOME_OPTS="-R" bdp2022/bdp2_review_docker:latest
```
For connecting to the Jupiter notebook use the URL http://public-IP-machine:80

### docker-compose.yml 
This file contains three services. One build the custom Jupiter image, one the Redis image, one the Portainer image.
The bdp2-net is the custom bridge for conneting all the containers. Removing it, docker-compose will create a new bridge automatically. 
In order to run this command docker-compose need to be available on the machine. 
```
sudo apt update && sudo apt install -y docker-compose
```
Remember to open the ports of the services to the machine. 

In order to start the three container use 
```
docker-compose up -d
```
In order to use https instead of http, insert the flag `GEN_CERT=yes` in environment of Jupyter. 

For removing the the application stack use the command
```
docker-compose down
```
