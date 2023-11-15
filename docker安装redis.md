## Linux中docker安装redis

#### 一、安装镜像

1.查询

```java
docker search redis
```

2.拉取

```java
docker pull redis:6.0.8
```

#### 二、创建文件目录

1.创建目录

```java
mkdir /home/redis/conf
mkdir /home/redis/data
```

2.修改配置文件

```java
直接使用文件夹里的redis.conf文件并放到/home/redis/conf里面
```

3.作出的修改

```java
#注意这里要把后台运行设置为no，避免docker后台运行冲突
daemonize no
    
#修改redis密码
requirepass Admin123!
```

#### 三、启动容器

1.启动

```java
docker run --restart=always \
-p 6379:6379 \
--name redis \
--privileged=true \
-v /home/redis/conf/redis.conf:/etc/redis/redis.conf \
-v /home/redis/data:/data \
-d redis:6.0.8 /etc/redis/redis.conf
```

2.进入容器

```java
docker exec -it myredis bash
```

3.启动redis（解决中文乱码）

```java
redis-cli --raw
    
auth Admin123! # 验证redis密码
```

