# gache

## 介绍 

  gache是一个高可用的Key-Value型nosql数据库最小实现，使用raft实现高可用。

## 安装

```
  go get github.com/xfali/gache
```

## 运行（主从复制）

测试示例如下：

leader:
```
./gache --raft-addr 127.0.0.1:7001 --raft-dir ./tmp/node1 -p 8001
```

follower1:
```
./gache --raft-addr 127.0.0.1:7002 --raft-dir ./tmp/node2 -p 8002 --raft-join 127.0.0.1:8001
```

follower2:
```
./gache --raft-addr 127.0.0.1:7003 --raft-dir ./tmp/node3 -p 8003 --raft-join 127.0.0.1:8001
```

## 运行（分片）

node1:
```
./gache -p 8001 --cluster-port 9001 --cluster-slot 0-5000
```

node2:
```
./gache -p 8002 --cluster-port 9002 --cluster-slot 5001-10000 --cluster-members 127.0.0.1:9001
```

node3:
```
./gache -p 8003 --cluster-port 9003 --cluster-slot 10001-16383 --cluster-members 127.0.0.1:9001
```

## 访问

地址：
http://127.0.0.1:8001/key/${KEY}

### 操作数据库

* POST：

   保存${KEY} 和 body的值
   
* DELETE：

   删除${KEY}
   
* GET:
  
   获得${KEY}对应的值
