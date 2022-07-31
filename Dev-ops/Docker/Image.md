# Image

## Definition

Docker image is a set of application binaries and dependencies as well as metadata, settings and instruction on how to run the application.

## Image layers

Docker images are structure by layers. A layer is a change to the previous layer, which can change the image size of not.
You could use the `docker image history` for inspecting the image layers.

Each layer would be unique on a machine by its SHA, so that it would help reduce the space, build time as well as the transfer cost.


A container is running by putting a read-write layer on top of image layers. 
If container change a file, docker would copy the file from the image layers and change it in the read-write layer (Copy on Write).

## Image name

Docker images are access via format `<repo>/<tag>` or id.
The repo need to be in the format of `<user/organization>/image` unless it is an offical image - you must comply this to be able to push the image to the docker hub.
By default, if it is not specified, the `lasted` tag wil be used.

You could have multiple tag on the same image. 
Eventhough it may list multiple times, it only saved once thank to image layer structure.
Create a image tag via the command: `docker image tag <old-image> <new-image>`.

## Dockerfile

`Dockerfile` is the blueprint for create the image. 
To build a image `docker image build <path/url>`, some popular options: 

* `-t` for specify the image tag
* `-f` for specify the file name, by default it would be `Dockerfile`


A `Dockerfile` contains multiple step, which will be a docker layer when buiding the image.
The steps will be exucuted top down.
Some popular `Dockerfile` step:

* `FROM`- for specify the base image
* `RUN`
* `ENV` - for setting environment variable
* `COPY <source> <target>` - for copy files from the current directory to image current directory
* `WORKDIR` - for changing the current working directory ( create one if the directory does not exist yet )
* `CMD [ <list-of-command-part> ]` - the default running command. 
  This is required and only the last one applied ( you can skip it if the base image already contains it )
* `EXPOSE` - for exposing the port of the container (not the host)

Best practices for writing `Dockerfile`:

- To take advantage of layering structure, you put frequenly change layers last.
- Since each step is saved as a layer, you should minimize the number of steps to reduce the saving space.
- Consider exposing logs to `/dev/error` and `/dev/log` so that docker can access it ( most base images do that for you)
