# gc
用途：

观测云快速数据接入Demo演示

Demo可展示功能：

1、K8S环境的微服务

2、Rum UserName埋点

3、Session Replay

4、Web浏览器日志收集

5、Source Map

6、IP地址库

7、K8S Node Pod以及各类Controller等指标

8、K8S业务日志、集群日志

9、观测云PipeLine、日志治理

10、微服务APM

11、APM、Log、Rum、Metrics相互关联

部署步骤

1、datakit

kubectl apply -f dk.yaml

2、redis

kubectl apply -f redis.yaml 

3、mysql

kubectl apply -f mysql.yaml

4、nacos

kubectl -f nacos.yaml

5、auth

kubectl apply -f auth.yaml

6、gateway

kubectl apply -f gateway.yaml

7、system

kubectl apply -f system.yaml

8、web

kubectl apply -f web.yaml
