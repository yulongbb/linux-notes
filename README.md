# 运维手记

## 测试环境

* 虚拟机：Oracle VM VirtualBox
* 系统镜像：CentOS-7-x86_64-Minimal-1810.iso
* 软件版本

    <table class="table table-bordered table-striped table-condensed">  
        <tr>  
            <th>序号</th>  
            <th>软件</th>  
            <th>版本</th>  
            <th>描述</th>  
        </tr>  
        <tr>  
            <td>1</td>  
            <td>JDK</td>
            <td>1.8.0_72</td>
            <td>JAVA运行环境</td>
        </tr>
        <tr>  
            <td>2</td>  
            <td>Nginx</td>
            <td>1.8.1</td>
            <td>开源Web服务器和反向代理服务器</td>
        </tr>
        <tr>  
            <td>3</td>  
            <td>MongoDB</td>
            <td>3.4.10</td>
            <td>跨平台的面向文档的数据库</td>
        </tr>
        <tr>  
            <td>4</td>  
            <td>ElasticSearch</td>
            <td>6.6.2</td>
            <td>具有RESTful API的分布式，可伸缩且高度可用的实时搜索平台。</td>
        </tr>
        <tr>  
            <td>5</td>  
            <td>Neo4j</td>
            <td>3.5.20</td>
            <td>用Java实现的图形数据库</td>
        </tr>
        <tr>  
            <td>6</td>  
            <td>Redis</td>
            <td>5.0.5</td>
            <td>NoSQL数据库管理软件</td>
        </tr>
        <tr>  
            <td>7</td>  
            <td>FastDFS</td>
            <td>5.05</td>
            <td>轻量级分布式文件系统</td>
        </tr>
        <tr>  
            <td>8</td>  
            <td>RabbitMQ</td>
            <td>3.7.3</td>
            <td>开源消息代理</td>
        </tr>
        <tr>  
            <td>9</td>  
            <td>Nacos</td>
            <td>1.3.2</td>
            <td>动态服务发现、配置和服务管理平台</td>
        </tr>
        <tr>  
            <td>10</td>  
            <td>Docker</td>
            <td>1.13.1</td>
            <td>部署容器化应用程序的开源软件</td>
        </tr>
    </table>

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
* [Nacos](/offline/Nacos.md)

## Docker安装

* [Nginx](/docker/Nginx.md)
* [MySQL](/docker/MySQL.md)
* [MongoDB](/docker/MongoDB.md)
* [ElasticSearch](/docker/ElasticSearch.md)
* [Neo4j](/docker/Neo4j.md)
* [Redis](/docker/Redis.md)
* [FastDFS](/docker/FastDFS.md)
* [RabbitMQ](/docker/RabbitMQ.md)
* [Nacos](/docker/Nacos.md)
* [ArangoDB](/docker/ArangoDB.md)
* [Kibana](/docker/Kibana.md)

## 数据迁移

* [MySQL](/migration/MySQL.md)
* [MongoDB](/migration/MongoDB.md)
* [ElasticSearch](/migration/ElasticSearch.md)
* [Neo4j](/migration/Neo4j.md)
* [Redis](/offline/Redis.md)
* [FastDFS](/migration/FastDFS.md)

## Tips

1. 鼠标脱离Virtual Box虚拟机窗口

    按右ctrl即可

2. Xshell工具中文乱码

    * File -> Properties -> Terminal
    * 将Encoding的值设置为Unicode(UTF-8)

3. 通过Xshell工具连接Virtual Box虚拟机

    * `vi /etc/sysconfig/network-scripts/ifcfg-enp0s3` 将ONBOOT的值改为yes。
    * 关闭虚拟机，将网卡1设为网络地址转换（NAT）,实现悉尼及通过主机网络访问互联网，网卡2设置微host-only，实现主机与虚拟机互联，重启虚拟机。
    * `yum update`
    * `yum search ifconfig`
    * `yum install net-tools.x86_64`
    * ifconfig

## 离线安装包文件请加我微信

![微信二维码](/images/wechat.jpg)
