---
layout: post
title: computer network introduction
date: 2024-10-19 11:01:00
description: introduction
tags: cs
categories: sample-posts
---

#### some basic word about computer network
host(主机)=end system
servers(服务器)
Routers(路由器)
Switches(交换机)
Protocols(协议)
ISP(Internet Service Provider)

##### protocols
Application :IMAP,SMTP,HTTP
Transport:TCP,UDP
Network:IP
Link
Physical

##### Internet structure:
Network edge:runs network applications网络边缘
- client/server model(web browser/server; email)
- peer-peer model(BitTorrent)

Access networks, physical media接入网
将设备连接到第一个routers


Network core网络核心

##### Packets
将要传输的文件分为一个个更小的单位packets，他的长度为L，将这个packet传送到access network所需的transmission rate R（又叫link capacity，bandwidth带宽）
那没传输延迟就是
$$packet \: transmission\: delay=\frac{L(bits)}{R(bits/sec)}$$


##### Access net
cable network用电缆传输数据
digital subscriber line(DSL)用电话线来传

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/computer_network1.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

##### The network core
==Packet switching== 
- store and forward(packet是按照bit来进行传输，一个路由器必须接受完一个packet之后才可以将这个packet传输出去)
- packet is transmitted at full link capacity
- not reserved
packet switching衍生出的两个问题，如果一个packet传入到一个路由器的速度大于他传输出去的速度，那必然会在output buffer中引起排队(queuing delay)，如果排队的数据过多，他会超出output buffer的容量，产生丢包(packet loss)

==forwarding and routing==
每个路由器中间都有一个转发表(forwarding table)当数据从输入端口时，路由器根据数据包的表头之类的信息将packet输出到路由器合适的端口

路由(routing)他是全局的作用，寻找一个从source到destination中最合适（最快maybe）的路径（路由器线路）然后将这些信息写入转发表中，然后路由器根据转发表将数据传输出去
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/computer_network2.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


==Circuit switching==
每两个设备之间拉一根线，那么对于每一个设备他就要有n根线
保障线路不被占用但非常浪费

##### ISP
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/computer_network3.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    ISP
</div>

##### Performance Metric(性能指标)
1. delay(时延)
	- nodal
		就是packet经过一个路由器到下一个路由器的总时间
		$d_{nodal}=d_{proc}+d_{queue}+d_{trans}+d_{prop}$
		总时延=处理时延（路由器检查packet报文头，确定转发路径）+排队时延+传输时延($\frac{L}{R}$)+传播时延（就是数据从路由器到另一个路由器之间物理链路的时延）
	- end to end
		就是从source到destination的总时间
		$\sum_{i=1}^{N} (nodal\:delay\:of\:nodal\:i)$

	>queueing delay:
	>
	traffic intensity =$\frac{L\lambda}{R}$
	L是每个packet有多少bits
	$\lambda$是平均每秒有多少packets到达这个路由器
	R是transmissions rate
	>
	如果traffic intensity趋近于0意味着他的queueing delay非常的小
	如果接近与1意味着他的queueing delay趋于无穷
	如果大于1那么意味着他的时延是无穷
2. packet loss(丢包)
3. Throughput(吞吐量)
	比特传输的速度
	- instantaneous瞬时
	- average（整个链路中最小的transmission rate R）
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
          {% include figure.liquid loading="eager" path="assets/img/computer_network4.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

##### Internet protocol stack
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/computer_network5.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Internet protocol stack
</div>

##### Encapsulation（封装）
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/computer_network6.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Encapsulation
</div>
