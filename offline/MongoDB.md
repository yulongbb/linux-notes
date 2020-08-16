# MongoDB

1. 解压安装包 `tar zxvf mongodb-linux-x86_64-rhel62-3.4.10.gz`

2. 重命名 `mv mongodb-linux-x86_64-rhel62-3.4.10 mongodb`

3. 移动目录 `mv mongodb/ /usr/program/mongodb`

4. 配置系统变量 `vi ~/.zshrc`

    ```shell
    export MONGODB_HOME=/usr/program/mongodb
    export PATH=$MONGODB_HOME/bin:$PATH
    ```

5. 激活配置 `source ~/.zshrc`

6. 测试是否安装成功 `mongod -v`

7. 创建数据库、日志存放目录

    ```shell
    mkdir -p /usr/program/mongodb/data
    mkdir -p /usr/program/mongodb/log
    touch /usr/program/mongodb/log/mongodb.log
    ```

8. 创建配置文件 `vi /etc/mongodb.conf`

    ```shell
    dbpath=/usr/program/mongodb/data
    logpath=/usr/program/mongodb/log/mongodb.log
    logappend=true
    port=27017
    fork=true
    ```

9. 查看mongo是否在运行 `ps -ef | grep mongo`

10. 通过配置文件启动 `mongod -f /etc/mongodb.conf`

11. 进入MongoDB后台管理Shell `cd /usr/program/mongodb/bin && ./mongo`

12. 创建数据库 `use admin`

13. 创建用户并授权

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

14. 修改配置文件，允许远程连接 `vi /etc/mongodb.conf`

    ```shell
    auth=true
    bind_ip = 0.0.0.0
    ```
