# Production Grade Machine Learning Service  

## Stack
##### ● [Flask](https://flask.palletsprojects.com/en/2.0.x/) as the web framework.
##### ● [Redis](https://redis.io/) for a fast loading of the trained model and other data between the workers.
##### ● [NGINX](https://www.nginx.com/) as a web server and reverse proxy.
##### ● [Gunicorn](https://gunicorn.org/) automatically creates parallel workers/threads according to the capacity of the machine it is running on.  
##### ● [Celery](https://docs.celeryproject.org/en/stable/getting-started/introduction.html) to support asynchronous time-consuming requests as training and initializing the ML model.   

## Important Info
 ● Made to help you scale from a basic Machine Learning project for research purposes to a production grade Machine Learning web service.  
 ● General purpose project, so it assumes that your service needs initialization, training, saving models to the databases for further usage in estimation.  
 ● Based on Docker, so it could be scalable and OS-agnostic.  

<p align="center">
    <img style='width: 500px' src="readme_structure.png"/>
</p>

#### For the detailed API, use the file  [***ml-service.yml***](ml-service.yml)  on any swagger editor, and you will see the API definition.  

#### You can find a postman collection of this service in the file  [***MLServiceStructure.postman_collection.json***](MLServiceStructure.postman_collection.json), use it to validate your deployment. 


Don't forget to create the file ***./src/config.properties*** , use the following template to add the auth-related configuration:  
NOTE: expiry_time_unit **MUST** BE ONE OF THE FOLLOWING:  
(days | seconds | microseconds | milliseconds | minutes | hours | weeks)
```./src/config.properties
[auth_info]
expiry=XXXX
expiry_time_unit=XXXX  
```
*expiry* is basically the amount of time in *expiry_time_unit* for the generated bearer tokens to expire.
example:
```./src/config.properties
[auth_info]
expiry=120
expiry_time_unit=seconds  
```

Also Don't forget to create the file ***./redis/config.properties*** , use the following template to add the redis information:
```./redis/config.properties
MASTER_USER=XXXXX
REDIS_MASTER_PW=XXXXX
REDIS_CELERY_PW=XXXXX
HOST=redis
END_FILE=true
```
There are no restrictions about the values of XXXX in this file, you can use your own or use the following example:
```./redis/config.properties
MASTER_USER=master_user
REDIS_MASTER_PW=1234pw!@$
REDIS_CELERY_PW=4321wp!@$
HOST=redis
END_FILE=true
```
