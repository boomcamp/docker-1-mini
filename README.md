# Project Summary

This is a brief introduction to Docker. Docker is a complex and useful tool, but
we are going to use it in a very limited way. Its main use case for us, is to
make the installation of other software seamless and idempotent (meaning the
installation will not have any side-effects on our base system).

We will learn how to install docker, as well as a small number of commands that
will be useful for us.

## Installation

### Ubuntu

1.  The easiest way to install Docker on ubuntu is by using `apt`

        sudo apt install docker.io

2.  Once you have docker installed there are a few other things you may want to
    configure to make using docker a little easier.

    - If you'd like to be able to run docker commands without having to use
      `sudo` run the following commands.

           sudo usermod -aG docker $USER
           newgrp docker

    - For more details see:
      https://docs.docker.com/install/linux/linux-postinstall/

3.  To test your installation run

        docker run hello-world

### Windows & MacOs

You can download docker for desktop here:
https://www.docker.com/products/docker-desktop

## What is Docker

For an in depth explanation you'll want the explore the documentation:
https://docs.docker.com/get-started/

For our purposes you won't need to have a deep understanding of exactly what
Docker is and can do, you'll just need to be able to run some simple commands to
manipulate Docker containers.

So what is it? Docker is a tool that allows us as developers to _containerize_
applications. In a way you can think of it as a very lightweight virtual
machine, that in our case, is just going to be running a specific application.
The advantage we are going to get by utilizing Docker is that we don't need to
modify our base system to get the Dockerized applications to run correctly, the
application is isolated in a Docker container, it makes configuration much
easier for us, and eliminates many variables that can occur when trying to
install software on many different machines (such as getting an entire class to
install software in a certain configuration).

## Key Concepts

- **Images** - These are pre-configured Docker containers, they can contain
  anything the image creator wants, but in many cases an image is designed to
  run a single application.

- **Containers** - You can think of these as currently running Docker images.
  - What do we mean by running? In Docker there is the concept of _starting_ an
    image, an image that has been _started_ is now running and could be
    considered a running Docker container.

For our use case we'll just be learning to fetch/run **Images**, stop running
**images**, list the running **Containers** on the system.

### Pull/Fetching Docker Images

1.  Here we'll fetch a simple Docker image that is hosted on the docker hub:
    https://hub.docker.com

         docker pull macinv/flask-example

    You'll see the image being downloaded

2.  Now that you've downloaded the image we can list all of the images that have
    been downloaded to our machine.

        docker images

### Running an image

1.  Let's run the image we just pulled down. The `run` command is what we want.
    There are a bunch of options available for this command referencing the
    documentation is a good idea.

    See: https://docs.docker.com/engine/reference/commandline/run/

        docker run -d -p 8080:8080 macinv/flask-example

    Command breakdown:

    - `run` the command to actually run the container
    - `d` runs the container in daemon mode
    - `-p` this option lets us bind ports from our host machine to the docker
      container. In this case we bind host (your machine) port 8080 to the
      container port 8080.
    - `macinv/flask-example` the name of the image we want to run

2.  Try out that command

### Active Docker Containers

1.  You started a Docker container in the last step, let's see if we can check
    on that container

        docker ps

    This command will list all of the currently _running_ containers on this
    host. Take a look at the metadata returned.

2.  So, we know this container is running, but what is it doing? Remember that
    port that was bound to the container (8080)? Let's open that address in a
    web browser and see what happens.

    Link: http://localhost:8080

    You'll see that the Docker container is running a web server sends back a
    message

    `Hello world! This is served by Flask in a Docker container`

### Stopping a Docker Container

1.  Now that we've seen a running Docker container, how do we stop one? Simple,
    run the following command.

        docker stop [container name]

    > Hint: unless explicitly set, container names will be random. You can set a
    > container name in the `run` command For example:
    > `docker run --name=example_app -d -p 8080:8080 macinv/flask-example`

## Finished

We covered the most basic aspects of Docker, but there's no need to stop there
if you're interested in learning more. There are more in-depth guides available,
check out this link to the official documentation: https://docs.docker.com/
