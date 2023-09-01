# Docker

## Basic Concepts

### Docker Client

Docker CLI, used to interact with the Docker Server

### Docker Server

Docker Daemon, creates images, runs containers, etc.

### Docker Container

Programs > system calls > kernel > Hard Drive

## Basic Commands

| Syntax                                              | Description                                                           |
| --------------------------------------------------- | --------------------------------------------------------------------- |
| Docker run                                          | Docker create + docker start                                          |
| Docker ps -all                                      | Watching all processes including ID´s                                 |
| Docker system prune                                 | Remove all stopped containers                                         |
| Docker stop id                                      |                                                                       |
| Docker kill id                                      |                                                                       |
| Docker exec                                         | To run an additional command in a container                           |
| Docker build -t docker_id/name_of_project:version . | Version >>> number/latest, Technically the version is the actual tag. |
| Docker run docker_id/name_if_project                | Run a taged image                                                     |

## Steps to create a Docker file

1. Specify a base image
2. Run some commands to install additional programs
3. Specify a command to run on container startup

### FROM

Use to specify the image we want to use as a base.

### CMD

Tell the container to run a certain command whenever it gets started in the future.

> The command creates a container.
> The output of that container is a temporary image containing the changes of that step.
> For each step we end up having a file System Snapshot and a startup command.
> At the end of the step the temporary container is removed and a snapshot of its image with the changes is taken

## Docker Build

Run a docker file and make an image out of it. The dot is the build context (set of files and folders we want to encapsulate in the container).

        Docker build -t docker_id/name_of_project:version .
