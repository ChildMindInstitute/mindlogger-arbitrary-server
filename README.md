#  Mindlogger Mongo docker container

SSL Enabled Mongo Server based on the official mongo 4 Image

## Getting Started

These instructions will cover usage information and for the docker container 

### Prerequisities


In order to run this container you'll need docker and docker-compose installed.


* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)
* [Docker Compose] (https://docs.docker.com/compose/install/)


### Usage

#### Container Parameters

List the different parameters available to your container

```shell
docker run give.example.org/of/your/container:v0.2.1 parameters
```

One example per permutation 

```shell
docker run give.example.org/of/your/container:v0.2.1
```

Show how to get a shell started in your container too

```shell
docker run give.example.org/of/your/container:v0.2.1 bash
```

#### Environment Variables

     MONGO_INITDB_DATABASE: mindlogger
      MONGO_INITDB_ROOT_USERNAME: rootuser
      MONGO_INITDB_ROOT_PASSWORD: rootpass

* `MONGO_INITDB_DATABASE` - Inital Database to be crated during first startup
* `MONGO_INITDB_ROOT_USERNAME` - root username
* `MONGO_INITDB_ROOT_PASSWORD` - root username password

#### Volumes

* `mongovolume` - Docker Volume 

#### Useful File Locations

* `./mongo/mongod.conf` - MongoDB Config File it gets mounted into the Mongo Volume at boot
* `./mongo/mongod.pem` - MongoDB SSL Connection Generated Key
* `./mongo/mongod.key` - MongoDB SSL Connection Generated Pem



## Built With

* List the software v0.1.3
* And the version numbers v2.0.0
* That are in this container v0.3.2

## Find Us

* [GitHub](https://github.com/your/repository)
* [Quay.io](https://quay.io/repository/your/docker-repository)

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the 
[tags on this repository](https://github.com/your/repository/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/repository/contributors) who 
participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Acknowledgments

* People you want to thank
* If you took a bunch of code from somewhere list it here