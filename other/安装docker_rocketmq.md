来源：https://blog.51cto.com/binghe001/5117065?b=totalstatistic
//安装 Namesrv
docker pull rocketmqinc/rocketmq:4.4.0
docker run -d -p 9876:9876 -v /Users/bianminmin/rocketmq/data/namesrv/logs:/root/logs -v /Users/bianminmin/rocketmq/data/namesrv/store:/root/store --name rmqnamesrv -e "MAX_POSSIBLE_HEAP=100000000" rocketmqinc/rocketmq:4.4.0 sh mqnamesrv

//安装 broker 服务器
/Users/bianminmin/conf
brokerClusterName = DefaultCluster
brokerName = broker-a
brokerId = 0
deleteWhen = 04
fileReservedTime = 48
brokerRole = ASYNC_MASTER
flushDiskType = ASYNC_FLUSH
brokerIP1 = 192.168.1.2

docker run -d -p 10911:10911 -p 10909:10909 -v  /Users/bianminmin/data/broker/logs:/root/logs -v  /Users/bianminmin/rocketmq/data/broker/store:/root/store -v  /Users/bianminmin/rocketmq/conf/broker.conf:/opt/rocketmq-4.4.0/conf/broker.conf --name rmqbroker --link rmqnamesrv:namesrv -e "NAMESRV_ADDR=namesrv:9876" -e "MAX_POSSIBLE_HEAP=200000000" rocketmqinc/rocketmq:4.4.0 sh mqbroker -c /opt/rocketmq-4.4.0/conf/broker.conf

//安装 rocketmq 控制台
docker pull pangliang/rocketmq-console-ng
docker run -e "JAVA_OPTS=-Drocketmq.namesrv.addr=192.168.1.2:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false" -p 8080:8080 -t pangliang/rocketmq-console-ng


