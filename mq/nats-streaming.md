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

详情可参考： [nats docs](https://nats-io.github.io/docs/)

### server端

#### 安装

- 使用docker安装

```shell
docker run -p 4223:4223 -p 8223:8223 nats-streaming -p 4223 -m 8223
```

详情可参考：[nats-streaming](https://hub.docker.com/_/nats-streaming?tab=description)

#### server启动参数介绍

可以使用配置文件配置特定于NATS流服务器的选项。使用-sc或-stan_config命令行参数指定要使用的文件。

对于嵌入的NATS服务器，可以使用另一个配置文件，并使用-c或--config命令行参数将其传递给流服务器。

由于大多数选项不重叠，因此可以将所有选项合并到单个文件中，并使用-sc或-c命令行参数指定此文件。

但是，名为tls的选项对于nats服务器和nats流服务器是通用的。如果计划使用单个配置文件并配置TLS，则`streaming`中应包含所有流配置。不管您是否使用TLS，这实际上是一个很好的实践，以防止在NATS服务器中添加可能与NATS流服务器选项名称冲突的新选项。

但是，如果要避免任何可能的冲突，只需使用两个不同的配置文件！

注意在NATS流服务器启动期间应用选项的顺序：
    1. 从一些合理的默认选项开始。
    2. 如果指定了配置文件，请使用文件中定义的所有选项覆盖这些选项。这包括已定义但未指定值的选项。在这种情况下，将使用选项类型的零值。
    3. 任何命令行参数都会覆盖以前的所有设置选项。

- NATS Streaming设置

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
|encrypt|指定存储消息时服务器是否应加密消息（仅有效负载）|true<br/>false|encrypt: true|-|
|encryption_cipher|用于加密的密码。目前支持AES和Chaha（Chachapoly）。默认为AES|AES<br/>CHACHA|encryption_cipher: "AES"|-|
|encryption_key|加密密钥。建议通过nats-streaming-encryption-key环境变量指定密钥。|String|encryption_key: "mykey"|-|

- TLS配置

    请注意，流服务器使用与NATS服务器的连接，因此NATS流TLS配置实际上是客户端TLS配置。

|名称|说明|值范围|配置文件示例|命令行缩写示例（支持名称，不赘述）|
|:-:|:-:|:-:|:-:|:-:|
|client_cert|流服务器的客户端密钥|File path|client_cert: "/path/to/client/cert_file"|-|
|client_key|流服务器的客户端证书|File path|client_key: "/path/to/client/key_file"|-|
|client_ca|流服务器的客户端证书CA|File path|client_ca: "/path/to/client/ca_file"|-|

- 存储限制配置

|名称|说明|值范围|配置文件示例|命令行缩写示例（支持名称，不赘述）|
|:-:|:-:|:-:|:-:|:-:|
|max_channels|最大通道数，0表示无限制|Number >= 0|max_channels: 100|-|
|max_subs|单个通道最大订阅数，0表示无限制|Number >= 0|max_subs: 100|-|
|max_msgs|单个通道最大消息数，0表示无限制|Number >= 0|max_msgs: 10000|-|
|max_bytes|单个通道最大消息数，0表示无限制|Number >= 0|max_bytes: 1GB|-|
|max_age|日志中可以保留多长时间的消息|Duration|max_age: "24h"|-|
|max_inactivity|在没有任何订阅和任何新消息的情况下自动删除通道的时间|Duration|max_inactivity: "24h"|-|
|channels|根据通道名称对通道进行特殊限制配置|Map: channels: { ... }|-|-|

根据通道名称对通道进行特殊限制配置举例：

```json
streaming: {
    channels: {
        "foo": {
            max_msgs: 100
        }
    }
}
```

- 存储为文件时的配置

|名称|说明|值范围|配置文件示例|命令行缩写示例（支持名称，不赘述）|
|:-:|:-:|:-:|:-:|:-:|
|compact|启用/禁用文件压缩。只有部分文件（clients.dat和subs.dat）需要压缩|true<br/>false|compact: true|-|
|compact_fragmentation|压缩比率|Number >= 0|compact_fragmentation: 50|-|
|compact_interval|压缩新文件的最小时间间隔|以秒表示|compact_interval: 300|-|
|compact_min_size|尝试压缩前文件大小的下限值|Bytes|compact_min_size: 1GB|-|
|buffer_size|可用于缓冲区写入操作的缓冲区大小|Bytes|buffer_size: 2MB|-|
|crc|定义是否应在读取时计算记录的CRC(Cyclic Redundancy Check 循环冗余校验)|true<br/>false|crc: true|-|
|crc_poly|您可以选择CRC多项式。请注意，在记录被持久化后更改值将导致服务器无法开始反馈数据损坏。|Number >= 0|crc_poly: 3988292384|-|
|sync_on_flush|定义服务器在刷新期间是否应执行“文件同步”操作|true<br/>false|sync_on_flush: true|-|
|slice_max_msgs|定义文件切片最大消息数。如果设置为0并且设置了通道计数限制，那么服务器将自动设置切片计数限制。|Number >= 0|slice_max_msgs: 10000|-|
|slice_max_bytes|定义文件切片的最大大小（包括索引文件的大小）。如果设置为0并且设置了通道大小限制，那么服务器将自动设置一个切片字节限制。|Bytes|slice_max_bytes: 64MB|-|
