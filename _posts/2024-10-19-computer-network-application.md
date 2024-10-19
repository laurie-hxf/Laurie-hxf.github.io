---
layout: post
title: computer network application
date: 2024-10-19 16:01:00 +0800
description: application
tags: cs
categories: sample-posts
---
### client-sever architecture(web, email)
##### sever:
- always on host
- 固定的ip地址
##### client
- 可以有动态的ip地址
- 跟sever来进行交流，不直接与client交流

### peer to peer architecture(P2P)
peer之间相互传文件


end system中每一个进程来对message进行发送和接受
每个进程通过sockets来发送和接受
内部的进程间相互交流通过inter-process communication（defined by OS）

### sockets
就是当一个进程想要访问外部资源时，os会帮这个进程创建一个socket，这个socket包含ip+端口+协议（tcp/ udp）这里的端口是os帮忙创建的临时端口，每个进程的端口号是不一样的，然后在同一台设备下运行的process的ip是一样的

这个socket还会包含目标的ip和端口号，这里的端口号一般都是固定的
比如HTTP：80 HTTPS：443
比如我有两个运行在同一台设备的两个process要访问相同的一个网址
```
			不同进程的socket						example.com
• 进程A：<192.168.1.10, 12345, TCP> → <93.184.216.34, 443, TCP>
• 进程B：<192.168.1.10, 12346, TCP> → <93.184.216.34, 443, TCP>
然后目标服务器根据传输来的socket将数据传回去
```

### 选择TCP还是UDP
#### TCP：
- 他要先与sever建立联系（三次握手）
- 更reliable
- 但是更慢
#### UDP：
- 更快
主要适用于直播或其他那种追求响应速度的需求

### WEB
web基于http/https然后也基于tcp协议，因为web不想丢包
URL相当于网址

### HTTP
- non-persistent HTTP
	一次tcp连接只能传一个文件，要下载多个文件就需要建立多次tcp连接
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/19.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
- persistent HTTP
	一次tcp连接可以传多个文件

HTTP请求的header message
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/20.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
HTTP的response message
status code状态码
200 OK
400 not found...
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/21.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### cookie
http没有记忆（stateless）意思就是如果你重复两次请求同一个网页，http不会记住你之前的一些行为，比如如果去购物网站，你添加商品进购物车，这时候你的下一次再访问你讲无法看到你先前添加的商品
这时候就产生cookie他用来记录用户的一些信息，当第一次访问一个网站时，web就会给你分配一个cookie id生成一个数据库，记录你在网站的一些喜好，信息之类的。然后当下一次请求同一个网站时，你的浏览器就会在你的请求里加上这个cookie那么sever就知道对应的喜好，不用再重新配置像语言等的喜好

#### Web caches：proxy（代理）server
就将原sever的一些内容缓存到proxy server中，当想要访问某个页面，就可以直接向proxy sever请求，如果有就直接返回，不用再访问origin sever
- 减轻origin sever的load
- 更快
但这样会有一个问题就是有可能cache中的内容out of date
那么这时候proxy sever可能就要向原sever发送请求保障自己的内容是up to date
但是具体多久检查一次之类就由程序编写决定

### Electronic Mail
user agents(邮箱软件)
mail servers
mail servers要一直运行，不然将无法接收到邮件，这也是必须要有mail sever的原因，不然的话就要让用户的电脑一直保持开机
如果直接让alice发邮件给bob的sever这样邮件可能发送失败，然后用户需要自己一遍遍重新发，如果有了sever就可以让sever来发，同时如果bob想要发送邮件给Alice那么他是发不过去的
还有就是mail sever不是一收到邮件就讲邮件传给用户电脑，而是当用户需要查看邮件打开user agents时server才将邮件传给用户电脑
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/22.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### SMTP
使用TCP协议，在进行TCP的三次握手之后，SMTP也有三次handshaking
220表示sever已经准备好接受邮件了
250表示请求成功
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/23.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
SMTP中的header和body都是ASCII码
#### Mail access protocols

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/24.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
bob的sever将邮件给bob电脑不能是smtp协议因为smtp是一个push的过程，这就要求bob的电脑要一直开机，所以这是就要用HTTP类似的协议因为这是一个pull的过程

