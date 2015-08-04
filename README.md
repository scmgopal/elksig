# elksig

Ddockers: 
Elastic Logstash Kibana Sensu Influxdb Grafana

Docker datcontainer for influxdb, elastic
Docker nginx to proxyfy kibana grafana Uchiwa.
Docker slapd to use with nginx authent module.

This docker composition is inspired from another existing (Hera-Monitoring) from nuance-mobility.

https://github.com/Nuance-Mobility/Hera-Monitoring.

![Architecture](https://github.com/alpern95/elksig/blob/master/ELKSIG.png)

# Getting Started

Installation of docker and docker-compose
 
- https://docs.docker.com/installation/
- https://docs.docker.com/compose/install/


## utils and git

sudo apt-get update

sudo apt-get install wget curl ldap-utils git

git clone https://github.com/alpern95/elksig.git

## Installation docker datacontainer and slapd

cd elksig
cd influxdbdata
docker build -t elksig/influxdbdata .
cd ..
cd elasticsearchdata/
docker build -t elksig/elasticsearchdata .
cd ..
cd slapd/
docker build -t elksig/slapd .
cd ..

## Lauch datacontainer

docker-compose -f data-containers.yml up -d
Setup ldap
./setup-ldap-config.sh
Test ldpa
ldapsearch -h localhost -p 389 -xLLL -b "dc=example,dc=com" uid=admin sn givenName cn


