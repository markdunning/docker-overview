# Overview of the Docker container system

![UOS-logo](TUOS_PRIMARY_LOGO_FULL%20COLOUR.png)

Sheffield R meetup - 6th March 2018



Longer version of materials prepared for CRUK Cambridge available [here](https://bioinformatics-core-shared-training.github.io/docker-4-bioinformatics/)

Mark Dunning (@DrMarkDunning)
Bioinformatics Core Director

### Sheffield Bioinformatics Core
web : [sbc.shef.ac.uk](https://sbc.shef.ac.uk)  
twitter: [@SheffBioinfCore](https://twitter.com/SheffBioinfCore)  
email: [bioinformatics-core@sheffield.ac.uk](bioinformatics-core@sheffield.ac.uk)

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

## Run an interactive container

```
docker run -it ubuntu /bin/bash
```

- the `-it` arguments launches an interactive container
- 

## Volumes in Docker

```
docker run ubuntu ls
```

## Running RStudio through Docker

## Use Case 1:- Distributing software for a training course

## Use Case 2:- Distributing supplementary data for a publication

## The elephant in the room

