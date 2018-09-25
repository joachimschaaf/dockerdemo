# Publishing example

This directory contains a `docker-compose.yml` file with a stripped down Publishing as an example.

Check the configuration of the different components and modify them.

Then create a new stack on Rancher. This can be done with the Rancher-CLI command, e.g.

    rancher --env <environment...> up -s "publishing-test" --description "Publishing Test stack" -d

or in the Rancher UI by uploading the `docker-compose.yml` file.

*Note*: during the first start of the stack, the Docker images have to be pulled before they can be started. Especially the Oracle image my take too long so that the Publishing installation will fail. You can pull the Oracle image manually before starting the stack.

## Deploy through the Rancher GUI

Use the docker-compose.yml to create a Stack in the Rancher GUI in our Frankfurt DEV Environment. Choose a name with your username in it to avoid conflicts.

*Q: How do you check, if the publishing is installed and ready to use?*
*Q: Is there a quick way to access the Shell through the GUI?*

## Modify the stack

Manually modify the stack and add the Anomalies Service. The image name for this is:

    hub.1worldsync.de/1worldsync/anomaly-detection:1.3

and the port to expose is the Port 9000. To add a new service to the Stack go to the Stack Overview and do an "Add Service", fill out the form, don't forget the expose of the port!

*Q: How can you check and modify the port configuration of a container?*

## Re-configure the publishing

To access the Anomalies Detection Service it needs to be enabled in the publishing installation. Upgrade the container/service and add the following environment variable:

    WS_USE_ANOMALIES_DETECTION=true

*Q: How can you check if the variable is applied to the Container? Hint: check the container settings*

## Access to the Database Container using the Rancher Client

Find the container name using rancher ps. Do a 

    rancher exec -it <container-id> bash

## Copy a file into the container using the rancher client

You need the Docker Container of the Database Container for this! Use the following command to find the right id:

    rancher --host fra1lap6d.1worldsync.com docker ps

Use the following command to copy a file to the container:

    rancher --host fra1lap6d.1worldsync.com docker cp README.md <container-id>:/tmp

This can be used to copy a dump file into the container to import it.


Have fun!
