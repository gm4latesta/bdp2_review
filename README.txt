The repositery bdp2_review contains a docker file needed for building an image that allows the use of redis in jupyter without installing it. 

The image is avaialable in the DockerHub repository called bdp2022/bdp2_review_docker

The docker run command for running that image is: docker run -d --rm --name my_jupyter -v ~/review:/home/jovyan -p 80:8888 --network bdp2-net -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN="bdp2_password" --user root -e CHOWN_HOME=yes -e CHOWN_HOME_OPTS="-R" bdp2022/bdp2_review_docker:latest. 

bdp2022/bdp2_review_docker:latest refers to the name of the image on DockerHub

