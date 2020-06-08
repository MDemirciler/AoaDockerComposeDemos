## Overview

Download the repository either manually (Clone or Download -> Download as Zip) or via git clone

```
git clone https://github.com/ThinkBigAnalytics/AoaDockerComposeDemos
```

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
docker-compose up
```

If you want to execute the complete stack, run 
```
docker-compose -f aoa-complete.yaml up
```


Then go to [JupyterLab](http://localhost:8888) and enter the password `aoa`. Open the Getting Started notebook and it will contain links to the other services and steps to get going. 


Sutting down and starting from zero is as simple as 

```
docker-compose down
```
 
Sometimes you might have an issue with docker compose not stopping or cleaning up correctly.

```
docker-compose down -v --remove-orphans
```

## Credentials

The following credentials are good to know 

 
| Service   |      Username      |    Password      |
|----------|:-------------:|-------------:|
| AOA |  admin | admin |
| Git |  gituser | gitpassword |
| Jupyter |   | aoa |
| Business Central | admin | admin 
| Minio | minioadmin | minioadmin | 
