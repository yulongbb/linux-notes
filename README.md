# 运维手记

## 测试环境

* 虚拟机：Oracle VM VirtualBox
* 系统镜像：CentOS-7-x86_64-Minimal-1810.iso

## 准备工作

1. 创建文件夹

    * 软件安装包 `/usr/setups`
    * 软件目录 `/usr/program`

    ```shell
    mkdir /usr/setups
    mkdir /usr/program
    ```

2. 防火墙

    * 查看防火墙状态 `firewall-cmd --state`
    * 关闭防火墙 `systemctl stop firewalld.service`
    * 禁止开机启动 `systemctl disable firewalld.service`

## 离线安装

* [JDK](/offline/JDK.md)
* [Nginx](/offline/Nginx.md)
* [MySQL](/offline/MySQL.md)
* [MongoDB](/offline/MongoDB.md)
* [ElasticSearch](/offline/ElasticSearch.md)
* [Neo4j](/offline/Neo4j.md)
* [Redis](/offline/Redis.md)
* [FastDFS](/offline/FastDFS.md)
* [RabbitMQ](/offline/RabbitMQ.md)

## 数据迁移

* [MySQL](/migration/MySQL.md)
* [MongoDB](/migration/MongoDB.md)
* [ElasticSearch](/migration/ElasticSearch.md)
* [Neo4j](/migration/Neo4j.md)
* [Redis](/offline/Redis.md)
* [FastDFS](/migration/FastDFS.md)
