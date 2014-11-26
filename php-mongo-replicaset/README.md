php-mongo-replicaset
====================

This docker container can be used to execute unit tests with a mongodb database (configure with a replicaset).

By default, command starts mongodb and run phpunit with configuration file into /data/app directory.
It is not very elegant because mongo and php are started in the same container but it is easier.

To build the container
----------------------

```
$ docker build -t artegeie/php-mongo-replicaset .
```

To run the container
--------------------

Container must be run with privileged mode (due to mongodb) :

```
$ cd my-symfony2-project/
$ docker run -it --privileged=true --rm -v `pwd`:/data -w /data artegeie/php-mongo-replicaset
```
