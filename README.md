
# Wordpress Docker Config
This repo holds the docker-compose config necessary for setting up a local Wordpress docker image. This makes it easy to setup many Wordpress images locally to manage all your wordpress sites.

## Quick Commands

- `docker-compose up -d` | Start the container at the current directory (in detached mode)
- `docker-compose stop` | Stop the current container
- `docker ps` | View current docker processes

## Installation Instructions

1. Clone this repo and rename it so that it is easily identifiable in Docker.
2. Install [Docker](https://www.docker.com/) on your machine.
3. Install [Kitematic](https://kitematic.com/) to make it easier to view running images, view/edit the mount volume, etc. (*Optional but recommended*)
4. Run the following command to start the image: `docker-compose up -d`
5. Navigate to http://localhost:8000
6. Setup your Wordpress site, and you're ready to go.

**That's it!**
Once you start the app for the very first time, they can easily be turned on/off through the Docker desktop. You can create several folders with several instances of this config, and it will automatically be registered by folder name.

## Overview
The `docker-compose.yml` is the source of truth, but you can modify the config to set up your image however you want. Refer to the [official docs](https://docs.docker.com/compose/compose-file/) to review all the configuration options. This is currently on version 3.

This config hosts the site under the port 8000, but you can fine tune the ports directly in the config if you want to run multiple wordpress images at once. You can read more on the [networking](https://docs.docker.com/network/) capabilitiies to make finer adjustments.

### Modifying Wordpress contents
Wordpress's docker image (as well as any other docker images), have a mount volume that is hidden  and path relative to the VM, so it is completely hidden from your machine and is not easily editable.

You'll need to "screen" into the docker instance in order to view it, as you see in the command below:

```bash
screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty
```

This is kind of a pain in the butt though...So to workaround this, you can try to mount the directory locally using a a command like:

```bash
docker run --rm -it -v /Users/<username>/volume-backup:/backup -v /var/lib/docker:/docker alpine:edge tar cfz /backup/volumes.tgz /docker/volumes/
```

However, I prefer an even easier method. Download [Kitematic](https://kitematic.com/) to view the all of your running images and their mount volumes. Then for your Wordpress image, automatically reconfigure it to change the mount volume to your local machine.
