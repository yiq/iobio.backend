iobio.backend
=============
IOBIO backend stack

This repository contains scripts and config files for locally deploy IOBIO backend on any docker-enabled servers

Prerequisites
-------------
  * Docker 1.7.1 or newer  [install doc](https://docs.docker.com/engine/installation/linux/)
  * docker-compose 1.4.2 or newer [install doc](https://docs.docker.com/compose/install/)
  * 60G free disk space

Things to plan before launching
-------------------------------
  * decide where you want to put about 60GB data on, if not root directory (optional step 1)
  * decide if you want to run HTTPS (optional step 2)

Quick-Start
-----------
```bash
git clone https://github.com/yiq/iobio.backend
cd iobio.backend

## optional step 1: if you need to put data volumes on a different drive
## the easiest way is to remove the 'data-vol' directory, and create
## a symbolic link with the same name to where you want to put data in
# rm -r data-vol
# ln -s /mnt/data-vol

## optional step 2: if you want to run HTTPS, copy your certificate and
## key file to nginx/server.crt and nginx/server.key. The certificate
## needs to follow nginx structure if intermediate chain certs are used.
## see: http://nginx.org/en/docs/http/configuring_https_servers.html#chains

./fetch-data.sh             # this will take a while (1)
./fetch-images.sh           # optional (2)
docker-compose up -d
```
Once everything starts up, open a browser on your client machine, and go to `http://<public-hostname>/`

Explaination
------------
### Line (1)
Some of the backend services require data files such as the human reference. This script will download all the required data volumes and uncompress them into $REPO/data-vol. These data volumes will then be mapped into the docker containers.

### Line (2)
Download all the needed docker images manually instead of let docker-compose handle it. This can also be used to update images when newer versions are released in the future.
