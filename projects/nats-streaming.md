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

[使用docker安装](https://hub.docker.com/_/nats-streaming?tab=description)

#### server启动参数介绍

|名称|配置文件|命令行|值范围|描述|
|:-:|:-:|:-:|:-:|:-:|