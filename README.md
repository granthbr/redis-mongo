#### MongoDB and Redis  compose 
##### Setting up Admin user and db: MongoDB

Use MongoDB for document datastore. 
First setup admin user and db:

```
docker exec -it document_store mongo admin
connecting to: admin
> db.createUser({ user: 'jsmith', pwd: 'some-initial-password', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
Successfully added user: {
    "user" : "admin",
    "roles" : [
        {
            "role" : "userAdminAnyDatabase",
            "db" : "persist"
        }
    ]
}
```
Access DB store from command line:

```
docker exec -it document_store mongo
```

#### External Data Stores
I prefer to use external data stores. So on OSX create a directory to contain
data store i.e. 
```
mkdir /Users/<your home dir>/mondo-data
mkdir /Users/<your home dir>/redis-data
```

And create them:
```
docker create -v $PWD/redis-data --name redis-data alpine:latest scratch test
docker create -v $PWD/mongo-data --name mongo-data alpine:latest scratch test
```