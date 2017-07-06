# KingDB #
A hierarchical in-memory data store with a RESTful API.

## Why use a hierarchical data store? ##
Some applications can represent their data model as a hierarchy of entities. A specialized data store can take advantage of optimized data structures, simplify the query model and reduce application development time and complexity.

Relational database can be slow since joins are performed at query time. Moreover, they often require the application to make a trade-off between making multiple round trips or repeating the joinned data when a query involves many tables.

Graph databases perform fast joins with hard-links, but provide too much flexibility in how entities are related. For a hierarchy data model, the client application is left with the responsibility of defining the edges that connect the vertices in every query. With graph databases, clients must construct a query string, which in essence redundantly redeclares the data model. There is a neglible but existent step for the graph databases to parse this query on every request.

Key-Value stores provide the fastest reads when all data is stored as a JSON blob, but frequently modifying a deeply nested value becomes an inneficient and perhaps complex task.

Document stores need to make multiple round trips to get the child entities. The alternative is to store all the data into a single, highly-nested document, which is inneficient to update, and so large that it can be difficult to work with.

## Features ##
- Queries can return any entity in any of the hierarchy levels.
- Queries can specify the depth level of child entities to reduce the amount of data returned.
- Each entity can be updated independently of it's parent or child entities.
- In memory storage provides speedy reads and writes atomically.
- A RESTful HTTP interface combines the application relational logic and the data store. When there is no additional domain logic, putting KingDB behind an API Gateway makes writing REST APIs unnecessary. As a consequence, deployments are simpler and the number of servers is reduces.

## Setting up KingDB ##

#### Prerequisites ####
Go > 1.8

#### Compiling into a binary ####
```
go get bitbucket.org/enticusa/kingdb
cd $GOPATH/bitbucket.org/enticusa/kingdb
go install
```

#### Running the database ####
```
$GOPATH/bin/kingdb --labels parent,child,grandchild
```

#### CLI Options ###
```
  -addr string
        The binding address (default ":6789")
  -labels string
        A comma-separated, ordered list of the labels of elements in the hieararchy
```

## REST API ##