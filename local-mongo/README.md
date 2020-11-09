# docker-dev
Docker-based services to be used in development

## Mongo

Mongo containers for development, provided as docker-compose services

### Services

Two services are provided:

- [Mongodb](https://www.mongodb.com/)
- [NoSqlClient](https://nosqlclient.com/docs/start.html)

## Volumes for holding transient data

Two volumes are declared: **dbdata** e **nosqldata**

They are used to hold data between container restarts.

### First run

When containers get started for the first time, or when volumes are removed, you might want to make some preparations for your development.

With the services running, get into the container, and get into the mongo command line:

```
> cd C:\pub\docker-dev\local-mongo

> docker-compose exec mongodb bash

root@mongodb:/# mongo
MongoDB shell version v4.4.1
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("b98dc6cd-ecc1-49e1-8c31-afa3baa2cb4f") }
MongoDB server version: 4.4.1

>
```

Then (possibly) insert some data for testing, and add users:

```
> use file-axe  

> db.tests.insert({ name: 'doc' })

> db.tests.find().pretty() 

> use admin 

> db.auth('local', 'password') 

# actual values are defined @ MONGO_INITDB_ROOT_USERNAME and MONGO_INITDB_ROOT_PASSWORD

> db.createUser(  
    {
      user: "file-axe",
      pwd: "file-axe",
      roles: [ { role: "readWrite", db: "file-axe" } ]
    }
  )

```

#### NoSqlClient

You may use NoSqlClient to manage your database:

[http://localhost:27018/](http://localhost:27018/)

Don't forget that to **nosqlclient**, the Mongo container is visible as **mongodb** 

```
host/port: mongodb:27017

database name: file-axe

```

Default Authentication type is SCRAM_SHA_1, authentication DB is **admin**, and credentials are specified as **MONGO_INITDB_ROOT_USERNAME** and **MONGO_INITDB_ROOT_PASSWORD**

#### Mongo Compass

If you're using Mongo Compass, the conntection url becomes:

```
mongodb://local:password@localhost:27017/file-axe
```

## Images

[mongo](https://hub.docker.com/_/mongo)

[NoSQLClient](https://hub.docker.com/r/mongoclient/mongoclient/)  (formerly known as mongoclient)

## Additional resources

[Compass](https://www.mongodb.com/products/compass)

[NoSQLClient](https://nosqlclient.com/docs/start.html)

[Aggregation Pipelines](https://docs.mongodb.com/manual/core/aggregation-pipeline/)

