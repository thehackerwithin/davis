# Intro to Docker  
Container technology so easy it should be illegal not to use it. 

![][1]   
Speaker: [Karen Ng](http://karenyyng.github.io)

# Outline 
* Why Docker?
* What is Docker?
* Basic docker terminologies and commands
* Hands-on exercise: Using Docker to update theHackerWithin Davis chapter website 

# Why Docker?
![][2]

# Why Docker?
* Helps reproduce an exact software environment
* Good for:
	* software development / deployment
	* reproducible science!
	* teaching (and grading)

# What is Docker? 
Software container = Operating-System-level virtualization   
![][4]

# What is Docker? 
Fast startup time (~500 ms)    
![][4]

# What is Docker? 
One container for approximately one app   
![][4]

# Docker vs virtual machines (VM)
VM = hardware level virtualization
![][5]

# Docker vs virtiual machines (VM)
VM has more overhead   
![][5]



# Launch Docker quickstart terminal

# Basic Docker terminologies

# Dockerhub 
an [online registry](link) where you can pull and host publicly available Docker images
```
$ docker pull karenyng/hackerwithin_davis
```
searches Dockerhub for an image file

# Docker image 
![Fig. Docker infrastructure if host machine is Linux. (fig stolen from Docker)][6]

* static image of an OS along with the software
* can have parent / base image

# Container 
![Fig. Docker infrastructure if host machine is Linux. (fig stolen from Docker)][6]   
a running / stopped instance of an image  

# Dockerfile 
* a recipe for building a Docker image
* [an Dockerfile example](https://github.com/karenyyng/GalSim_dockerfile/blob/v1.3.0/Dockerfile) vs the [original installation guide](https://github.com/GalSim-developers/GalSim/blob/releases/1.3/INSTALL.md)


# Docker basic commands 
```
$ docker run <IMAGE_NAME> 
$ docker images 
$ docker ps 
```

# Pulling an image
```
$ docker pull <IMAGE_NAME>
```
where we used `<IMAGE_NAME> = karenyng/hackerwithin_dockerfile`      


# Hands-on session: building the image from a
[Dockerfile](https://github.com/karenyyng/hackerwithin_dockerfile/blob/master/Dockerfile)
```
$ git clone \
https://github.com/karenyyng/hackerwithin_dockerfile
$ cd hackerwithin_dockerfile
$ vim Dockerfile
```
[ref API](https://docs.docker.com/v1.8/reference/builder/)


# How did I build and debug the image? 
```
$ git clone \
https://github.com/thehackerwithin/davis
$ cd davis 
$ git checkout failed
$ docker build -t SillyDemoImageName .
```
where `-t` specifies the built image name.

# Debug problematic image 
```
$ docker run <CACHED IMAGE HASH> 
$ docker run -ti <CACHED IMAGE HASH> 
```

# Commit 
```
$ docker commit --help
```

# Login to DockerHub and push
```
$ docker login
```

# Or commit Dockerfile to GitHub for an automated build 
See [DockerHub](https://hub.docker.com/r/karenyng/galsim_dockerfile/)

# Check what images are locally available
```
$ docker images 
```

# Check what containers are running 
```
# only shows running containers 
$ docker ps     

# show all the containers  
$ docker ps -a  
```

# Running the HackerWithin site
```
$ cd <DIRECTORY OF HACKERWITHIN GIT REPO>
$ docker run -it \
-p 4000:4000 \ 
-v $(pwd):/root \
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
-v $(pwd):/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
* `docker run` runs a certain image, in this case `hackerwithin` which we have pulled previously

# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $(pwd):/root \
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
-v $(pwd):/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
* `-p HOST_PORT:CONTAINER_PORT` exposes the port 

# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $(pwd):/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
* `-v $(pwd):/root` tells Docker to mount our present working directory (pwd)
    to `/root` in the container

# What did we just do? 
```
$ docker run -it \
-p 4000:4000 \ 
-v $(pwd):/root \
karenyng/hackerwithin_dockerfile \
ruby -S jekyll serve \
--host=0.0.0.0 --watch --force_polling
```
Last two lines tells `Jekyll` to keep on monitoring for changes.


# Clearing up space 
```
$ docker stop CONTAINER_ID 
$ docker ps -a   # checks local containers 
$ docker rm CONTAINER_ID # remove container 
$ docker images  # checks local images
$ docker rmi IMAGE_NAME  # remove image 
```

# What is next? Use Docker for ...
* collaboration 
* running SaaS for a startup
* running a continuous integration server 
* running R Studio ([NERSC HPC version](http://rstudio.nersc.gov) / [Jupyter NERSC](http://ipython.nersc.gov) web client

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

* run and modify the `HackerWithin` page
* run [rOpenSci R studio web client](https://hub.docker.com/r/rocker/rstudio/) 
* run Jupyter [Docker-stack](https://github.com/jupyter/docker-stacks) for `Spark`/ `SparkR`/ `PySpark` / `Scipy` Jupyter notebook in Docker
* run [`Tensorflow`](https://www.tensorflow.org/versions/r0.7/get_started/os_setup.html#docker-installation)

# Building Dockerfiles / using Docker on the Cloud
difficulty: more involved

* write your own Dockerfile and build your own app
* use `Docker compose` to run the `Docker` 3rd birthday web app [tutorial](http://www.meetup.com/Docker-Galway/events/228871179/)
* setup the `HortonWorks Data Platform`
    [sandbox](https://hub.docker.com/r/torusware/hortondataplatform-examples/) for playing with `Hadoop` and `Spark` in Docker
* Challenge: write the Dockerfile(s) for Astrophysics codes, e.g.   
    * [Cosmosis](https://bitbucket.org/joezuntz/cosmosis/wiki/Home),
    * [Astrometry.net](http://astrometry.net/)


[1]: http://7030-presscdn-0-54.pagely.netdna-cdn.com/wp-content/uploads/2014/01/homepage-docker-logo.png 
[2]: http://cdn.meme.am/instances/500x/18961028.jpg
[3]: http://steinim.github.io/slides/devops-i-praksis/img/worked-fine-in-dev.jpg
[4]: img/docker_spring2016/docker_tech.png
[5]: img/docker_spring2016/docker_vs_vmware.jpg
[6]: img/docker_spring2016/terminology.png
[7]: img/docker_spring2016/docker_birthday.png
[8]: https://www.google.com/url?sa=i&rct=j&q=&esrc=s&source=images&cd=&cad=rja&uact=8&ved=0ahUKEwjIg72Z39zLAhWD6CYKHVoKCsYQjRwIBw&url=http%3A%2F%2Fwww.memegen.com%2Fmeme%2Fllhckr&psig=AFQjCNHs01o0ODuSEkY2794lcE1wqVeOyA&ust=1459026309354409
