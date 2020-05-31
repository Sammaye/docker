# Docker
My default Docker environment.

## How to use

It is quite simple, just change the name of the app container to replace `projectname` with your project name and set port 
numbers for the `app`, `mysql` and `mongodb` containers.

The reason you need ports for the two database containers is because nginx cannot tunnel both Http and TCP traffic down the 
same port, however, all other services such as PhpMyAdmin and Mongo Express are all routed via nginx.

## Environment Variables

The main box, `app`, supports a number of environment variables (not `ARG`) to configure it:

- `ENVIRONMENT` for the most part, does nothing, however, it is fed into the `start.sh` so you can use it to do environment specifics
- `PHP_VERSION` controls what php version gets installed, by default 7.2
- `NODE_VERSION` control what nodejs version gets installed, by default 10.x

## Design Considerations

### php

I do not use the official docker php image because it is not what I use in production. You could say the same for MongoDB a
nd MySQL but they actually are built from the same packages as I do in production. The php image from docker is built from a 
completely different set of sources and configuration to what I actually use in production.

### nginx

I installed nginx on the php box because it was just easier to manage and made for fewer containers.
