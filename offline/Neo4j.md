# Neo4j

1. 解压安装包 `tar zxvf neo4j-community-4.1.1-unix.tar.gz`

2. 重命名 `mv  neo4j-community-4.1.1 neo4j`

3. 移动目录 `mv neo4j/ /usr/program/neo4j`

4. 修改配置文件 `vi conf/neo4j.conf`

    ```shell
    dbms.default_listen_address=0.0.0.0
    dbms.default_advertised_address=0.0.0.0
    ```

5. 启动neo4j服务 `./bin/neo4j start`
