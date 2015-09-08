Docker Tools for AA Server Management
=====================================

These are some tools for running [AlienArena](http://red.planetarena.org)
servers in [Docker](http://www.docker.com) containers in Linux.

# aamgr

Command-line tools to list running servers, list available server configs, 
fetch server logs, and start/kill new servers on your machine.

# Docker image builders

Dockerfiles for building a base server-only image on Ubuntu 14.04.

_aa-trunk_ : Creates the alienarena-ded server from AlienArena [SVN](http://svn.icculus.org/alienarena).

_aa-server_ : Creates an image based on _aa-trunk_, adding your game directory
(`.local/share/cor-games`). This should contain all your 3rd party maps, `.nod` files, bot files and other goodies in the `arena` subdirectory.

# Using Docker for running your servers

* First, [install Docker](https://docs.docker.com/installation/).

* Make sure the docker daemon is running:
```
$ ps -Af | grep docker
root       889     1  0 Aug29 ?        00:20:35 /usr/bin/docker daemon
```

* Use docker/aa-server/Dockerfile to build your local AA image:

  * Clone this repo into your home dir:
```
 $ cd
 $ git clone https://github.com/xulb/aa-docker.git
 $ cd aa-docker
```

  * Move into the docker/aaserver directory, and *copy* your local AA stuff 
into a new subdir called `codered` (copy is necessary; you can get rid of it
later):
```
 # assuming your local maps, etc. are in standard .local/share/cor-games
 $ cd docker/aa-server
 $ cp -R ~/.local/share/cor-games codered
```

  * Create the Docker image:
```
 $ sudo docker build -t aaserver .
```

  * Try starting a server in a docker container:
```
 $ sudo docker run -dt -p 27900:27900/udp -p 27909:27909/udp \
   --name myserver myconfig.cfg
```


