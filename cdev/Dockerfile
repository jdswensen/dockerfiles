# C development tools in a container
#
# docker run \
#   -it \
#   -v $HOME:/home/docker \
#   --name cdev \
#   jdswensen/cdev
#

FROM debian:buster
LABEL maintainer "Jake Swensen <jake@swensen.io>"

# Tell debconf to run in non-interactive mode
ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y    \
    cmake                                   \
    gcc                                     \
    gdb                                     \
    git                                     \
    make                                    \
    python3                                 \
    python3-pip                             \
    shellcheck                              \
    uncrustify                              \
    valgrind                                \
    vim

# Install python packages
RUN pip3 install pre-commit

# Create user
ENV HOME /home/docker
RUN useradd --create-home --home-dir $HOME docker
USER docker

# Change home dir permissions
RUN chown -R docker:docker $HOME

RUN apt-get update && apt-get install -y    \
    --no-install-recommends                 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR $HOME
