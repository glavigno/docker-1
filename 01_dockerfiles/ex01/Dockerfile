FROM debian

ENV TS3SERVER_LICENSE=accept

WORKDIR /opt/teamspeak

RUN apt-get update && apt-get -y upgrade && apt-get install -y wget bzip2

RUN wget http://dl.4players.de/ts/releases/3.6.1/teamspeak3-server_linux_amd64-3.6.1.tar.bz2
RUN	tar -jxvf teamspeak3-server_linux_amd64-3.6.1.tar.bz2

WORKDIR /opt/teamspeak/teamspeak3-server_linux_amd64/

EXPOSE 9987/udp 10011 30033

ENTRYPOINT ["sh", "ts3server_minimal_runscript.sh", "createinifile=1"]

# build the image from the dockerfile
# docker build -t <name> .

# run the image created with appropriate flags, especially ports here
# docker run -it --rm -p 9987:9987/udp -p 30033:30033 -p 10011:10011 <name>

# launch Teamspeak client installed via ths MSC
# connect with the address of the docker-machine
