# japanica-warehouse

A docker image and container of PostgreSQL with the columnar store. The current version uses the [citusdata/citus](https://github.com/citusdata/citus), an extension for PostgreSQL. It is assumed that the data in the database is used in a training machine learning model or an autonomous AI system.

## Table of content

- [Bulding steps](#Building-steps)
    - [Build image from docker-compose](#Build-image-from-docker-compose)
    - [Run container](#Run-container)
    
## Building steps

### Build image from docker-compose

You don't need to build the image if you use the image from the docker hub. But you can build the image manually. Here are the build steps.

```shell
# Clone this repository.
$ git clone https://github.com/takahish/japonica-warehouse.git

# Build postgres-cstore image.
$ docker-compose -f docker-compose-for-build.yml build
```

### Run container

```shell
# Detach japonica-warehouse.
# Here is the commands if you build image manually.
$ docker-compose -f docker-compose-for-build.yml up -d

# ... or you can run the container directly from the image from the docker hub.
# After this step, I will describe the topics using the image from the docker hub.
$ docker-compose up -d

# Here are psql connection settings from a local environment. 
$ export PGUSER=jwhuser
$ export PGPASSWORD=jwhuser

# Connect persistent-postgres-cstore.
# Prerequisite is to install postgresql for using psql.
# Note: In the internal network in a docker environment, the 5432 port is used as a database connection. 
# But in the external network, the 5500 port is used as the connection away from the docker environment.
$ psql -h localhost -d jwh -p 5500
psql (13.1, server 12.11 (Debian 12.11-1.pgdg110+1))
Type "help" for help.

dwh=# \dt
Did not find any relations.
dwh=# \q
```

## Remarks

The japonica-warehouse is assumed to be a backend of [japonica-notebook](https://github.com/takahish/japonica-notebook) as the primary use case. Japonica Notebook is famous as the study notebook at the elementary school in Japan. Therefore, I hope the japonica-notebook and japonica-warehouse help those who want to experiment and explore a machine learning algorithm on your project and who want to manage the datasets and the metadata that includes the experimental results, etc., by using the notebook or database, the same as a student in elementary school writes and tracks their study history. Here is the Amazon link for the [Japonica Learning book](https://www.amazon.co.jp/%E3%82%B8%E3%83%A3%E3%83%9D%E3%83%8B%E3%82%AB%E5%AD%A6%E7%BF%92%E5%B8%B3/s?k=%E3%82%B8%E3%83%A3%E3%83%9D%E3%83%8B%E3%82%AB%E5%AD%A6%E7%BF%92%E5%B8%B3) and special thanks to [SHOWA NOTE CO., LTD.](https://www.showa-note.co.jp/)

![Japonica_Learning_Book](https://user-images.githubusercontent.com/6460090/223916928-cd93d5bb-68c6-4d4a-bb3f-7272479e74c1.jpg)
