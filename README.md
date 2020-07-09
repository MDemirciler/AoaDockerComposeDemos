- [Overview](#overview)
- [Services and Credentials](#services-and-credentials)
- [Running with JBPM](#running-with-jbpm)
- [Extending / Customizing](#extending---customizing)
- [Troubleshooting](#troubleshooting)
  * [Compose updates not taking effect](#compose-updates-not-taking-effect)
  * [Disk Full Issues](#disk-full-issues)
  * [Vantage Credentials](#vantage-credentials)
  * [Airflow Logs](#airflow-logs)


## Overview

The goal of this repository is to make demos faster, more consistent and more powerful. We try and keep this updated with the latest stable releases and fixed for all the AOA components. This is NOT meant to be a development environment and the JupyterLab that is provided is purely for demo purposes. You can of course use this for POCs and other simple deployment scenarios with guidance and help on the appropriate deployment configuration with the help of the AnalyticOps Service Team. 

You can either [Download](https://github.com/ThinkBigAnalytics/AoaDockerComposeDemos/archive/master.zip) the repository or clone it or clone it via Git.

Open a terminal and navigate to the directory where you clone or downloaded this (making sure to unzip if necessary). **All commands that are executed below assume you're current working directory is in this repository**

If you want to access Transcend or run any of the models using Transcend the MLE, follow the instructions [here](#vantage-credentials).

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


## Services and Credentials

The following credentials are included in the JupyterLab `Getting Started` notebook but we also include here for reference.  

| Service          |   Default Port                                 |   Username    |    Password  |
|----------        |:-------------:                                 |:-------------:|-------------:|
| AOA              | [4200](http://localhost:4200)                  |  admin        | admin        |
| Git              | [3000](http://localhost:3000)                  |  gituser      | gitpassword  |
| Jupyter          | [8888](http://localhost:8888)                  |               | aoa          |
| Business Central | [8081](http://localhost:8081/business-central) | admin         | admin        | 
| Minio            | [9000](http://localhost:9000)                  | minioadmin    | minioadmin   | 
| Airflow          | [9090](http://localhost:9090/admin/)           |               |              |


## Running with JBPM

If you want to execute the extended stack which includes jBPM Business Central and all the automation pieces connected, you can run the following. Note we don't recommend you do that regularly as the stack is very large and consumes a lot of resources. 

```
docker-compose -f docker-compose.yaml -f docker-compose.jbpm.yaml up
```

## Extending / Customizing

Docker compose supports a number of ways to extend and customise compose files without actually editing the main docker-compose.yaml file itself. This is very useful if you want to make some changes but don't want to have to resolve merge conflicts when pulling the latest version. We recommend that you read [this](https://docs.docker.com/compose/extends/) docker-compose documentation to understand the options. 

As the official docker compose documentation providers a complete description, we will only show one simple change here. Imagine we have deployed this on a Linux system and we need to update some of the values as we don't need to use the host name dns we use in Windows and OSX. See the `docker-compose.linux.yaml` file to see how this is done. To use this you would run 

```
docker-compose -f docker-compose.yaml -f docker-compose.linux.yaml up
```

## Troubleshooting

### Compose updates not taking effect

If you pull a new version of the docker-compose scripts or make changes to them locally, those changes will not be reflected unless you perform a `down` command. However, even then, sometimes you might have an issue with docker compose not stopping or cleaning up correctly. Perform the following command to fully cleanup

```
docker-compose down -v --remove-orphans
```

### Disk Full Issues 

You may see disk full issues in any number of places from minio, to docker images to jupyter. If you see it in any of those places or any other location, you will need to free up some space in your docker installation. 

Remember, docker will only use a certain % of your overall disk space on OSX and Windows so you might have lots of free disk space but docker does not as it runs as a VM within your OS.

To see you disk space stats

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

Sometimes the above is not enough and you cannot reclaim enough space. You can see which images are using the most space and then selectively cleanup the versions of those images. The AOA tries to cleanup images it creates during training and evaluation but for scoring it cannot as it does not know when you are finished using them. 

To cleanup all docker images with a given name (i.e. all versions of an image), you can run the following command and replace `imagename` with your docker image name. This is useful if you find a certain image you have been testing with locally, building, etc is consuming a lot of space.

```
docker rmi $(docker images -a --format '{{.Repository}}:{{.Tag}}' | grep 'imagename')
```

### Vantage Credentials

As mentioned in the introduction, if you want to connect to Vantage systems such as Transcend, you must be on the VPN and you must update the aoa-core.env file with your Teradata / Vantage credentials. Note you will need to perform a `docker-compose down` for this to take effect.

### Airflow Logs

By default, we have set the airflow to WARN as they are very very verbose. However, this also means that logs from a docker container execution of a job are not visible either and this makes debugging quite challenging. You can change this by adding the following value to the docker-compose.overrides.yaml

    AIRFLOW__CORE__LOGGING_LEVEL: WARN