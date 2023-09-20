# Install Docker 

You should install docker based on your operation system following this link:

[https://docs.docker.com/engine/install](https://docs.docker.com/engine/install)

# Running the container

There are two types of images: some are built on our own machine or pulled from a remote repository and are now stored on our machine. In both scenarios, they are assumed to be local images, and the image name alone can be used. However, for remote images hosted on GitHub or other repositories, not on hub.docker.com, the full URL of the image should be used, not just the name.

Assuming you want to execute a command within a container that prints 'hello-world' to the console, this can be accomplished with the following command:

```bash
docker run some-image
```

This command runs the image with the name "some-image" on our local machine. It then prints "hello-world" to the console and exits instantly because the container's job is finished, resulting in an exit code of 0, which indicates success.

> Note that if the "some-image" couldn't be found on our local machine, Docker will automatically check the public repositories on Docker Hub for that image and attempt to pull it from there if available.

As you might be thinking, you don't want to use the predefined commands in our containers, and you want to run the container with modified datasets and configurations. there are two ways to accomplish that.

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
