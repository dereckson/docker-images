Openresty
=========

Docker container with openresty and Nginx::Test 

``̀
$ docker build --rm=true -t artegeie/openresty .
``̀

Run tests :

``̀
$ cd openresty-tests
$ docker run -ti -v `pwd`:/data artegeie/openresty sh -c "cd /data && prove -v"

``̀