FROM ubuntu:16.04

## Update apt cache
RUN apt-get update

## Install basic functions
RUN apt-get install sudo -y

## Install git
RUN apt-get install git -y

## Create user and group
ARG HOST_USER_UID=OVERRIDE_THIS
ARG HOST_USER_GID=OVERRIDE_THIS
RUN groupadd -g $HOST_USER_GID containergroup 
RUN useradd -m -l -u $HOST_USER_UID -g $HOST_USER_GID containeruser 

## Passwordless sudo for user    
RUN usermod -aG sudo containeruser
RUN echo "containeruser ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/containeruser && \
    chmod 0440 /etc/sudoers.d/containeruser

## Activate User    
USER containeruser

## Set working directory
WORKDIR /home/containeruser

## Workaround for vscode bug
ENV HOME=/home/containeruser

## Keep container running forever
CMD tail -f /dev/null
