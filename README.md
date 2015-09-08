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
(.local/share/cor-games). This should contain all your 3rd party maps, .nod files, bot files and other goodies in the `arena` subdirectory.
