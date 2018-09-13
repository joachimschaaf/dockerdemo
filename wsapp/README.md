# Publishing example

This directory contains a `docker-compose.yml` file with a stripped down Publishing as an example.

Check the configuration of the different components and modify them.

Then create a new stack on Rancher. This can be done with the Rancher-CLI command, e.g.

    rancher --env <environment...> up -s "publishing-test" --description "Publishing Test stack" -d

or in the Rancher UI by uploading the `docker-compose.yml` file.

Have fun!
