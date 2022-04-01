#  MindLogger Mongo docker container

SSL Enabled Mongo Server based on the official mongo 4 Image

## Getting Started

This repro is to send user's response data to your own server versus storing the data within MindLogger. These instructions will cover usage information and for the docker container 

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

#### Ports

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

#### Information you need to provide to MindLogger Team 
* Your server environment variables including access information 
* S3 bucket environmentr variables including access information
* Email address of the account owner 

Below is an example of the fields we require: 

```shell
Server IP: XX.XX.XXX.XXX
MONGO_INITDB_DATABASE: XXXXXXX
MONGO_INITDB_ROOT_USERNAME: XXXXXXX
MONGO_INITDB_ROOT_PASSWORD: XXXXXXXX
MONGODB_PORT: XXXXX are open
DB Host URL: XXXXXXXXXXXXX
MindLogger Owner email: XXXXXXXX@XXXXXX.XXX

S3 Bucket
ACCESS_KEY_ID: XXXXXXXXXXXXXXXXXXXXX
SECRET_ACCESS_KEY: XXXXXXXXXXXXXXXXX
Bucket name: XXXXXXXXXX
```

#### Update MongoDB Credential
Once docker file created container (volume), you cannot change the mongodb credentials by simply updating environment variables. You would have to delete the volume(container) completely, update environment variables(username & password) in ``docker-compose.yml``, and rerun the container.

Otherwise, please following instructions to update db password manually by adding a new user.

```shell
docker exec -it mongodb bash
```

```shell
mongo --username [username] --password [password]
```

```shell
db.createUser({user: `[username]`, pwd: '[password]', roles: [{ role: 'readWrite', db:'[database]'}]})
```

Now you can access the database as a new user with new credentials.
