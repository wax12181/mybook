<!-- TOC -->

- [NAT](#nat)
    - [网络地址转换 （Network Address Transport）](#网络地址转换-network-address-transport)
        - [解决什么问题](#解决什么问题)
        - [定义](#定义)
        - [应用场景](#应用场景)
        - [NAT带来的问题](#nat带来的问题)
    - [NAT策略](#nat策略)
    - [CLI命令整理](#cli命令整理)
        - [奇安信防火墙 （极速墙、智慧墙）](#奇安信防火墙-极速墙智慧墙)
        - [华为墙](#华为墙)
        - [H3C防火墙](#h3c防火墙)
        - [山石防火墙](#山石防火墙)
        - [飞塔防火墙](#飞塔防火墙)
        - [启明星晨防火墙](#启明星晨防火墙)

<!-- /TOC -->

# NAT

## 网络地址转换 （Network Address Transport）

参考：

[网络地址转换](https://zh.wikipedia.org/wiki/%E7%BD%91%E7%BB%9C%E5%9C%B0%E5%9D%80%E8%BD%AC%E6%8D%A2)

[rfc2663](https://tools.ietf.org/html/rfc2663#section-3)

### 解决什么问题

Internet[IPv4地址枯竭](https://zh.wikipedia.org/wiki/IPv4%E4%BD%8D%E5%9D%80%E6%9E%AF%E7%AB%AD)

对于IPV4地址枯竭的问题，IPV6是根本的解决方案，NAT只是临时的解决方案

### 定义

在计算机网络中是一种在IP数据包通过路由器或防火墙时重写来源IP地址或目的IP地址的技术。这种技术被普遍使用在有多台主机但只通过一个公有IP地址访问因特网的私有网络中

1. 基本网络地址转换（Basic NAT）

    仅支持地址转换，不支持端口映射

2. 网络地址端口转换(NAPT)

    支持端口转换的NAT

    - 源地址转换

        发起连接的计算机的IP地址将会被重写，使得内网主机发出的数据包能够到达外网主机。

    - 目的地址转换

        被连接计算机的IP地址将被重写，使得外网主机发出的数据包能够到达内网主机。

### 应用场景

LAN网络（内网）与WAN网络（外网）的边界

        \ | /                  .                               /
    +---------------+  WAN     .           +-----------------+/
    |Regional Router|----------------------|Stub Router w/NAT|---
    +---------------+          .           +-----------------+\
                               .                      |        \
                               .                      |  LAN
                               .               ---------------
                        Stub border

### NAT带来的问题

1. 公用Internet会增加路由环路的风险，需要实现NAT的网络设备设置针对公网IP的路由漏洞

## NAT策略

ACL的补充，解决IPv4地址枯竭对ACL的影响

NAT策略的配置需要ACL的配合才能完成

1. NAT分类
    - 源NAT策略

        内网流量映射外网IP访问外网

    - 目的NAT策略

        外网流量映射内网IP访问内网

2. 流量匹配
    - 链路层
        - 安全域
        - 物理接口
    - 网络层
        - IPV4
        - IPV6
        - ICMP
    - 传输层
        - TCP
        - UDP
        - 自定义传输协议

3. 转换动作
    - 公网地址池
    - 端口
    - 转换类型
        - Basic NAT
        - NAPT

## CLI命令整理

### 奇安信防火墙 （极速墙、智慧墙）

TODO

### 华为墙

- [nat](device/cli/huawei/USG6300/nat.xml)
- [zone](device/cli/huawei/USG6300/zone.xml)
- [address](device/cli/huawei/USG6300/address.xml)
- [nat-address](device/cli/huawei/USG6300/nat-address.xml)
- [system-info](device/cli/huawei/USG6300/system.xml)

### H3C防火墙

### 山石防火墙

### 飞塔防火墙

### 启明星晨防火墙
