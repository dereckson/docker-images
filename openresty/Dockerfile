FROM centos:centos6

RUN yum install -y perl gcc gcc-c++ make zlib-devel pcre-devel openssl-devel lua lua-devel lua-socket wget tar curl perl-CPAN

RUN wget http://openresty.org/download/ngx_openresty-1.7.7.1.tar.gz \
&& tar xvfz ngx_openresty-1.7.7.1.tar.gz \
&& cd ngx_openresty-1.7.7.1 \
&& ./configure --with-luajit \
&& make \
&& make install \
&& rm -rf /ngx_openresty*

RUN (echo y;echo o conf build_requires_install_policy yes;echo o conf prerequisites_policy follow;echo o conf commit)|cpan

RUN cpan fi Test::Nginx