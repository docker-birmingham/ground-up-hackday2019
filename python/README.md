### Overview

This is a simple Python Flask web-application which connects to a CockroachDB database and manages bank accounts.
It will present a webservice on port `5000` from which it will serve a simple html webpage and expose an API for
managing accounts.

You'll need to "Dockerize" this application so that it can run in a container by creating a Dockerfile to generate
an image.

#### Requirements

The image will need the following to run the application:

* A CGLib compliant flavour base image
* Python 3.x
* Libraries from the `requirements.txt` file installed by running `python3 -m pip install -r requirments.txt`
* Code in the `app` directory 

#The App

Once containerised the app will look for an instance of CockroachDB running on port `26275` the with a user of `maxroach` 
and a database created called `bank`.  See the root level readme for how to do this.

The url for the database should be provided using an environment variable `DB_URL` which should be the DNS or IP of 
the service.   

The web-application will be available on port `5000` when started. 
