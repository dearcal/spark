# install spark on docker
## pull docker image from https://hub.docker.com/r/bde2020/spark-master/
```
docker pull bde2020/spark-master
```


## install master
```
docker run --name spark-master -h spark-master -e ENABLE_INIT_DAEMON=false -d bde2020/spark-worker:2.4.5-hadoop2.7
```

## install worker

```
docker run --name spark-worker-1 --link spark-master:spark-master -e ENABLE_INIT_DAEMON=false -d bde2020/spark-worker:2.4.5-hadoop2.7
```


## run spark on docker
```
docker exec -it spark-master bash
```

## change pyspark init with python3
1.edit pyspark file
```
vim /spark/bin/pyspark
```

2.replace python with python3

## you can try pyspark on container
```
/spark/bin/pyspark
```

## you can try scala on container
```
/spark/bin/spark-shell
```


## save changes to a new image
```
docker commit <ContainerID> bde2020/spark-master:ls
```

## restart changed container
```
docker run --name spark-master -h spark-master -e ENABLE_INIT_DAEMON=false -p 7077:7077 -p 6066:6066 -p  8081:8080 -d bde2020/spark-master:ls
```


 