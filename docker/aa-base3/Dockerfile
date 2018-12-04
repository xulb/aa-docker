# xulb/aa-base3
FROM ubuntu:16.04
MAINTAINER xulb <xulb.aa@gmail.com>
LABEL org.xulbia.docker="Xulb's AlienArena Trunk Build" version="3.0"
ENV DEBIAN_FRONTEND noninteractive
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
