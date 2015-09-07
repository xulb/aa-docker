# docker run -dt -p 27900:27900/udp -p 27909:27909/udp --name aa-server <config.cfg>
FROM aatrunk:latest
MAINTAINER xulb <xulb.aa@gmail.com>
LABEL org.xulbia.docker="Xulb's AlienArena Trunk Server" version="0.01"
EXPOSE 27900/udp 27901/udp 27902/udp 27903/udp 27904/udp 27905/udp
EXPOSE 27906/udp 27907/udp 27908/udp 27909/udp 27910/udp
RUN addgroup alien
RUN adduser alien alien
RUN mkdir -p /home/alien/local/share/cor-games
ADD codered /home/alien/local/share/cor-games
# workaround for issues with docker permissions
RUN chown -R alien:alien /home/alien ; \
    cp -Rp /home/alien/local /home/alien/.local ; \
    rm -rf /home/alien/local
USER alien
WORKDIR /home/alien/.local/share/cor-games
ENTRYPOINT ["alienarena-ded", "+set", "game", "arena", "+exec"]





