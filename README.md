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
    + potentially a good way for beginners to learn command-line tools?
- Really useful for testing software
- Clear benefits for working reproducibly
    + instead of just distributing the code used for a paper, you can effectively share the computer you did the analysis on
- For those of you that have used Virtual Machines, it is a similar concept
- However, they are more lightweight and easier to distribute
- Images are combined in a layered system

## Installing Docker

### Mac

- [Mac OSX - 10.10.3 or newer](https://www.docker.com/docker-mac)
- [Older Macs](https://download.docker.com/mac/stable/DockerToolbox.pkg)

### Windows

(may require some messing around with virtualisation or Hyper-V)

- [Windows 10](https://www.docker.com/docker-windows)
- [Older Windows](https://download.docker.com/win/stable/DockerToolbox.exe)


Once you have installed Docker using the insructions above, you can open a terminal (Mac) or command prompt (Windows) and run the following to download an image for the Ubuntu operating system;

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

You'll notice that when you launch a container, you don't automatically have access to the files on your OS. In Docker, we can mount *volumes* using the -v argument to make files accessible e.g. `-v /PATH/TO/YOUR/data:/data` inside the container.

```
docker run -it --rm -v 
```

## Running R (and RStudio) through Docker

The latest version of R and R devel are provided by the rocker project https://github.com/rocker-org/rocker

```
docker run --rm -it r-base R
```

- run the `r-base` docker image
- run interatively (`-it`)
- run the `R` executable

For latest developmental version of R:-

```
docker run --rm -it r-devel R
```

Can also [get previous versions of R](https://hub.docker.com/r/library/r-base/tags/)

- good if you need to re-run code that was written on a previous R version
- good if you need to test code on latest version of R


RStudio is also supported. See https://github.com/rocker-org/rocker/wiki/Using-the-RStudio-image

- this time we do something slightly different

```
docker run -p 8787:8787 rocker/rstudio
```
- the `-p` argument opens a port in the docker container
- open a web browser and enter the address `http://localhost:8787`
- username `rstudio` password `rstudio`
- you have a version of RStudio working in your web browser!

You can install whatever R packages you need in this container and analyse your data (provided you mount a volume with `-v`. 

- once a docker has quit, it can be restarted with `docker start` and `docker attach`

```
docker start <name-of-container-that-just-exited>
docker attach <name-of-container-that-just-exited>
```

You can then build a new image 

```
docker commit <name-of-container-that-just-exited> <new image>
```

## The `Dockerfile`

The `Dockerfile` is the recommended way of composing your own image

- stating the starting point for your image (e.g. Ubuntu)
- listing the commands to install your libraries etc

```
FROM bioconductor/release_base2
MAINTAINER Mark Dunning<mark.dunning@cruk.cam.ac.uk>

## Install packages from Ubuntu repositories
RUN rm -rf /var/lib/apt/lists/
RUN apt-get update 
RUN apt-get install --fix-missing -y git samtools fastx-toolkit python-dev cmake bwa picard-tools bzip2 tabix bedtools build-essential git-core cmake zlib1g-dev libncurses-dev libbz2-dev liblzma-dev man
 
## Download and install fastqc

WORKDIR /tmp
RUN wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.3.zip -P /tmp
RUN unzip fastqc_v0.11.3.zip
RUN sudo chmod 755 FastQC/fastqc
RUN ln -s $(pwd)/FastQC/fastqc /usr/bin/fastqc


## Make directory structure
RUN mkdir -p /home/participant/Course_Materials/Day1
RUN mkdir -p /home/participant/Course_Materials/Day2
RUN mkdir -p /home/participant/Course_Materials/Day3
RUN mkdir -p /home/participant/Course_Materials/Day4

## Install required R packages
COPY installBioCPkgs.R /home/participant/Course_Materials/
RUN R -f /home/participant/Course_Materials/installBioCPkgs.R


## Populate directories for each day
COPY Day1/* /home/participant/Course_Materials/Day1/
COPY Day2/* /home/participant/Course_Materials/Day2/
COPY Day3/* /home/participant/Course_Materials/Day3/
COPY Day4/* /home/participant/Course_Materials/Day4/

## Create data, reference data directories
## These will need to be mounted with local directories containing the data when running the container
## scripts are included to download the relevant files

VOLUME /data/
VOLUME /reference_data/

WORKDIR /home/participant/Course_Materials/


```


## Use Case 1:- Distributing software for a training course

```
docker run --rm -p 8787:8787 markdunning/cancer-genome-toolkit
```



## Use Case 2:- Distributing supplementary data for a publication

Stephen Eglen of University of Cambridge made the data and code for his paper available on github :+1:

## The elephant in the room

Docker should be a great solution for shared systems (e.g. HPC) where typically everyone installs their own versions of R. However, when you run a Docker container you have super-user access rights inside that container. Unix admin people that manage HPC systems don't like this.

There is an alternative....

Singularity

![](http://singularity.lbl.gov/images/logo/logo.svg)
