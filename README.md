# docker-slpdb
This Docker container sets up
[SLPDB](https://github.com/christroutner/SLPDB) and
[slpserve](https://github.com/fountainhead-cash/slpserve)
to create API endpoints for querying [SLP token](https://simpleledger.cash/) information.

## Installation
It's assumed that you are starting with a fresh installation of Ubuntu 18.04
LTS on a 64-bit machine.
It's also assumed that you are installing as
a [non-root user with sudo privileges](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04).

- Install Docker on the host system.
[This tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04)
shows how to install Docker on a Ubuntu 16.04 system. It's specifically targeted
to Digital Ocean's cloud servers, but should work for any Ubuntnu system.

- Install Docker Compose too.
[This tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-16-04)
shows how to do so on a Ubuntu system.

- Ensure you have a fully-synced BCH full node running on the same machine with
ports 8332 (RPC) and 8333 (p2p) exposed.
This [docker-abc](https://github.com/christroutner/docker-abc) dockerized
full node will do exactly this.

- Clone this repository in your home directory with the following command:

`git clone https://github.com/christroutner/docker-slpdb`

- Customize the [config.ts](config.ts) file to reflect
the setting of your full node. If using
the [BCH JS Toolkit](https://bchjs.cash) no changes are necessary.

- (optional) By default,
the [docker-compose.yml](docker-compose.yml) file is configured to pull the image
from Docker Hub. But the container can also be built from scratch with this
command:

`docker-compose build --no-cache`

6. Bring the container online by running the following command:

`docker-compose up -d`

## Usage
The location of the MongoDB data store is specified in the `docker-compose.yml` file.
This makes it easy to backup the data. However, be sure to shut down the docker
containers before backing up the data, otherwise it will be fragmented and unusable later.

## Docker Debugging
The following commands are useful for debugging applications like this one
inside a Docker container. The commands below help you to enter a shell
inside the container.

* `docker ps -a`
  * Show all docker processes, including ones that are stopped.

* `docker container run --name test-container --rm -it <Image ID> bash`
  * This command will run a docker container and drop you into a bash shell.
  All you need is the image ID.

* `docker exec -it <container ID> bash`
  * This command will let you enter a bash shell inside a running Docker container.
