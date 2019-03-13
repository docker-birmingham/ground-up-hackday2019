## Docker Hackday 2019

### Overview

Welcome to the hackday project.  The aim is to containerise two very simple applications which interact with a database,
using docker-compose to orchestrate the components and run some basic tests.

The problems that you will need to solve here using the standard Docker tooling are ones which you'll most likely 
encounter in a real-world environment where you have a distributed polyglot application stack.

### Getting started

You'll need Docker and Docker compose installed on your machine / VM / whatever.  Instructions for this can be found 
on the Docker website for your specific host setup.

You'll find [this compose reference](https://docs.docker.com/compose/compose-file/) really helpful when constructing your
stack!

### Steps


#### CockroachDB 

You'll need to orchestrate either a single CockroachDB node or if you're feeling adventurous, a clsuter!  There are some
instructions which can be followed on the CockroachDB site [here](https://www.cockroachlabs.com/docs/stable/start-a-local-cluster-in-docker.html).

The best approach for this is to create a docker-compose file which will orchestrate the service.  Mapping the
service commands form the website is a good place to start.

Once the cluster is up and running you'll need to seed the database with users via a command such as:

```
./cockroach sql --insecure --host="cockroachdb" --execute="  DROP USER IF EXISTS maxroach; \
                                        DROP DATABASE IF EXISTS bank CASCADE; \
                                        CREATE DATABASE IF NOT EXISTS bank; \
                                        CREATE USER maxroach; \
                                        GRANT ALL ON DATABASE bank TO maxroach;"
```

There's a [really nice looking UI](https://www.cockroachlabs.com/docs/v2.1/admin-ui-cluster-overview-page.html) for 
the database which displays numerous metrics which is available on port 8080 of the process.   

#### Applications

Once you have the database working, you'll need to create images for each of the apps.  The instructions are in READMEs
for each subdir in this repo.

The applications all present http endpoint which should be possible to invoke via curl / the browser and are documented
 in the READMEs.
