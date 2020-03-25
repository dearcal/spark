# 在docker上安装spark
## 拉安装好spark的镜像 https://hub.docker.com/r/bde2020/spark-master/
```
docker pull bde2020/spark-master
```


## 安装master节点
```
docker run --name spark-master -h spark-master -e ENABLE_INIT_DAEMON=false -d bde2020/spark-worker:2.4.5-hadoop2.7
```

## 安装worker节点

```
docker run --name spark-worker-1 --link spark-master:spark-master -e ENABLE_INIT_DAEMON=false -d bde2020/spark-worker:2.4.5-hadoop2.7
```


## 在docker上运行镜像
```
docker exec -it spark-master bash
```

## 更改初始化pyspark python2为python3 环境
1.edit pyspark file
```
vim /spark/bin/pyspark
```

2.replace python with python3

## 尝试用python 
```
/spark/bin/pyspark
```

## 尝试用scala
```
/spark/bin/spark-shell
```


## 保存更改的容器到新镜像
```
docker commit <ContainerID> bde2020/spark-master:ls
```

## 重新启动容器并暴露端口
```
docker run --name spark-master -h spark-master -e ENABLE_INIT_DAEMON=false  -p  8081:8080 -d bde2020/spark-master:ls
```



 