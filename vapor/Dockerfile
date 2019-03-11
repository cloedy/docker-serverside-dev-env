FROM ubuntu:18.04

LABEL maintainer="Mars <11@boxue.io>"
LABEL description="Docker container for server side development."

# Vapor setup
RUN /bin/bash -c "$(wget -qO- https://apt.vapor.sh)"

# Install vapor and clean
RUN apt-get install swift vapor -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN vapor --help

