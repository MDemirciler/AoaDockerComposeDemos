## Overview

Download the [docker-compose.yaml](./docker-compose.yaml) either manually or via

```
https://github.com/jupyterlab/jupyterlab/blob/master/binder/requirements.txt
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
| Jupyter |   | aoa |
| Business Central | admin | admin 
| Minio | minioadmin | minioadmin | 