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

Remove images   
```
docker image rm image:tag
OR 
docker rmi image:tag
```  

Remove dangling images  
```
docker image prune

docker system prune  

# additionally remove any stopped containers and unused images 
docker system prune -a
```

Docker Hub  
```
docker build --tag neranjan007/jq:1.6 jq/1.6/
Docker login 
docker push neranjan007/jq:1.6
```  

When testing can use:  
```
docker build --tag mummer:test mummer/4.0.0/ --progress=plain 
```

`--progress=plain` prints  all STDOUT/STDERR is printed to screen can see every command being executed


building specific targets:  
```
docker build --target app --tag hmmer:3.3.2 hmmer/3.3.2/ 

docker build --target app --tag neranjan007/mummer:4.0.0-ani mummer/4.0.0/ --progress=plain
```