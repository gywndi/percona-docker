FROM centos:6.9

MAINTAINER gywndi <gywndi@gmail.com>

# the numeric UID is needed for OpenShift
RUN useradd -u 1001 -r -g 0 -m -s /bin/bash -c "Default Application User" mysql

ENV PERCONA_MAJOR 57

RUN yum -y update 
RUN yum -y install http://www.percona.com/downloads/percona-release/redhat/0.1-4/percona-release-0.1-4.noarch.rpm 
RUN yum -y install Percona-Server-server-$PERCONA_MAJOR 
RUN yum -y install Percona-Server-tokudb-$PERCONA_MAJOR 
RUN yum -y install Percona-Server-rocksdb-$PERCONA_MAJOR 
RUN rm -rf /etc/percona-server.conf.d/*
RUN rm -rf /var/lib/mysql /var/log/mysql
RUN mkdir -p /var/lib/mysql /var/log/mysql
RUN chown -R 1001:0 /var/lib/mysql /var/log/mysql

RUN echo "LD_PRELOAD=/usr/lib64/libjemalloc.so.1" >> /etc/default/mysql
RUN echo "THP_SETTING=never" >> /etc/default/mysql

VOLUME ["/var/lib/mysql", "/var/log/mysql"]

COPY ps-entry.sh /entrypoint.sh
COPY my.cnf /etc/my.cnf.d/my.cnf

ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306

USER 1001

CMD [""]
