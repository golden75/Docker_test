# Docker_test   

test

```
mkdir fastqc/0.11.9
cd fastqc/0.11.9 
touch dockerfile
```

dockerfile will look like:
```
FROM ubuntu:latest

RUN apt-get update && apt-get upgrade 

WORKDIR /data
```

create a docker using build command. 
```
docker build -t neranjan007/fastqc:0.11.9 .
``` 

To check the avaliable docker images:  
```
docker images
``` 


login to the docker container using:  
```
docker run -it neranjan007/fastqc:0.11.9
``` 
