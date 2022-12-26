---
title: Docker
description: 
published: true
date: 2022-11-22T17:39:11.616Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:24:03.756Z
---

# [Install Wizard](/InstallWizard) > [SynologyNAS](/InstallWizard/SynologyNAS) > Docker

> Since this guide, there is official docker image which might be much better starting point. This guide should be re-evaluated.
>
> Updates are appreciated
{.is-warning}

## Install Docker

Go to the DSM Package Center and install the Docker package. Run it.

## Create a user

Use the DSM Control Panel to create a new user called `docker`. Make a note of the user's UID:

```sh
$ id -u docker
1234
```

The rest of this page will assume a UID of 1234.

## Build a FlexGet image

Create a new directory on your NAS (doesn't really matter where) and copy these two files there. You'll use them to create your image. 

`Dockerfile`
```
FROM     python:alpine

ARG      DOCKER_UID

# Create a user to run the application
RUN      adduser -D -u ${DOCKER_UID} flexget
WORKDIR  /home/flexget

# Data and config volumes
VOLUME   /home/flexget/.flexget
VOLUME   /home/flexget/torrents

# Install build dependencies and FlexGet
RUN      apk add --no-cache --virtual  .build-deps gcc g++ musl-dev linux-headers && \
         pip3 install -U pip && pip3 install flexget && \
         apk del .build-deps gcc musl-dev

# Add start script
COPY     start.sh /home/flexget/
RUN      chmod +x ./start.sh

USER     flexget
CMD      ["./start.sh"]
```

`start.sh`
```
#!/bin/sh
if [ -f ~/.flexget/.config-lock ]; then
    rm ~/.flexget/.config-lock
fi
flexget daemon start
```

Make a note of the current version of [FlexGet on PyPI](https://pypi.python.org/pypi/FlexGet) (we'll use this to label the image we create). At time of writing, this is 3.1.62.

Navigate into the directory containing the files above. To build your image, run the following command (don't forget to substitute in your `docker` user's UID):

```sh
docker build --build-arg DOCKER_UID=1234 -t flexget:3.1.62 .
```

Make sure that it worked by running `docker images`. You should see something like this:

```sh
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
flexget             3.1.62              ff4e5f3f1239        20 hours ago        160.4 MB
python              alpine              2070486450e1        2 weeks ago         88.63 MB
```

## Build a Transmission image (optional)

FlexGet and Transmission make a great pair; FlexGet decides what .torrents to grab (say, from an RSS feed) and Transmission handles downloading the actual content. Docker makes it really easy to run Transmission as well.

As above, copy the file below into its own directory (not the one you used for FlexGet). Note, the download folder in the container starts with a capital D!

`Dockerfile`
```
FROM        alpine

ARG         DOCKER_UID

# Create a user to run the application
RUN         adduser -D -u ${DOCKER_UID} transmission
WORKDIR     /home/transmission

# Data and config volumes
VOLUME      /home/transmission/.config
VOLUME      /home/transmission/Downloads
VOLUME      /home/transmission/incomplete
VOLUME      /home/transmission/watch

# Install Transmission
RUN         apk update && apk add --no-cache transmission-daemon

EXPOSE      9091

USER        transmission
ENTRYPOINT  ["transmission-daemon", "--foreground", "--log-info"]
```

Navigate into said directory and run this command to build an image:

```sh
docker build --build-arg DOCKER_UID=1234 -t transmission:2.94-r1 .
```

And again, check that it worked:

```sh
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
transmission        2.94-r1             15577a02872f        20 hours ago        8.157 MB
flexget             3.1.62              ff4e5f3f1239        20 hours ago        160.4 MB
python              3.6-alpine          2070486450e1        2 weeks ago         88.63 MB
alpine              latest              76da55c8019d        2 weeks ago         3.962 MB
```

## Launch the container(s)

The provided Dockerfiles use the `VOLUME` directive to create points at which we can mount the host's filesystem into that of our containers. This is very handy:

* It lets us keep config files on the host, which makes them much easier to edit.
* It lets data created by the containers outlive them. For the purposes of this guide, we want to store our finished torrents in a Shared Folder. We also want our torrent data and metadata to persist even if we have to delete or replace the Transmission container for some reason (e.g. updates).
* It's a simple way to let two different containers share access to a single directory. FlexGet can download .torrent files directly into Transmission's watch directory.

The `docker run` commands you need to launch each container are below. Note that once you've launched a container, `docker stop` and `docker start` are used to control its state.

### Transmission

Create the necessary directories on your NAS:

```sh
mkdir -p \
  /volume1/docker/transmission/config \
  /volume1/docker/transmission/incomplete \
  /volume1/docker/transmission/watch
```

The `docker run` command below maps Transmission's config, incomplete, and watch directories into locations under `/volume1/docker/transmission` on the host. It also maps the downloads directory to a Shared Folder cat `/volume1/Media/Downloads`.

Note that you'll need to set the correct in-container locations for each of these directories in Transmission's [`settings.json`](https://github.com/transmission/transmission/wiki/Editing-Configuration-Files) file at `/volume1/docker/transmission/config/transmission-daemon/settings.json`. This file gets created automatically the first time the container starts, so you can just start it once to generate a default config.

Use this command to launch the container:

```sh
docker run -d \
  --env "TZ=America/Los_Angeles" \
  --name transmission \
  --net host \
  --publish 9091:9091 \
  --restart always \
  --volume /volume1/docker/transmission/config:/home/transmission/.config \
  --volume /volume1/docker/transmission/incomplete:/home/transmission/incomplete \
  --volume /volume1/docker/transmission/watch:/home/transmission/watch \
  --volume /volume1/Media/Downloads:/home/transmission/Downloads \
  transmission:latest
```

Stop it with `docker stop transmission` before editing the settings file.

Choose a password you'll use to access the Transmission web UI and then change the following settings:

```json
{
    "blocklist-enabled": true,
    "blocklist-url": "http://john.bitsurge.net/public/biglist.p2p.gz",
    "download-dir": "/home/transmission/Downloads",
    "incomplete-dir": "/home/transmission/incomplete",
    "incomplete-dir-enabled": true,
    "rpc-authentication-required": true,
    "rpc-bind-address": "0.0.0.0",
    "rpc-enabled": true,
    "rpc-password": "password",
    "rpc-port": 9091,
    "rpc-url": "/transmission/",
    "rpc-username": "you",
    "rpc-whitelist": "127.0.0.1",
    "rpc-whitelist-enabled": false,
    "start-added-torrents": true,
    "trash-original-torrent-files": true,
    "watch-dir": "/home/transmission/watch",
    "watch-dir-enabled": true
}
```

Save your changes and start Transmission back up with `docker start transmission`.

The web UI will be available at `http://your-nas-host:9091/transmission/web/` (don't omit the trailing slash).

### FlexGet

Create the necessary directories:

```sh
mkdir -p /volume1/docker/flexget
```

Start FlexGet:

```sh
docker run -d \
  --env "TZ=America/Los_Angeles" \
  --name flexget \
  --restart always \
  --volume /volume1/docker/flexget:/home/flexget/.flexget \
  --volume /volume1/docker/transmission/watch:/home/flexget/torrents \
  flexget:3.1.62
```

With these volume settings, FlexGet will download .torrent files directly into Transmission's watch directory.

Your config file lives at `/volume1/docker/flexget/config.yml`. It's not necessary to stop/start the whole container when you make changes – instead, use the following command:

```sh
docker exec flexget flexget daemon reload-config
```

## That's all folks

I hope this guide was helpful!