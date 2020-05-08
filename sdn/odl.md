# OpenDayLight

ODL版本采用Sodium SR2 1.2.2

## 环境搭建

1. JDK
    - 版本： Java 8

2. Maven
    - 版本： 3.5.2 or later
    - settings.xml设置

        ```shell
        cp -n ~/.m2/settings.xml{,.orig} ; wget -q -O - https://raw.githubusercontent.com/opendaylight/odlparent/master/settings.xml > ~/.m2/settings.xml
        ```

## 项目管理

- 新建项目

    1. 使用maven generate进行项目初始化

        ```shell
        mvn archetype:generate -DarchetypeCatalog=internal -DarchetypeGroupId=org.opendaylight.archetypes -DarchetypeArtifactId=opendaylight-startup-archetype \
        -DarchetypeCatalog=remote -DarchetypeVersion=1.2.2
        ```

    2. 设置项目的版本信息

        ```shell
        Define value for property 'groupId': : org.opendaylight.example
        Define value for property 'artifactId': : example
        Define value for property 'version':  1.0-SNAPSHOT: : 1.0.0-SNAPSHOT
        Define value for property 'package':  org.opendaylight.example: :
        Define value for property 'classPrefix':  ${artifactId.substring(0,1).toUpperCase()}${artifactId.substring(1)}
        Define value for property 'copyright': : Copyright (c) 2015 Yoyodyne, Inc.
        ```

- 编译项目

    ```shell
    mvn clean install
    ```

- 运行项目

    ```shell
    cd karaf/target/assembly/bin
    ./karaf
    ```
