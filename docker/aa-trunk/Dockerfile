FROM ubuntu:14.04
MAINTAINER xulb <xulb.aa@gmail.com>
LABEL org.xulbia.docker="Xulb's AlienArena Trunk Build" version="0.01"
ENV AATrunk=svn://svn.icculus.org/alienarena/trunk
RUN apt-get update
RUN apt-get install -y \
 subversion \
 curl \
 gcc \
 pkg-config \
 make
RUN svn checkout $AATrunk aa-trunk
WORKDIR aa-trunk
RUN ./configure --disable-client
RUN make install
