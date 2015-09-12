Docker Tools for AA Server Management
=====================================

These are some tools for running [AlienArena](http://red.planetarena.org)
servers in [Docker](http://www.docker.com) containers in Linux.

## Docker image builders

Dockerfiles for building a base server-only image on Ubuntu 14.04.

_aa-trunk_ : Creates the alienarena-ded server from AlienArena [SVN](http://svn.icculus.org/alienarena).

This image is available on [Docker Hub](https://hub.docker.com/r/xulb/aa-trunk).

_aa-server_ : Creates an image based on _aa-trunk_, adding your game directory
(`.local/share/cor-games`). This should contain all your 3rd party maps, `.nod` files, bot files and other goodies in the `arena` subdirectory. 
The Dockerfile pulls the `xulb/aa-trunk` down from Docker Hub; you don't 
have to create it yourself.

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

  * Move into the docker/aa-server directory, and *copy* your local AA stuff 
into a new subdir called `codered` (copy is necessary; using a link won't work)
```
 # assuming your local maps, etc. are in standard .local/share/cor-games
 $ cd docker/aa-server
 $ cp -R ~/.local/share/cor-games codered
```

  * Create the Docker image:

```
 $ sudo docker build -t aa-server .
```

  * Try starting a server in a docker container:

```
 $ sudo docker run -dt -p 27900:27900/udp -p 27909:27909/udp \
   --name myserver aa-server myconfig.cfg
```

_Explanation_: This command runs a container called "myserver" using
image `aa-server` that starts alienarena-ded execing myconfig.cfg. The
host machine port 27909 is mapped the container port 27909 to allow
players in. The port in the docker command must match the port set in
the config file (the `set port [nnnnn]` line). Port 27900 is also
exposed to the world, so that the server can communicate with the
master server and show up on the [server
browser](http://hal.nanoid.net/arena/tools/browser/).

## aamgr

Command-line tool to list running servers, list available server
configs, fetch server logs, and start/kill new servers on your
machine.

* `aamgr --start yourconfig.cfg` will search the config for the
  correct port and start the machine on that port

* `aamgr --list-configs` lists the config files that are present in
  the container

### aamgr Installation

`aamgr` is a single bash shell script. Move it to a location on your
PATH, e.g., `/usr/local/bin`. If it doesn't run, do

```
$ chmod a+x aamgr
```

on it.

