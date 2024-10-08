# Description



---------------------------------------

### Utils
Take into consideration using the MongoDB extension for VisualStudio code.

### Bash commands for usage

#### Change directory to 0 location


```bash
  cd to Docker/2
```


#### Build images

Fist move the each directory, where each Dockerfile resides, before building. (web/db)

```bash
    docker build -t mongodb:v1.1 .
```

```bash
    docker build -t tiny-web:v1.181 .
```
#### Build basic network

```bash
docker network create my-network
```

#### Run Images
```bash
    docker run -d -p 5002:27017 -v /vol:/data/db --cpus=1 --memory=512m --name tiny-mongodb --network my-network mongodb:v1.1
    docker run -d -v /vol:/data/db --cpus=1 --memory=512m --name tiny-mongodb --network my-network mongodb:v1.1
```


```bash
    docker run -d -p 5001:5000 --cpus=1 --memory=64m --name tiny-web --network my-network -e MONGO_URI=mongodb://tiny-mongodb:27017 tiny-web:v1.181

```

#### Connect to web-server

```bash
    curl localhost:5002
```

#### Connect to instance

```bash
mongosh mongodb://localhost:5002
```

#### Try first insert

```bash

const database = 'FirstDB';
const collection = 'CollectOne';

// Create a new database.
use(database);

// Create a new collection.
db.createCollection(collection);

db.getCollection('CollectOne').insertOne({
    "name": "AleSb",
    "role": "Professional Student"
});

// Find documents where the name is "AleSb"
db.CollectOne.find({name: "AleSb"}).pretty()

```

### Try stop and run the container again

``` bash

docker stop tiny-mongodb
docker start tiny-mongodb
```

