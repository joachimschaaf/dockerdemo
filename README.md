# Docker workshop

Quick & dirty example for a Docker workshop.

**Contents:**

- Create/edit Dockerfile
- Build Docker image
- Docker hub login
- Push image
- Start and stop a container with docker-compose

## Dockerfile

An example `Dockerfile` can be found in `src/main/docker`.

## Build Docker image

To build a new image from the Dockerfile, run the following command:

    docker build -t myimage .

The builds a new image with the name (tag) `myimage`. The new image can be found with 

    docker images


## Docker hub login

To access our private Docker hub (or registry), a login is required.

If you just want to download images, the 'readonly' user is sufficient, but if
you want to push (upload) the images you have built you have to login with
a user with write access. Use the user 'docker' in this case. Passwords are
provided privately :-)

## Push image

text

## Do it with Maven

We use the `dockerfile-maven-plugin` from Spotify to build images in our software.

To build the image run

    maven clean install
    
The image will be built as hub.1worldsync.de/1worldsync/demo-postgres:1.0.0-SNAPSHOT


## Start a container

To start the container using docker-compose, use

    docker-compose up -d

To stop and remove the container use

    docker-compose down


