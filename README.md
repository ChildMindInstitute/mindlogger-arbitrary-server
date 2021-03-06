#  Mindlogger Mongo docker container

SSL Enabled Mongo Server based on the official mongo 4 Image

## Getting Started

These instructions will cover usage information and for the docker container 

### Prerequisities


In order to run this container you'll need docker and docker-compose installed.


* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)
* [Docker Compose](https://docs.docker.com/compose/install/)


### Usage

#### Getting Started

Clone github repository 
```shell
git clone https://github.com/ChildMindInstitute/mindlogger-arbitrary-server.git
```

Build Docker container
```shell
docker-compose build
```

Start the Mongodb docker container
```shell
docker-compose up -d
```

You will be able to login to Mongodb running locally on 0.0.0.0 using the
mapped ports and the credentials specified in the docker-compose.yml

### Ports

Docker/docker-compose maps the following ports
- Local:InsideDocker
- 27017:27017
- 27018:27018
- 27019:27019

#### Environment Variables

* `MONGO_INITDB_DATABASE` - Inital Database to be crated during first startup
* `MONGO_INITDB_ROOT_USERNAME` - root username
* `MONGO_INITDB_ROOT_PASSWORD` - root username password

#### Volumes

* `mongovolume` - Docker Volume 

#### Useful File Locations

* `./mongo/mongod.conf` - MongoDB Config File it gets mounted into the Mongo Volume at boot
* `./mongo/mongod.pem` - MongoDB SSL Connection Generated Key
* `./mongo/mongod.key` - MongoDB SSL Connection Generated Pem




