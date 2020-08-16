# Redis

1. 安装依赖 `rpm -Uvh *.rpm --nodeps --force`

2. 查看gcc版本和g++版本

    ```shell
    gcc -v
    g++ -v
    ```

3. 解压安装包 `tar zxvf redis-5.0.5.tar.gz`

4. 移动目录 `mv redis-5.0.5/ /usr/program/redis-5.0.5`

5. 编译 `make`

6. 安装 `make install`

7. 复制配置文件 `cp /usr/program/redis-5.0.5/redis.conf /etc/`

8. 修改配置 `vi /etc/redis.conf`

    ```shell
    bind 0.0.0.0
    daemonize yes
    ```

9. 启动 `/usr/local/bin/redis-server /etc/redis.conf`

10. 查看是否启动 `ps -ef | grep redis`

11. 开机启动配置 `echo "/usr/local/bin/redis-server /etc/redis.conf" >> /etc/rc.local`

12. 关闭 `redis-cli -h 127.0.0.1 -p 6379 shutdown`
