FROM ubuntu:18.04 as build

RUN apt update && \
  apt -y upgrade && \
  apt -y install gcc make ca-certificates git

WORKDIR /home
