# MySQL

1. 查询并卸载系统自带的 Mariadb

    ```shell
    rpm -qa | grep mariadb
    rpm -e --nodeps mariadb-libs-5.5.64-1.el7.x86_64
    ```

2. 安装依赖包

    * 安装 libaio `rpm -ivh libaio-0.3.109-13.el7.x86_64.rpm --nodeps --force`

    * 安装numactl `rpm -ivh numactl* --nodeps --force`

    * 安装perl

        ```shell
            rpm -ivh perl-5.16.3-294.el7_6.x86_64.rpm --nodeps --force
            rpm -ivh perl-Getopt-Long-2.40-3.el7.noarch.rpm --nodeps --force
            rpm -ivh perl-Data-Dumper-2.145-3.el7.x86_64.rpm --nodeps --force
            rpm -ivh perl-DBD-MySQL-4.023-6.el7.x86_64.rpm --nodeps --force
        ```

3. 安装MySQL `rpm -ivh mysql-community-* --nodeps --force`

4. 启动MySQL `systemctl start mysqld`

5. 设置开机启动

    ```shell
        systemctl enable mysqld
        systemctl daemon-reload
    ```

6. 修改mysql root 密码

    * 查询临时密码 `grep 'temporary password' /var/log/mysqld.log`

    * 设置新密码

        ```shell
            SET GLOBAL validate_password_policy=LOW;
            SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpassword');
        ```

7. 创建新用户并开启远程登陆

    * 创建用户 `create user 'user'@'%' identified by 'password';`

    * 授权 `grant all privileges on *.* to 'user'@'%';`

    * 开启3306端口 `firewall-cmd --zone=public --add-port=3306/tcp --permanent`

    * 重启防火墙 `firewall-cmd –-reload`

    * 查看端口号3306是否开启 `firewall-cmd --query-port=3306/tcp`

    * 查询开启端口列表 `firewall-cmd --list-port`

8. 配置默认编码为UTF-8

    * 修改/etc/my.cnf配置文件，在[mysqld]下添加编码配置，如下所示：

    ``` shell
        [mysqld]
        character_set_server=utf8
        init_connect='SET NAMES utf8'
    ```

9. 重启 `systemctl restart mysqld`
