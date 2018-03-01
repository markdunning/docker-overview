# Overview of the Docker container system

![](https://www.docker.com/sites/default/files/vertical_large.png)

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


[Docker](https://www.docker.com) is an open platform for developers to build and ship applications, whether on laptops, servers in a data center, or the cloud.

- Or, it is a (relatively) painless way for you to install and try out Bioinformatics software. 
- You can think of it as an isolated environment inside your exising operating system where you can install and run software without messing with the main OS
- Really useful for testing software
- Clear benefits for working reproducibly
    + instead of just distributing the code used for a paper, you can effectively share the computer you did the analysis on
- For those of you that have used Virtual Machines, it is a similar concept
## Installing Docker

### Mac

- [Mac OSX - 10.10.3 or newer](https://www.docker.com/docker-mac)
- [Older Macs](https://download.docker.com/mac/stable/DockerToolbox.pkg)

### Windows

- [Windows 10](https://www.docker.com/docker-windows)
    + also requires some virtualisation settings
- [Older Windows](https://download.docker.com/win/stable/DockerToolbox.exe)


Once you have installed Docker using the insructions above, you can open a terminal (Mac) or command prompt (Windows) and run the following to download a container for the Ubuntu operating system;

```
docker pull ubuntu
```

To run any software inside the container we can do;

```
docker run ubuntu echo "Hello World"
```

- run the docker container for the Ubuntu operating system
- run the `echo` command within this operating system
- exit

To use the container in interactive mode we have to specify a `-it` argument. Which basically means that it doesn't exit straight away, but instead runs the `bash` command to get a terminal prompt

*NB* the `--rm` means that the container is deleted on exit, otherwise your disk could get clogged up with lots of exited containers

```
docker run -it --rm ubuntu
```


## Volumes in Docker

```
docker run ubuntu ls
```

## Running RStudio through Docker

## Use Case 1:- Distributing software for a training course

## Use Case 2:- Distributing supplementary data for a publication

## The elephant in the room

