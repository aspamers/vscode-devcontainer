# VSCode docker development container

This repository provides a template of a docker development container configuration for vscode. You should be able to copy these files into your project and customise as needed.

This configuration is intended for use with Ubuntu, though in all likelihood would work elsewhere with little effort. 

## Basic usage

Install vscode and its remote development plugin along with docker and docker compose as suggested at the link:
https://code.visualstudio.com/docs/remote/containers

Clone this repository. After opening the project folder in vscode, open your command palette. Select the option `Remote-Containers: Open Folder In Container`. This will cause the docker image to build and the project to open inside the development container.

## Advanced usage

This configuration allows you to inject your current user id into the container at build time. Impersonating your host user is important if you would like to avoid permissions issues and do things like use your host user's git config.

On your host machine run the following command to get your user id:
```
$ id -u <username>
1002
```

On your host machine run the following command to get your user group id:
```
$ id -g <username>
1002
```

Set the user and group id you just obtained in the docker-compose.yml file
```
$ vi .devcontainer/docker-compose.yml
HOST_USER_UID: 1002
HOST_USER_GID: 1002
```

Rebuild your container using the command palette. You should be able to use git and other vscode features without issue.
