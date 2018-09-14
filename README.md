# Docker workshop

Some introductory usage examples for the Docker workshop.

**Contents:**

- Create/edit Dockerfile
- Build Docker image
- Docker hub login
- Push image
- Start and stop a container with docker-compose
- Containers, data and volumes
- Build with Maven

*Questions to test your knowledge start with a Q.*

## Dockerfile

We want to build a Docker image with a Postgres database. An example `Dockerfile` can be found in the directory `dockerfile`.

*Q: where does the base image come from? What does the ENV command? Why multiple lines with \ ?*

## Build Docker image

To build a new image from the Dockerfile, run the following command:

    cd dockerfile
    docker build -t myimage .

*Q: what does the `-t` parameter? What is the `.` for?*

This builds a new image with the name `myimage` and tag `latest` (the default tag). The new image can be found with 

    docker images

## Docker hub login

Per default, Docker images are *pulled* from the central Docker hub (https://hub.docker.com/).
For example, get the latest Alpine Linux with
    
    docker pull alpine

*Q: how to search for Docker images? How to get a specific version?*

To access our private Docker hub (or registry), a login is required:

    docker login hub.1worldsync.de

If you just want to download images, the 'readonly' user is sufficient, but if
you want to *push* (upload) the images you have built you have to login with
a user with write access. Use the user 'docker' in this case. Passwords are
provided privately :-)

*Q: after a successful login the credentials are stored. Where?*

## Tag and Push image

To publish a previously built Docker image, it has to be tagged and pushed to the registry.

Tag the image with your Linux username so we can all push our own image. Then tag it
with the registry and push the image:

    docker tag myimage demo-<My_Userid>/myimage
    docker tag demo-<My_Userid>/myimage hub.1worldsync.de/demo-<My_Userid>/myimage
    docker push hub.1worldsync.de/demo-<My_Userid>/myimage

*Q: does every tag get a new image id? How to check? How to delete a tag and how is that different from deleting an image?*

## Start a container

The new image can be used to start a new container. Use the `docker run` command!

*Q: on which port does the Postgres database run? Try to connect! How to stop the container?*

It is easier to run a container with docker-compose. A `docker-compose.yml`file is required. To start the container using docker-compose, use

    docker-compose up -d

Check the status with `docker ps` or `docker-compose ps` and check the logs.

*Q: on which port is the Postgres database running? `expose`and `ports` - where's the difference? How to run the database on port 9999?*

## Stop the container 

A running container can be stopped with the 'docker stop' command.

*Q: does the container still exist after the stop command?*

To stop and remove the container that was started with docker-compose use

    docker-compose down

*Q: what's the difference of `docker-compose stop` and `docker-compose down`?*

## Delete images and containers

text

## Containers, data and volumes

After a container has been started, the data that is created is stored in the container filesystem. 
To store data outside of the container, host directories can be mounted or Docker volumes, a kind of data container, can be used. Volumes are the preferred solution!

We want to create a file in the container. This can be done by running a shell in the container with the 'exec' command:

    docker exec -ti myimg ash
    touch /test.txt
    exit
    
*Q: now stop the container - does the file still exist? Start the container again and check it! Stop and remove the container, then start it again: does the file still exist?*

The Postgres image uses a volume to store the data of the database. You can find the configuration in the 'docker-compose.yml' file. A container directory is mounted to the volume.

*Q: where is the volume ?*

## Do it with Maven

Go to the directory `maven-project` for an example project that builds the same image, but with Maven.
We use the `dockerfile-maven-plugin` from Spotify to build images in our software. Do not confuse it with the `docker-maven-plugin`!

To build the image run

    mvn clean install

*Q: what's the name and tag of the new image?*


## References

[Docker documentation](https://docs.docker.com/)

[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

[Docker compose reference](https://docs.docker.com/compose/compose-file/compose-file-v2/)

[Spotify Dockerfile Maven plugin](https://github.com/spotify/dockerfile-maven)
