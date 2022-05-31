#  MindLogger Mongo docker container

SSL Enabled Mongo Server based on the official mongo 4 Image

This repro is to send user's response data to your own server versus storing the data within MindLogger. These instructions will cover usage information and for the docker container 

## Prerequisities

In order to run this container you'll need docker and docker-compose installed.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)
* [Docker Compose](https://docs.docker.com/compose/install/)

## Usage

### Getting Started

#### 1. Clone github repository 

```
git clone https://github.com/ChildMindInstitute/mindlogger-arbitrary-server.git
```

#### 2. Update/Set admin configurations

Mke sure you do not use default credentials - go to ``docker-compose.yml`` and update environment variables before running the container. You can't change it again once you run docker.
#### Environment Variables

* `MONGO_INITDB_DATABASE` - Inital Database to be crated during first startup
* `MONGO_INITDB_ROOT_USERNAME` - root username
* `MONGO_INITDB_ROOT_PASSWORD` - root username password

There are other configurations of docker container and below are descriptions. If you do not want to use defaults, we recommend you to update it in ``docker-compose.yml``.

#### Volumes

* `mongovolume` - Docker Volume 

#### Useful File Locations

* `./mongo/mongod.conf` - MongoDB Config File it gets mounted into the Mongo Volume at boot
* `./mongo/mongod.pem` - MongoDB SSL Connection Generated Key
* `./mongo/mongod.key` - MongoDB SSL Connection Generated Pem

#### Ports

Docker/docker-compose maps the following ports
- Local:InsideDocker
- 27017:27017
- 27018:27018
- 27019:27019
  
#### 3. Build and start the Mongodb docker container

```
docker-compose up -d
```

You will be able to login to Mongodb running locally on 0.0.0.0 using the
mapped ports and the credentials specified in the docker-compose.yml

### Test MongoDB Server Setup

To test if the mongodb server was successfully installed, you can run the command below

```
docker exec -it mongodb mongo localhost:27017/admin -u < MONGO_INITDB_ROOT_USERNAME > -p <MONGO_INITDB_ROOT_PASSWORD>
```

The ``MONGO_INITDB_ROOT_USERNAME`` and ``MONGO_INITDB_ROOT_PASSWORD`` has to previously be configured in the docker-compose.yml file.

#### Update MongoDB Credential
Once docker container is created, you cannot change the mongodb credentials by simply updating environment variables. You would have to delete the volume(container) completely, update environment variables(username & password) in ``docker-compose.yml``, and rerun the container.
Refer [this document](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes) to learn how to remove docker container.

Otherwise, the only way is manually add a new user with new db credentials. (But this is not recommended)

```
docker exec -it mongodb bash

mongo --username [username] --password [password]

db.createUser({user: `[username]`, pwd: '[password]', roles: [{ role: 'readWrite', db:'[database]'}]})
```

Now you can access the database as a new user with new credentials.


### Storage Account Setup

Once you have successfully run mongodb server, now you need to set up a storage account for specific usage of storing secured assets.

Mindlogger supports the follow 3 types of storage accounts:
 - [ AWS S3 Bucket ](https://docs.aws.amazon.com/AmazonS3/latest/userguide/GetStartedWithS3.html)
 - [ Google Storage Bucket ](https://cloud.google.com/storage/docs/creating-buckets)
 - [ Azure Storage Account ](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&tabs=azure-portal)

### Information you need to provide to MindLogger Team 

Once everything is setup, you need to provide the following information to Mindlogger Team.

* Your server environment variables including access information
* Storage account environment variables including access information
* Email address of the account owner 

Below is an example of the fields we require: 

**Server Information**
```
Server IP: XX.XX.XXX.XXX
MONGO_INITDB_DATABASE: XXXXXXX
MONGO_INITDB_ROOT_USERNAME: XXXXXXX
MONGO_INITDB_ROOT_PASSWORD: XXXXXXXX
MONGODB_PORT: XXXXX are open
MindLogger Owner email: XXXXXXXX@XXXXXX.XXX
```
**Storage Account Information**

- S3 Bucket
```
Bucket Name: XXXXXX
ACCESS_KEY_ID: XXXXXXXXXXXXXXXXXXXXX
SECRET_ACCESS_KEY: XXXXXXXXXXXXXXXXXXXXX
```
- Google Storage
```
Bucket Name: XXXXXX
Service Account: XXXXXXXXXXXXXXXXXXXXX
ACCESS_KEY: XXXXXXXXXXXXXXXXXXXXX
SECRET_ACCESS_KEY: XXXXXXXXXXXXXXXXXXXXX
```
- Azure Storage
```
Bucket Name: XXXXXX
ACCESS_KEY: XXXXXXXXXXXXXXXXXXXXX
Connection String: XXXXXXXXXXXXXXXXXXXXX
```
