# Overview of the Docker container system

Sheffield R meetup - 6th March 2018

Longer version of materials prepared for CRUK Cambridge available [here](https://bioinformatics-core-shared-training.github.io/docker-4-bioinformatics/)

## Basics
https://docs.docker.com/engine/docker-overview


## Obtaining Docker

- Recent [Mac OSX](https://docs.docker.com/docker-for-mac) (10.10.3 and newer) and [Windows 10](https://docs.docker.com/docker-for-windows) have easy installation
- Older OS require [Docker Toolbox](https://docs.docker.com/toolbox/overview). Older Windows may require some *virtualisation* settings
- Can install in Unix through `apt-get`

## Running your first docker container

If using Windows or Mac open a Command Prompt or terminal

```
docker run ubuntu echo "Hello World"
```

- downloads the `ubuntu` operating system image (if not already present)
- launches the ubuntu container
- runs the command echo "Hello World"
- exits

```
docker run ubuntu date
docker run cat /etc/lsb-release
docker run ubuntu:14.04 cat /etc/lsb-release
```

## R



## Running RStudio through Docker

## Use Case 1:- Distributing software for a training course

## Use Case 2:- Distributing supplementary data for a publication

## The elephant in the room

