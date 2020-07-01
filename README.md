## Overview

You can either [Download](https://github.com/ThinkBigAnalytics/AoaDockerComposeDemos/archive/master.zip) the repository or clone it or clone it via Git.

Navigate to the directory where you clone or downloaded this (making sure to unzip if necessary). **All commands that are executed below assume you're current working directory is in this repository**

```
cd <my-clone-or-download-path>/AoaDockerComposeDemos
```

If you want to access Transcend to run the example MLE models etc, you will need to update the [env config](./aoa-core.env) with your Teradata username (your quicklook id) & password.

Ensure you have access to the docker repositories (request it in the AnalyticOps Technical Support team), and have logged into docker

```
docker login
```

We have two docker-compose files which allow you to run a lightweight (default) and complete AnalyticOps stack. We recommend getting started with the lightweight version as its faster to start and play with. To start the lightweight stack, run

```
docker-compose pull

docker-compose up
```

Then go to [JupyterLab](http://localhost:8888) and enter the password `aoa`. Open the Getting Started notebook and it will contain links to the other services and steps to get going. 


To stop the docker-compose instance, you can `Ctrl-C`. This will simply stop the containers and when you do `up` the next time, it will restart them and you will have all previously trained models, notebook changes, source changes etc.

If you want to perform a clean start and get rid of all changes, perform a `down`

```
docker-compose down
```


## Credentials

The following credentials are included in the JupyterLab `Getting Started` notebook but we also include here for reference.  

| Service   |      Username      |    Password      |
|----------|:-------------:|-------------:|
| AOA |  admin | admin |
| Git |  gituser | gitpassword |
| Jupyter |   | aoa |
| Business Central | admin | admin 
| Minio | minioadmin | minioadmin | 


## Running with JBPM

If you want to execute the complete stack which includes jBPM Business Central and all the automation pieces connected, you can run the following. Note we don't recommend you do that regularly as the stack is very large and consumes a lot of resources. 

```
docker-compose -f aoa-complete.yaml up
```

## Troubleshooting
If you pull a new version of the docker-compose scripts or make changes to them locally, those changes will not be reflected unless you perform a `down` command. However, even then, sometimes you might have an issue with docker compose not stopping or cleaning up correctly. Perform the following command to fully cleanup

```
docker-compose down -v --remove-orphans
```


If you receive a disk full error when running a training check the free disk space that docker is allowed use (its only a certain % of your overall disk space)

```
docker system df
```

You can free up space by doing 

```
docker system prune
```

We have also seen the need to cleanup the docker volumes separately via 

```
docker volume prune
```