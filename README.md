## Overview

Download the [docker-compose.yaml](./docker-compose.yaml) and [env config](./aoa-core.env) either manually or via

```
git clone https://github.com/ThinkBigAnalytics/AoaDockerComposeDemos
```

If you want to access Transcend to run the example MLE models etc, you will need to update the [env config](./aoa-core.env) with your Teradata username (your quicklook id) & password.

Ensure you have access to the docker repositories (request it in the AnalyticOps Technical Support team), and have logged into docker

```
docker login
```

Then execute 

```
docker-compose up
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
