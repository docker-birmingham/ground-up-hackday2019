### Overview

This is a simple Java [Quarkus](https://quarkus.io/) web-application which connects to a [CockroachDB](https://www.cockroachlabs.com/) 
database and reads bank accounts.  It will present a webservice on port `8080` from which it will serve a simple json documents
which have been added byt another service.

You'll need to "Dockerize" this application so that it can run in a container by creating a Dockerfile to generate
an image.

#### Requirements

The image will need the following to run the application, and would be best built using a multi-stage process as
the resultant binary will not need any of the build tooling and can therefore be discarded. 

##### Build

* A CGLib compliant flavour base image
* Latest GraalVM `oracle/graalvm-ce:1.0.0-rc13`
* Maven 3.6.0
* GRAALVM_HOME set (`GRAALVM_HOME=/opt/graalvm-ce-1.0.0-rc13/`)
* The pom.xml and code in the `src` directory

##### Runtime

* A distroless image with basic tools such as (`cescoffier/native-base:latest`)
* The binary in the previous build step `/work/target/getting-started-1.0-SNAPSHOT-runner`
* A flag provided as part execution definition of `-Dquarkus.http.host=0.0.0.0` to bind to all interfaces

#The App

Once containerised the app will look for an instance of CockroachDB running on port `26275` with a user of `maxroach` 
and a database called `bank`.

The url for the database should be provided using an environment variable `DB_URL` which should be the DNS or IP of 
the service.   

The web-application will be available on port `8080` when started.  It have the following endpoint:

`http://localhost:8080/account`

Through which it should be possible to get data about the bank accounts. 
