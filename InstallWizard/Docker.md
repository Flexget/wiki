---
title: Docker
description: 
published: true
date: 2022-10-11T18:37:12.536Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:08.245Z
---

# [Install Wizard](/InstallWizard) > Docker

## Install Docker

Follow the instructions for your operating system [here](https://docs.docker.com/engine/install/).

## Running a Docker FlexGet image

### Official Image
[ghcr.io/flexget/flexget](https://github.com/flexget/flexget/pkgs/container/flexget)

docker cli:
```
docker run -d \
  --name flexget \
  -v /host/config:/root/.flexget \ # required
  -e TZ=$TIMEZONE \ # optional: defaults to UTC
  -p 5050:5050 \ # optional: for webui
  ghcr.io/flexget/flexget \
  daemon start --autoreload-config
```
docker compose:
```
services:
  flexget:
    image: ghcr.io/flexget/flexget
    container_name: flexget
    commands:
      - daemon
      - start
      - --autoreload-config
    ports:
      - 5050:5050 # optional: for webui
    environment:
      - TZ=$TIMEZONE # optional: defaults to UTC
    volumes:
      - /host/config:/root/.flexget # required
      - /host/downloads:/downloads 
```
Replace bindmount host paths with the host directory path you would like to use for the config and download folders.
Add additional bindmounts as needed for downloads and other storage.

Replace `$TIMEZONE` with desired timezone. See list of valid timezones [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). Use the name in the tz database name column. Defaults to UTC if not specified.

Valid image tags:
 - latest (default) - latest tagged version release
 - develop - latest commit on develop branch
 - major.minor.patch version (e.g. ghcr.io/flexget/flexget:3.3.33)
 - major.minor version (e.g ghcr.io/flexget/flexget:3.3)
 - major version (e.g. ghcr.io/flexget/flexget:3)
 

### 3rd party images
  - [wiserain/flexget](https://hub.docker.com/r/wiserain/flexget)
  - [cpoppema/docker-flexget](https://hub.docker.com/r/cpoppema/docker-flexget)
  - [cptactionhank/flexget](https://hub.docker.com/r/cptactionhank/flexget)

### Build your own image

If you want to build your own, the Synology installation has a docker option with [instructions](/InstallWizard/SynologyNAS/Docker) (adjust to your OS as needed since some instructions are Synology specific such as the volume paths).
