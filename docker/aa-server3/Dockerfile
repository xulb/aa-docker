# docker run -v /home/alien/.local/share/cor-games:/home/alien/.local/share/cor-games -dt -p 27900:27900/udp -p 27909:27909/udp --name aa-server aa-server3 <config.cfg>
FROM xulb/aa-base3:latest
MAINTAINER xulb <xulb.aa@gmail.com>
LABEL org.xulbia.docker="Xulb's AlienArena Trunk Server" version="3.0"
ENV COR_GAMES=.local/share/cor-games
ARG ALIEN_UID
EXPOSE 27900/udp 27901/udp 27902/udp 27903/udp 27904/udp 27905/udp
EXPOSE 27906/udp 27907/udp 27908/udp 27909/udp 27910/udp
# uid same as uid of host user (alien)
RUN useradd alien --uid $ALIEN_UID
RUN mkdir -p /home/alien/local/share/cor-games/arena
RUN chown -R alien:alien /home/alien ; \
    cp -Rp /home/alien/local /home/alien/.local ; \
    rm -rf /home/alien/local
WORKDIR /home/alien
ADD arena ./.local/share/cor-games/arena
RUN chown -R alien:alien ./.local/share/cor-games
USER alien
ENTRYPOINT ["alienarena-ded", "+set", "game", "arena", "+exec"]





