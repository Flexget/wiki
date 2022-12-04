---
title: Docker
description: 
published: true
date: 2022-10-26T01:32:34.924Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:08.245Z
---

# [Install Wizard](/InstallWizard) > Docker

## Install Docker

Follow the instructions for your operating system [here](https://docs.docker.com/engine/install/).

## Running a Docker FlexGet image

### Official Image
- [flexget/flexget](https://hub.docker.com/r/flexget/flexget)
- [ghcr.io/flexget/flexget](https://github.com/flexget/flexget/pkgs/container/flexget)

#### Based on python:3.10-alpine

This image includes `deluge-client`, `transmission-rpc` and `cloudscraper`.

If you need other pip or alpine packages, create a custom script to run as an entrypoint to install them before running flexget.

### Usage

docker cli:
```bash
docker run -d \
  --name flexget \
  -v /host/config:/config \        # required
  -e TZ=$TIMEZONE \                # optional: defaults to UTC
  -p 5050:5050 \                   # optional: for webui
  ghcr.io/flexget/flexget \
  daemon start --autoreload-config
```

docker compose:
```yaml
services:
  flexget:
    image: ghcr.io/flexget/flexget
    container_name: flexget
    command:
      - daemon
      - start
      - --autoreload-config         # optional
    ports:
      - 5050:5050                   # optional: for webui
    environment:
      - TZ=$TIMEZONE                # optional: defaults to UTC
    volumes:
      - /host/config:/config        # required
      - /host/downloads:/downloads 
```
Replace bindmount host paths with the host directory path you would like to use for the config and download folders.
Add additional bindmounts as needed for downloads and other storage.

Replace `$TIMEZONE` with desired timezone. See list of valid timezones [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). Use the name in the tz database name column. Defaults to UTC if not specified.

Valid image tags:
 - latest (default) - latest tagged version release
 - develop - latest commit on develop branch
 - major.minor.patch version (e.g. ghcr.io/flexget/flexget:3.4.0)
 - major.minor version (e.g ghcr.io/flexget/flexget:3.4)
 - major version (e.g. ghcr.io/flexget/flexget:3)

#### Custom entrypoint

`entrypoint.sh`
```
#!/bin/sh

apk add --no-cache $PKG1

pip install $PKG2

flexget daemon start --autoreload-config
```

Make sure it's executeable: `chmod +x entrypoint.sh`

docker cli:
`docker run ... -v /host/config:/config --entrypoint /config/entrypoint.sh ...`

docker compose:
```yaml
services:
  flexget:
    ...
    entrypoint: /config/entrypoint.sh
    ...
```


### 3rd party images
  - [wiserain/flexget](https://hub.docker.com/r/wiserain/flexget) / [ghcr.io/wiserain/flexget](https://github.com/wiserain/docker-flexget/pkgs/container/flexget)
  - [ksurl/flexget](https://hub.docker.com/r/ksurl/flexget) / [ghcr.io/ksurl/flexget](https://github.com/ksurl/docker-flexget/pkgs/container/flexget)
  - [cptactionhank/flexget](https://hub.docker.com/r/cptactionhank/flexget)
  - [cpoppema/docker-flexget](https://hub.docker.com/r/cpoppema/docker-flexget)
  
### Build your own image

If you want to build your own, the Synology installation has a docker option with [instructions](/InstallWizard/SynologyNAS/Docker) (adjust to your OS as needed since some instructions are Synology specific such as the volume paths).
