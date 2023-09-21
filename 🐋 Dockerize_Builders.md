- [Install Docker](#install-docker)
- [Dockerfile](#dockerfile)
- [Build](#build)
- [Container](#container)
  - [Running the container](#running-the-container)
  - [Reattach to the Container](#reattach-to-the-container)
  - [List of containers](#list-of-containers)

# Install Docker 

You should install docker based on your operation system following this link:

[https://docs.docker.com/engine/install](https://docs.docker.com/engine/install)

# Dockerfile

Docker image can be created by writing a Dockerfile in the root of a project and then running `Docker build` in that project.

**What is a Dockerfile?** It's a set of instructions that tells the Docker engine the steps to follow in order to create the image.

Here is a sample which is for LADy Project:

```Dockerfile
############## Stage 1
# The first line always have to indicate the image that docker will use to run following commands in
FROM python:3.8.12-slim-bullseye

# Sets the working directory in the docker image 
WORKDIR /app

# Installing essential build tools for python and libraries like GCC
RUN apt update
RUN apt install -y build-essential

############## Stage 2
# Install dependencies from requirements.txt
COPY requirements.txt .
RUN pip install -r requirements.txt

RUN python -m spacy download en_core_web_sm
RUN python -m nltk.downloader stopwords
RUN python -m nltk.downloader punkt

############## Stage 3
# Copy octis library files to the container
COPY ./src/octis ./src/octis

# Setup octis
# It seems it has relative imports, so we need to change the working directory
WORKDIR /app/src/octis

RUN python setup.py install

############## Stage 4
# Get back to the root directory and copy the rest of the files
WORKDIR /app
COPY . .

# Changing working directory to src for later use at commandline
WORKDIR /app/src

RUN python ./main_exp_slim.py
```

As you can see, there are multiple stages that is separated for better understanding. Please keep in mind that this is for demonstration purposes, and the caching and staging processes by Docker engine are different from these stages.

Assuming a file has changed in the project, and when creating a new image, the goal is to avoid having the Docker engine run every step in the Dockerfile because there haven't been changes to the dependencies or the base image used. The expectation is that the Docker engine should begin running from Stage 4. In this Dockerfile, this behavior would occur. However, there is another option, as seen in many Dockerfiles. In Stage 2, instead of copying just the `requirements.txt` file, the command `COPY . .` can be used, eliminating the need to manually copy other files repeatedly. While this is true, it's important to note that when a file changes, the dependencies need to be reinstalled with every `docker build`, and this process can be time-consuming and not cache-friendly.

Used Commands:

| Command | Description                                                                |
| ------- | -------------------------------------------------------------------------- |
| FROM    | image you are forking from                                                 |
| COPY    | copy local files into the container                                        |
| RUN     | run a command inside container but in build time                           |
| WORKDIR | set the working directory where the RUN commands and other commands excute |

# Build

After writing your `Dockerfile` in your project's base directory, the image could be built by running the following command with the `-t` flag to tag this image for future use:

```bash
docker build . -t [image-tag]
```

After running this command, the image can be found in the list of Docker images. You can verify this by using the `docker image ls` command, which presents a list of all images. You should look for the image with the tag you specified.

# Container

As it may have been observed, the application hasn't been run yet. There is now an image that includes the application, prepared with installed requirements and environments. When running the application, there are several ways to consider, depending on the application type:

1. **For Applications with a Server:**
   If the application has a server that can be accessed by users through a specific port, port forwarding should be utilized. Prior to that, it is important to ensure that the required port is exposed to the public in the Dockerfile.

2. **For Data Science Projects or Non-Server Applications:**
   In many data science projects, there isn't an application with a server for user interaction. In such scenarios, the following steps should be followed:

   - It's important to note that the working directory in the last line of the Dockerfile can be changed to improve command organization in the future. For instance, instead of utilizing `/src/a/b/c/d`, one can modify the directory to `src` and employ `/a/b/c/d` or tailor it to suit the specific use case.

## Running the container

There are two types of images: some are built on our own machine or pulled from a remote repository and are now stored on our machine. In both scenarios, they are assumed to be local images, and the image name alone can be used. However, for remote images hosted on GitHub or other repositories, not on hub.docker.com, the full URL of the image should be used, not just the name.

Assuming you want to execute a command within a container that prints 'hello-world' to the console, this can be accomplished with the following command:

```bash
docker run some-image
```

This command runs the image with the name "some-image" on our local machine. It then prints "hello-world" to the console and exits instantly because the container's job is finished, resulting in an exit code of 0, which indicates success.

> Note that if the "some-image" couldn't be found on our local machine, Docker will automatically check the public repositories on Docker Hub for that image and attempt to pull it from there if available.

As you might be thinking, you don't want to use the predefined commands in our containers, and you want the user to run the container with modified datasets and configurations. there are two ways to accomplish that.

1. To attach a shell to the container, similar to SSH, you can use the following command: `docker run some-image --name my-container /bin/bash`. This command creates a container with the name `my-container` and attaches to it using Bash. If you don't want to attach to it immediately, you can add the `-d` flag, which indicates that the container should be detached after creation, allowing you to re-attach to it later.
2. To run a command similar to the previous 'hello-world' example but with modifications, follow the same steps as the first one. However, instead of `/bin/bash` at the end, you should replace it with your desired command. For example: `docker run some-image python main.py --model one --parallel --dataset dummy`.

## Reattach to the Container

the running container could be reattached with following command:
`docker exec -it container-name /bin/bash`

but if the container is stopped it can be started with the following command:
`docker start container-name`

## List of containers

it could be fetched via the following command:
`docker ps -a`
