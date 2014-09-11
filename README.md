YADC
===

Yet Another Dockerized CouchDB.
Put the couch in a docker container and ship it anywhere.

This is the RaceHub fork! We forked to publish a stable, versioned container for the [Dokku CouchDB plugin](https://github.com/racehub/dokku-couchdb-plugin).

If you're looking for a CouchDB with SSL support you can check out [klaemo/couchdb-ssl](https://index.docker.io/u/klaemo/couchdb-ssl/)

Version: `CouchDB 1.6.0`

## Run

Available in the docker index as [racehub/couchdb](https://index.docker.io/u/racehub/couchdb)

```bash
[sudo] docker pull racehub/couchdb:latest

# expose it to the world on port 5984
[sudo] docker run -d -p 5984:5984 --name couchdb racehub/couchdb

curl http://localhost:5984
```

## Features

* built on top of the solid and small `debian:wheezy` base image
* exposes CouchDB on port `5984` of the container
* runs everything as user `couchdb` (security ftw!)
* docker volumes for data, logs and config

The previous version of this image used to come with a process manager to keep
CouchDB running. As of Docker 1.2 you can use the `--restart` flag to accomplish this.

## Build your own

You can use `racehub/couchdb` as the base image for your own couchdb instance.
You might want to provide your own version of the following files:

* `local.ini` for CouchDB

Example Dockerfile:

```
FROM racehub/couchdb

ADD local.ini /usr/local/etc/couchdb/
```

and then build and run

```
[sudo] docker build -t you/awesome-couchdb .
[sudo] docker run -d -p 5984:5984 -v ~/couchdb:/usr/local/var/lib/couchdb you/awesome-couchdb
```

## Next Steps

Some nice additional tasks would be:

- Version tags as CouchDB gets upgraded inside the Dockerfile
- Add version tags to the CouchDB plugin
- Turn the Docker Hub repo into a trusted build, built directly off of this repo
- A tutorial on how to bind the internal persistence volume to a data container for backups
