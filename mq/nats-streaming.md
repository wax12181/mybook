<!-- TOC -->

- [Nats Streaming](#nats-streaming)
    - [简介](#简介)
    - [使用向导](#使用向导)
        - [server端](#server端)
            - [安装](#安装)
            - [server启动参数介绍](#server启动参数介绍)

<!-- /TOC -->

# Nats Streaming

## 简介

NATS Server是一个简单，高性能的开源消息系统，适用于云本机应用程序，物联网消息传递和微服务架构。

NATS Streaming Server是基于NATS Server的, 增加消息持久化功能的消息系统.

该项目属于CNCF（Cloud Native Computing Foundation）。Synadia团队的成员创建了NATS服务器（用Go编写），NATS Streaming，以及用Python，Ruby，Node.js，Elixir，Java，NGINX，C和C＃编写的客户端。 社区已经提供了越来越多的库，包括Arduino，Rust，Lua，PHP，Perl等

OpenTable，爱立信，HTC，西门子，VMware，Pivotal，GE和百度等公司依靠NATS企业消息系统提供高性能和弹性的功能。

## 使用向导

### server端

#### 安装

- 使用docker安装

```shell
docker run -p 4223:4223 -p 8223:8223 nats-streaming -p 4223 -m 8223
```

详情可参考：[nats-streaming](https://hub.docker.com/_/nats-streaming?tab=description)

#### server启动参数介绍

* 基础属性设置

|名称|说明|值范围|配置文件示例|命令行缩写示例（支持名称，不赘述）|
|:-:|:-:|:-:|:-:|:-:|
|cluster_id|集群名称|字符和下划线组合的字符串|cluster_id: "my_cluster_name"|-cid my_cluster_name|
|discover_prefix|客户端发现服务器的主题前缀|NATS主题|discover_prefix: "_STAN.Discovery"|-|
|store|存储类型|memory<br/>file<br/>sql|store: "file"|-st FILE|
|dir|使用文件存储时，使用该属性设置根目录|文件目录|dir: "/path/to/storage"|-dir /path/to/storage|
|sd|使能Debug级别日志|true<br/>false|sd: true|-|
|sv|使能trace级别日志|true<br/>false|sv: true|-|
|nats_server_url|如果指定，则连接到外部NATS服务器，否则启动嵌入的服务器。|NATS URL|nats_server_url: "nats://localhost:4222"|-|
|secure|如果为true，则创建到服务器的TLS连接，否则不需要使用TLS配置（无NATS服务器证书验证）|true<br/>false|secure: true|-|
|tls|TLS配置|Map: tls: { ... }|-|-|
|store_limits|存储限制|Map: store_limits: { ... }|-|-|
|file_options|文件存储特定选项|Map: file_options: { ... }|-|-|
|sql_options|SQL存储特定选项|Map: sql_options: { ... }|-|-|
|hb_interval|服务器向客户端发送心跳的间隔|Duration|hb_interval: "10s"|-|
|hb_timeout|服务器在将客户端的心跳响应视为失败的心跳之前等待多长时间|Duration|hb_timeout: "10s"|-|
|hb_fail_count|服务器在将客户端的心跳响应视为失败的心跳之前等待多长时间|Duration|hb_timeout: "10s"|-|
|ft_group|在容错模式下，您可以启动一组流服务器，其中只有一台服务器处于活动状态，而其他服务器则处于待机状态。这是FT组的名称|String|ft_group: "my_ft_group"|-|
|partitioning|如果设置为“真”，则必须在“存储限制/通道”部分中定义通道列表。然后，此部分有两个用途，即覆盖给定通道的限制或将其添加到分区中。|true<br/>false|partitioning: true|-|
|cluster|集群配置|Map: cluster: { ... }|-|-|
