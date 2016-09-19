#### MongoDB and Redis  compose 

##### PreReqs
Create data volumes first:
docker volume create --name=redis-data
docker volume create --name=mongo-data

Once done the data is always available until those two volumes are removed. 


##### Setting up Admin user and db: MongoDB



Use MongoDB for document datastore. 
First setup admin user and db:

```
docker exec -it document_store mongo admin
connecting to: admin
> db.createUser({ user: 'admin', pwd: 'db', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
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