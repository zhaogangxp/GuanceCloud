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

环境说明

1、K8S集群可访问互联网

2、必须安装部署步骤，顺序执行，因为服务间有一定的调用关系，如：nacos调用mysql，必须等mysql启动并初始化完成。各服务模块（auth、gateway、system）必须等待nacos启动完成，以便完成微服务的注册。

3、域名必须使用如下访问（本地客户端指定HOSTS文件强制解析如下域名）：

ruoyi.dataflux.cn 为demo系统的应用（一个微服务业务）

datakit.dataflux.cn 是观测云采集器datakit的Rum数据接收地址

4、该demo的K8S集群外部访问入口使用了Nginx Ingress Controller和Service Type为NodePort，可根据部署时的环境，调整Service Type为各公有云厂商的LB，并做好域名解析。

部署步骤

0、namespace

kubectl create namespace ruoyi

1、datakit

kubectl apply -f datakit1.8.0.yaml

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
