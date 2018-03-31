# Arduino IDE in a container
#   NOTE: You will need to run the following from the host machine:
#           `sudo usermod -a -G dialout $USER && sudo chmod a+rw /dev/ttyACM0`
#
# docker run -d \
#    -v /tmp/.X11-unix:/tmp/.X11-unix \
#    -v $HOME:/home/user \
#    -e DISPLAY=unix$DISPLAY \
#    --device=/dev/ttyACM0 \
#    --name arduino \
#    jdswensen/arduino
#

FROM debian:buster
LABEL maintainer "Jake Swensen <jake@swensen.io>"

# Tell debconf to run in non-interactive mode
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
	openjdk-8-jre \
	wget \
	xz-utils \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV ARDUINO_IDE_VERSION 1.8.5
RUN wget -q -O- https://downloads.arduino.cc/arduino-${ARDUINO_IDE_VERSION}-linux64.tar.xz | tar xJC /usr/share
RUN ln -s /usr/share/arduino-${ARDUINO_IDE_VERSION} /usr/share/arduino

ENV HOME /home/user
RUN useradd --create-home --home-dir $HOME user \
	&& chown -R user:user $HOME

COPY start.sh /usr/local/bin/start.sh

WORKDIR $HOME

CMD [ "start.sh" ]
