# [Install Wizard](/InstallWizard) > [SynologyNAS](/InstallWizard/SynologyNAS) > Docker

## Install Docker

Go to the DSM Package Center and install the Docker package. Run it.

## Create a user

Use the DSM Control Panel to create a new user called `docker`. Make a note of the user's UID (the rest of this page will assume a UID of 1234).

## Build a FlexGet image

Copy these two files to the same directory your NAS. You'll use them to create your image.

`Dockerfile`
```
FROM     python:3.5-alpine

ARG      DOCKER_UID

# Create a user to run the application
RUN      adduser -D -u ${DOCKER_UID} flexget
WORKDIR  /home/flexget

# Data and config volumes
VOLUME   /home/flexget/.flexget
VOLUME   /home/flexget/torrents

# Install FlexGet
RUN      pip3 install -U pip && pip3 install flexget

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

Make a note of the current version of [FlexGet on PyPI](https://pypi.python.org/pypi/FlexGet) (we'll use this to label the image we create). At time of writing, this is 2.10.95.

Navigate into the directory containing the files above. To build your image, run the following command (don't forget to substitute in your `docker` user's UID):

```sh
docker build --build-arg DOCKER_UID=1234 -t flexget:2.10.95 .
```

Make sure that it worked by running `docker images`. You should see something like this:

```sh
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
flexget             2.10.95             ff4e5f3f1239        20 hours ago        160.4 MB
python              3.5-alpine          2070486450e1        2 weeks ago         88.63 MB
```

## Build a Transmission image (optional)

FlexGet and Transmission make a great pair; FlexGet decides what .torrents to grab (say, from an RSS feed) and Transmission handles downloading the actual content. Docker makes it really easy to run Transmission as well.

As above, copy the file below into its own directory (not the one you used for FlexGet).

`Dockerfile`
```
FROM        alpine

ARG         DOCKER_UID

# Create a user to run the application
RUN         adduser -D -u ${DOCKER_UID} transmission
WORKDIR     /home/transmission

# Data and config volumes
VOLUME      /home/transmission/.config
VOLUME      /home/transmission/downloads
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
docker build --build-arg DOCKER_UID=1234 -t transmission:2.92-r5 .
```

And again, check that it worked:

```sh
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
transmission        2.92-r5             15577a02872f        20 hours ago        8.157 MB
flexget             2.10.95             ff4e5f3f1239        20 hours ago        160.4 MB
python              3.5-alpine          2070486450e1        2 weeks ago         88.63 MB
alpine              latest              76da55c8019d        2 weeks ago         3.962 MB
```

## Launch the container(s)

The provided Dockerfiles use the `VOLUME` directive to create points at which we can mount the host's filesystem into that of our containers. This is very handy for config files, which are much easier to edit if they live on the host.

It's also a simple way to give separate containers access to a shared directory. We can use this to have FlexGet download .torrent files directly into Transmission's watch directory.

### Create directories

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
  --volume /volume1/Media/Downloads:/home/transmission/downloads \
  transmission:latest
```

```sh
docker run -d \
  --env "TZ=America/Los_Angeles" \
  --name flexget \
  --restart always \
  --volume /volume1/docker/flexget:/home/flexget/.flexget \
  --volume /volume1/docker/transmission/watch:/home/flexget/torrents \
  flexget:2.10.95
```