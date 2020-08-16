# ElasticSearch

1. 创建一个普通用户，es默认不能使用root用户进行启动，这里创建一个用户"es"  `adduser es`

2. 解压安装包  `tar zxvf elasticsearch-6.6.2.tar.gz`

3. 重命名 `mv elasticsearch-6.6.2 elasticsearch`

4. 移动目录 `mv elasticsearch/ /usr/program/elasticsearch`

5. 用户授权 `chown -R es /usr/program/elasticsearch`

6. 切换用户"es" `su es`

7. 进入 elasticsearch，并启动elasticsearch，输出日志中显示started表示启动成功

    ```shell
    cd elasticsearch/bin
    ./elasticsearch
    ```

8. 验证是否启动成功输入 `curl localhost:9200`

9. 外网访问需要修改配置文件 `vi config/elasticsearch.yml`

    ```shell
    network.host: 0.0.0.0
    ```

10. 设置后台启动，进入到bin目录下，启动后面加参数-d `./elasticsearch -d`

11. 查询es进程 `ps -ef|grep elastic`

12. 文件句柄太少，至少要65536

    * 编辑配置 `vi /etc/security/limits.conf`

        ```shell
        * soft nofile 65536
        * hard nofile 131072
        * soft nproc 2048
        * hard nproc 4096
        ```

13. 虚拟内存太少，至少262144

    * 编辑配置 `vi /etc/sysctl.conf`

        ```shell
        vm.max_map_count=655360
        ```

    * 激活配置 `sysctl -p`
