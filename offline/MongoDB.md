# MongoDB

1. 解压安装包 `tar zxvf mongodb-linux-x86_64-rhel62-3.4.10.gz`

2. 重命名 `mv mongodb-linux-x86_64-rhel62-3.4.10 mongodb`

3. 移动目录 `mv mongodb/ /usr/program/mongodb`

4. 配置系统变量

    ```shell
        vi ~/.zshrc
        export MONGODB_HOME=/usr/program/mongodb
        export PATH=$MONGODB_HOME/bin:$PATH
        source ~/.zshrc
    ```

5. 测试是否安装成功 `mongod -v`

6. 创建数据库、日志存放目录

    ```shell
        mkdir -p /usr/program/mongodb/data
        mkdir -p /usr/program/mongodb/log
        touch /usr/program/mongodb/log/mongodb.log
    ```

7. 创建配置文件

    ```shell
        vi /etc/mongodb.conf
        dbpath=/usr/program/mongodb/data
        logpath=/usr/program/mongodb/log/mongodb.log
        logappend=true
        port=27017
        fork=true
    ```

8. 查看mongo是否在运行 `ps -ef | grep mongo`

9. 通过配置文件启动 `mongod -f /etc/mongodb.conf`

10. 进入MongoDB后台管理Shell `cd /usr/program/mongodb/bin && ./mongo`

11. 创建数据库 `use admin`

12. 创建用户并授权

    ```shell
        db.createUser(
            {
                user: "yulongbb",
                pwd: "eszrdxtfc",
                roles: [
                    { role: "root", db: "admin" },
                ]
            }
        )
    ```

13. 开放防火墙端口

    * 开启27107端口 `firewall-cmd --zone=public --add-port=27107/tcp --permanent`
    * 重启防火墙 `firewall-cmd –-reload`
    * 查看端口号27017是否开启 `firewall-cmd --query-port=27017/tcp`
    * 查询开启端口列表 `firewall-cmd --list-port`

14. 修改配置文件，允许远程连接 `vi /etc/mongodb.conf`

    ```shell
        auth=true
        bind_ip = 0.0.0.0
    ```
