# iobio.local
IOBIO backend stack

This repository contains scripts and config files for locally deploy IOBIO backend on any docker-enabled servers

# Prerequisites
  * Docker 1.7.1 or newer  [install doc](https://docs.docker.com/engine/installation/linux/)
  * docker-compose 1.4.2 or newer [install doc](https://docs.docker.com/compose/install/)
  * 60G free disk space

# Getting Started
To get started, you need to have a hostname assigned to your server so that
both the server and the clients can resolve to the same ip address. This is
because iobio applications make websocket connections to the underlying
services running on the server, and the services themselves also make
connections to other services. Hostnames such as '*localhost*' (or loopback IP
*127.0.0.1*) has different meanings between the client, the server itself, and
the different service containers, making it unsuitable even for testing
purpose. The FQDN of a server managed by either internal or external DNS works
the best. Otherwise, you may have to come up with a name, and manually mess
with `/etc/hosts` on both the server and the clients.

## Quick-Start
```bash
git clone --recursive https://github.com/yiq/iobio.local
cd iobio.local
./fetch-data.sh             # this will take a while.  (1)
./fetch-images.sh           # optional (2)
sudo docker-compose up -d
```
Once everything starts up, open a browser on your client machine, and go to `http://<public-hostname>/`

## Explaination
### Line (1)
Some of the backend services require data files such as the human reference. This script will download all the required data volumes and uncompress them into $REPO/data-vol. These data volumes will then be mapped into the docker containers.

### Line (2)
Download all the needed docker images manually instead of let docker-compose handle it. This can also be used to update images when newer versions are released in the future.
