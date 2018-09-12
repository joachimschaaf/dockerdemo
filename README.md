# Docker workshop

Quick & dirty example for a Docker workshop.

**Contents:**

- Create/edit Dockerfile
- Build Docker image
- Docker hub login
- Push image
- Start and stop a container with docker-compose
- Build with Maven

*Questions to test your knowledge start with a Q.*

## Dockerfile

We want to build a Docker image with a Postgres database. An example `Dockerfile` can be found in the directory `dockerfile`.

## Build Docker image

To build a new image from the Dockerfile, run the following command:

    cd dockerfile
    docker build -t myimage .

*Q: what does the `-t` parameter? What is the `.` for?*

This builds a new image with the name and tag `myimage:latest`. The new image can be found with 

    docker images

## Docker hub login

Per default, Docker images are *pulled* from the central Docker hub (https://hub.docker.com/).
For example, get the latest ubuntu with
    
    docker pull ubuntu

*Q: how to search for Docker images?*

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

*Q: does every tag get a new image id? How to check? How to delete a tag?*

## Start a container

To start the container using docker-compose, use

    docker-compose up -d

Check the status with `docker ps` or `docker-compose ps` and check the logs.

*Q: on which port is the Postgres database from the example running? `expose`and `ports` - where's the difference? How to run the database on port 9999?*

To stop and remove the container use

    docker-compose down

*Q: what's the difference of `docker stop` and `docker down`?*

## Do it with Maven

Go to the directory `maven-project` for an example project that builds the same image, but with Maven.
We use the `dockerfile-maven-plugin` from Spotify to build images in our software. Do not confuse it with the `docker-maven-plugin`!

To build the image run

    mvn clean install

*Q: what's the name and tag of the new image?*



