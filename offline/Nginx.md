# Nginx

1. 安装依赖

    * 安装gcc

    ```shell
        rpm -Uvh *.rpm --nodeps --force
        gcc -v
    ```

    * 安装pcre

    ```shell
        rpm -ivh pcre-8.32-17.el7.x86_64.rpm --nodeps --force
        rpm -ivh pcre-devel-8.32-17.el7.x86_64.rpm --nodeps --force
    ```

    * 安装libstdc++（gcc-c++依赖）

    ```shell
        rpm -ivh libstdc++-4.8.5-39.el7.x86_64.rpm --nodeps --force
        rpm -ivh libstdc++-devel-4.8.5-39.el7.x86_64.rpm --nodeps --force
    ```

    * 安装gcc-c++

    ```shell
        rpm -ivh gcc-c++-4.8.5-39.el7.x86_64.rpm --nodeps --force

    ```

    * 安装zlib

    ```shell
        rpm -ivh zlib-1.2.7-18.el7.x86_64.rpm --nodeps --force
        rpm -ivh zlib-devel-1.2.7-18.el7.x86_64.rpm --nodeps --force
    ```

2. 解压安装包 `tar zxvf nginx-1.8.1.tar.gz`

3. 移动目录 `mv nginx-1.8.1/ /usr/program/nginx-1.8.1`

4. 进入解压目录 `cd nginx-1.8.1/`

5. 编译配置 `./configure`

6. 编译 `make`

7. 安装 `make install`

8. 防火墙

    * 关闭防火墙 `systemctl stop firewalld.service`
    * 禁止开机启动 `systemctl disable firewalld.service`
    * 查看防火墙状态 `firewall-cmd --state`

9. 检查nginx进程 `ps aux | grep nginx`

10. 检查是否监听80端口 `netstat -ntulp | grep 80`

11. 启动 `/usr/local/nginx/sbin/nginx`

12. 停止 `/usr/local/nginx/sbin/nginx -s stop`

13. 重启 `/usr/local/nginx/sbin/nginx -s reload`
