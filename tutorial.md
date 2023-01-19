##  day1   

```
docker run staphb/ncbi-datasets:latest datasets download genome accession GCF_000240185.1
```

```  
docker run --rm -u $(id -u):$(id -g) -v $(pwd):/data staphb/ncbi-datasets:latest datasets download genome accession GCF_000240185.1
```

`$(id -u):$(id -g)` : Username or UID (format : <name|uid>[:<group|gid>])   

`-v $(pwd):/data`  : bind mount volume: This mounts the current directory to `/data`

```  
unzip ncbi_dataset.zip 
cp ncbi_dataset/data/GCF_000240185.1/GCF_000240185.1_ASM24018v2_genomic.fna .

docker run --rm -u $(id -u):$(id -g) -v ${PWD}:/data staphb/kleborate:latest kleborate --all -o results.txt -a GCF_000240185.1_ASM24018v2_genomic.fna
```
`--rm` removes the container once it’s done running, but the image remains

To remove an image, you’ll need something like docker rmi imagename:tag


To start the docker 
```
service docker stop
service docker start
```
to clear docker images so it will give space
```
docker system prune --volumes -a
```

