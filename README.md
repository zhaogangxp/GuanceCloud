# gc

观测云演示数据

 |K8S|微服务|Pod|Controller|
|:-:|:-:|:-:|:-:|
|浏览器日志|SourceMap|IP解析|会话回放|
|VIP跟踪|eBPF|集群事件|业务日志|
|日志字段治理|APM|Profiling|Mysql|

部署架构图



资源准备

|资源|规格要求|
|:-:|:-:|
|操作系统|CentOS 7.9 Minimal安装|
|Demo主机 |2C 8G 20GB 物理机或云主机1台|
|Demo主机|可访问到观测云SaaS平台|
|电脑|可访问到Demo主机|

注意事项

* 必须该文的ingress控制器，因Demo应用的域名已经绑定此类控制器，并且ingress控制器节点充当网络访问入口。

* 必须按照部署步骤，顺序执行，因为服务间有一定的调用依赖关系，如：nacos调用mysql，必须等mysql启动并初始化完成。各服务模块（auth、gateway、system）必须等待nacos启动完成，以便完成微服务的注册。

* 域名必须使用如下访问（本地客户端指定HOSTS文件强制解析如下域名）：

  ruoyi.dataflux.cn Demo系统的应用（SpringCloud）

  datakit.dataflux.cn 观测云采集器datakit的Rum数据接收地址

部署步骤

1 部署Kubernetes及其Ingress控制器

`下载sealos至Demo主机上，执行如下命令安装集群并部署ingress`

[Sealos4.3.0](https://github.com/labring/sealos/releases/tag/v4.3.0 "Sealos")

```
tar zxvf sealos_4.3.0_linux.tar.gz sealos && chmod +x sealos && mv sealos /usr/bin
sealos run labring/kubernetes:v1.24.0 labring/helm:v3.8.2 labring/calico:v3.22.1 --single
kubectl apply -f ingress.yaml
```

2 在访问Demo的电脑上添加hosts解析如下

```
192.168.167.160 ruoyi.dataflux.cn
192.168.167.160 datakit.dataflux.cn
```
3 创建 应用ID 在观测云控制台-用户访问监测-新建应用

`appid_1ae7755342fb47f0a7bcd62830d557c8`

<div align=left><img src="https://github.com/zhaogangxp/gc/assets/28213758/c66bc3a7-b9c3-4b76-8dfb-eb7de6880010" style="width: 30%;"></div>

4 部署观测云采集器

<font color=#ff0000>修改datakit.yaml中的token为你的观测云工作空间看到的token</font>

`kubectl apply -f datakit.yaml`

5 部署Demo应用

```
kubectl create namespace ruoyi
kubectl apply -f redis.yaml
kubectl apply -f mysql.yaml
```
`kubectl -f nacos.yaml`
```
kubectl apply -f auth.yaml
kubectl apply -f gateway.yaml
kubectl apply -f system.yaml
kubectl apply -f web.yaml
```
