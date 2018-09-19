# Publishing example

This directory contains a `docker-compose.yml` file with a stripped down Publishing as an example.

Check the configuration of the different components and modify them.

Then create a new stack on Rancher. This can be done with the Rancher-CLI command, e.g.

    rancher --env <environment...> up -s "publishing-test" --description "Publishing Test stack" -d

or in the Rancher UI by uploading the `docker-compose.yml` file.

*Note*: during the first start of the stack, the Docker images have to be pulled before they can be started. Especially the Oracle image my take too long so that the Publishing installation will fail. You can pull the Oracle image manually before starting the stack.

Have fun!