### DNS
domain name system
就是将ip地址和网址map的数据库
他还可以将一长串网址的别名（alias）和原网址map起来
他还可以分担服务器的压力
因为一个网站可能有多个服务器支持，那么他就有多个ip，dns可以将这个网址和这些多个ip map起来将访问者分配到不同的ip上面以此来分担压力

#### dns的分层结构
- root DNS severs（根据想要网址的后缀.com.org...进行区分，指出对应的TLD服务器）
- TLD severs
- Authoritative DNS servers
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/25.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
- Local DNS server
	相当于一个缓存，存一些已经知道对应ip的网址，这样用户电脑要访问某个网站的时候，就可以直接问local dns server有没有，如果有就不用在问local dns sever了
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/26.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/27.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    left:iterated query    right:recursive query
</div>

#### DNS records
distributed database storing resource records（RR）
可以理解为dns存储的不同类型数据
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/28.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
如果DNS是authoritative那么他存储的类型就是Type A
对于not authoritative 他应该有一个Type NS和一个Type A
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/29.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/30.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### P2P
他和client-server的传输延时差别
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/31.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/32.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

#### P2P file distribution ：bitTorrent
将文件分为一个个chunks
peers在bitTorrent中发送和接受文件的chunks
在发送和接受时，peer可以随时离开和进来
```
1. 发布文件：当一个用户想要共享某个文件时，他们会生成一个包含文件信息的 **torrent 文件**。这个文件包含了 tracker 的 URL 以及该文件的哈希值等元数据。

2. 连接 tracker：当其他用户想要下载该文件时，他们会通过下载到的 torrent 文件获取到 tracker 的地址，客户端软件会向 tracker 发出一个请求，询问有哪些 peers 拥有该文件。

3. 获取 peers 列表：Tracker 接收到请求后，返回一组活跃的 peers（这些 peers 持有部分或全部文件）。

4. 连接 peers：客户端收到 peers 列表后，开始直接与这些 peers 建立连接，下载或上传文件。

5. 汇报状态：在下载过程中，客户端会定期向 tracker 汇报自己的状态（例如下载进度、是否依然在线），以帮助 tracker 维护最新的网络状态。
```
P2P中有两个主要问题：
- 每个peer传送不同的chunks，我应该先接受哪个chunks呢
	先接收稀有的
- 如果有多个neighbors向我请求，我应该先给谁呢
	谁帮我最多我就先帮他

### Video Streaming
视频就是一系列图片
Coding（Compression）编码（压缩）
1. spatial：对于照片中有一部分是相同颜色，相比于记录每个像素是什么颜色，不如直接记录这个颜色从第几行到第几行
2. 对于连续两张图片而言，与其分别记录两张图片的信息，不如记录其中一张的信息和两张图片之间的差别
video bitrate：视频比特率（视频每秒传输的比特数，通常以 Mbps（百万位每秒）为单位。比特率越高，视频质量越好，但占用的带宽也更大。）
Frame rate：帧率

#### DASH
通常用于在线视频平台或流媒体服务，DASH sever将视频文件切割成许多小的时间片段（通常几秒钟长）。这些片段被独立存储在服务器上，客户端（DASH Client）可以根据需要请求不同质量的片段进行播放。

当用户开始播放视频时，DASH Client（例如网页播放器或视频应用）会根据当前的网络条件选择适当的片段进行下载和播放。如果网络状况较好，客户端会下载高分辨率的片段；如果网络状况较差，客户端则会切换到较低分辨率的片段，以避免缓冲或卡顿现象。

DASH只在流媒体平台中应用，和将视频下载之后再下载不同，DASH就像用视频平台的自动清晰度，根据网络动态调整画面的清晰度以此保证视频的流畅度。而将视频下载之后再看需要一开始就确定视频的清晰度，并且播放时无法改变清晰度。
