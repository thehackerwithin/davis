# Intro to Docker  
Container technology so easy it should be illegal not to use it. 

![][1]   
Speaker: [Karen Ng](http://karenyyng.github.io)

# Outline 
* Why Docker?
* What is Docker?
* Basic docker terminologies and commands
* Hands-on exercise: 
	* build a Docker image
	* run Docker container to update theHackerWithin Davis chapter website 
* Markdown outline of slides available
    [here](https://github.com/karenyyng/davis/blob/gh-pages/meeting-materials/2016-04-14/docker_slides.md)

# Why Docker?
![][2]

# Why Docker?
* Helps reproduce an exact software environment
* Good for:
	* software development / deployment
	* reproducible science!
	* teaching (and grading)

# What is Docker? 
> An open-source technology that allows you to package an app with all its dependencies into a
standardized unit for software development.    
-Docker website

![][4]
<aside class='notes' data-markdown>
for example in this diagram, each of these colored boxes shows you a container,
containing an app.
And the bottom box shows your server / host machine  
on top you have whatever operating system that is running
    on the host machine, in this case this diagram assumes the OS on the host
    machine is Linux.
Running on top of the host OS is the docker engine.
Each of Docker container that runs on top of the docker engine captures 
all the software dependencies, 
including the runtime, system tools, system libraries and other dependencies.
Since docker assumes that each app would run inside a certain
flavor of Linux, docker allows the system services in the container to bind
directly to the kernel of the host OS without introducing extra overhead.
And I will show you how this differs if the host OS is not Linux.
</aside>


# What is Docker? 
* One container for running approximately one app     

![][4]
<aside class='notes' data-markdown>
It is not a strict rule to only have one piece of software in a container. 
Use any logical unit to group several pieces that have dependencies. 
But each container is isolated by default. 
You can tweak the settings so each container is secure from outside attacks. 
</aside>

#  Virtual machines (left) vs Docker (right)
![][5]
Software container = operating-system-level virtualization   
VM = hardware level virtualization

<aside class='notes' data-markdown>
On the left, for there to be isolation of different apps, you need several
virtual machines, each running an additional OS.
On the right, for Docker, all the different containers can share the same
operating system kernel. 
This means that Docker is more efficient with its resources. 
</aside>

#  Virtual machines (left) vs Docker (right)
VM has more overhead   
![][5]

# What is Docker? 
* Containers start up faster (~500 ms)    

![][5]
<aside class='notes' data-markdown>
This also means that once the docker daemon is running each app can be started very quickly.
Later on we will also see that each container can contain some runtime 
instructions to specify how each app should be run.
</aside>


# Launch Docker quickstart terminal    
(Mac and Windows User)
![][8]

Linux users execute:
```
$ sudo docker -d & 
```

# Basic Docker terminologies

# Dockerhub 
an [online registry](https://hub.docker.com/) where you can pull and host publicly available Docker images
```
$ docker pull karenyng/hackerwithin_dockerfile
```
searches Dockerhub for an image file

# Docker image 
![Fig. Docker infrastructure if host machine is Linux. (fig stolen from Docker)][6]

* static image that packages Linux system runtime / library files along with the software
* can have parent / base image
* immutable

<aside class='notes' data-markdown>
Docker 's ability of being able to build on top of a base image 
makes it faster to build apps on top of the same image
vs if you build separate amazon machine images. 
There are different pros and cons.
</aside>
 

# Container 
![Fig. Docker infrastructure if host machine is Linux. (fig stolen from Docker)][6]   
a running / stopped instance of an image  

# Dockerfile 
* a recipe for building a Docker image
* can contain runtime configurations
* [a Dockerfile example](https://github.com/karenyyng/GalSim_dockerfile/blob/v1.3.0/Dockerfile) vs the [original installation guide](https://github.com/GalSim-developers/GalSim/blob/releases/1.3/INSTALL.md)


# Hands-on session: 
running some Docker basic commands 
```
$ docker run <IMAGE_NAME> 
$ docker images 
$ docker ps 
```

# (Some prep for later) Pulling an image
```
$ docker pull <IMAGE_NAME>
```
where we used `<IMAGE_NAME> = karenyng/hackerwithin_dockerfile`      


# Ex1: Building the image from a [Dockerfile](https://github.com/karenyyng/hackerwithin_dockerfile/blob/master/Dockerfile)
```
$ git clone \
https://github.com/karenyyng/hackerwithin_dockerfile
$ cd hackerwithin_dockerfile
$ vim Dockerfile
```
[Dockerfile ref API](https://docs.docker.com/v1.8/reference/builder/)


# How did I build and debug the image? 
``` 
$ git fetch origin  # fetch all remote branches
$ git checkout -b failed origin/failed
$ docker build -t karenyng/silly .
```
where `-t` tags the image with `REPO_NAME/IMAGE_NAME`.

# Debug problematic image 
Get the CACHED IMAGE HASH from printed message.
```
$ docker run -ti <CACHED IMAGE HASH> 
```

# Build image then check what images are locally available
```
$ docker build -t MY_DOCKERHUB_REPONAME/silly .
$ docker images 
```
`-t` tags the `REPO/IMAGE_NAME`

# Login to DockerHub and push
```
$ docker login  
$ docker push MY_DOCKERHUB_REPONAME/silly
```

# Or commit Dockerfile to GitHub for an automated build 
See [DockerHub](https://hub.docker.com/r/karenyng/galsim_dockerfile/)


# Check what containers are running 
```
# only shows running containers 
$ docker ps     

# shows all the containers  
$ docker ps -a  
```

# Committing the container as an image  
```
$ docker commit --help
$ docker commit CONTAINER_ID DOCKERHUB_REPO/IMAGE_NAME:TAG
```

# Ex2: Running the HackerWithin site
```
$ git clone \
https://github.com/thehackerwithin/davis
$ cd davis 
```
* keep HackerWithin website files (`html` / markdown) outside container
* built all software dependencies (`Jekyll`, `Ruby`) inside container

# Running the HackerWithin site
```
$ docker run -it \
-p 4000:4000 \ 
-v $PATH_TO_HACKERWITHIN_DAVIS_DIR:/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
Now it is up and running!

# Check the IP address of your Docker machine
```
$ docker-machine ip 
192.168.99.100  # for Mac and Windows 
127.0.0.1       # for Linux
```
Now point your browser to `DOCKER_IP:4000`


# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $PATH_TO_HACKERWITHIN_DAVIS_DIR:/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
* `docker run` runs a certain image, in this case `karenyng/hackerwithin_dockerfile` which we have pulled previously

# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $PATH_TO_HACKERWITHIN_DAVIS_DIR:/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
* `-i` means run iteractively, asking the container to read from the host's `STDIN`
* `-t` asks container to bind to a pseudo-terminal

# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $PATH_TO_HACKERWITHIN_DAVIS_DIR:/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
* `-p HOST_PORT:CONTAINER_PORT` exposes the port 

# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $PATH_TO_HACKERWITHIN_DAVIS_DIR:/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
`-v $PATH_TO_HACKERWITHIN_DAVIS_DIR:/root` tells Docker to mount the
    directory of the Hackerwithin Davis repo to `/root` in the container

<aside class='notes' data-markdown>
* For Mac users, only directories under `/Users/` can only be mounted 
* special restrictions apply for Windows as well 
</aside>

# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $PATH_TO_HACKERWITHIN_DAVIS_DIR:/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
Last two lines tell `Jekyll` to keep on monitoring for changes.


# Clearing up space 
```
$ docker stop CONTAINER_ID 
$ docker ps -a   # checks local containers 
$ docker rm CONTAINER_ID # removes container 
$ docker images  # checks local images
$ docker rmi IMAGE_NAME  # removes image 
```

# What is next? Use Docker for ...
![][9]

* collaboration 
* running SaaS for a startup
* running a continuous integration service
* running R Studio ([NERSC HPC version](http://rstudio.nersc.gov)) or [Jupyter](http://ipython.nersc.gov) web client for remote machines

# Learning resources
* [Docker tutorial](https://github.com/docker/docker-birthday-3)
* [Docker online webminars](https://training.docker.com/self-paced-training)
* San Francisco [Docker meetups](http://www.meetup.com/Docker-meetups/)
* [Docker best practises](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
* How to use [Jekyll](http://salizzar.net/2014/11/06/creating-a-github-jekyll-blog-using-docker/) from Docker

# Thanks for listening!
![][7]
Questions?


# Hands-on exercises for those who want to run docker images
difficulty: easy

* run and modify the `HackerWithin`[page](https://github.com/thehackerwithin/davis)
* run [rOpenSci R studio web client](https://hub.docker.com/r/rocker/rstudio/) 
* run Jupyter [Docker-stack](https://github.com/jupyter/docker-stacks) for `Spark`/ `SparkR`/ `PySpark` / `Scipy` Jupyter notebook in Docker
* run [`Tensorflow`](https://www.tensorflow.org/versions/r0.7/get_started/os_setup.html#docker-installation)

# Building Dockerfiles / using Docker on the Cloud
difficulty: more involved

* write your own Dockerfile and build your own app
* use `Docker compose` to run the `Docker` 3rd birthday web app [tutorial](https://github.com/docker/docker-birthday-3)
* setup the `HortonWorks Data Platform`
    [sandbox](https://hub.docker.com/r/torusware/hortondataplatform-examples/) for playing with `Hadoop` and `Spark` in Docker
* challenge: write the Dockerfile(s) for Astrophysics codes, e.g.   
    * [Cosmosis](https://bitbucket.org/joezuntz/cosmosis/wiki/Home),
    * [Astrometry.net](http://astrometry.net/)

# Incomplete collection of useful commands
Restart stopped container
```
$ docker start CONTAINER_ID 
$ docker attach CONTAINER_ID
``````

# Incomplete collection of useful commands
If your container is running in background
and you want to use the command prompt inside the container
```
$ docker exec -it $(docker ps -q) bash
```


[1]: img/docker_spring2016/homepage-docker-logo.png 
[2]: img/docker_spring2016/18961028.jpg
[3]: img/docker_spring2016/worked-fine-in-dev.jpg
[4]: img/docker_spring2016/docker_tech.png
[5]: img/docker_spring2016/docker_vs_vmware.png
[6]: img/docker_spring2016/terminology.png
[7]: img/docker_spring2016/docker_birthday.png
[8]: img/docker_spring2016//applications_folder.png
[9]: img/docker_spring2016/Screen+Shot+2014-06-13+at+8.34.10+pm.png
