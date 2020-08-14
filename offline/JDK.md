# JDK

1. 检查JDK命令 `java -version`

2. 查询本地 JDK 安装程序情况 `rpm -qa|grep java`

3. 如果存在老版本的JDK，卸载 `rpm -e --nodeps 软件名称`

4. 解压安装包 `tar -zxvf jdk-8u72-linux-x64.tar.gz`

5. 移动目录 `mv jdk1.8.0_72/ /usr/program/jdk1.8.0_72`

6. 配置环境变量

    * 编辑配置文件 vi /etc/profile
    * 在配置文件的末尾处添加以下内容

    ``` shell
        JAVA_HOME=/usr/program/jdk1.8.0_72
        JRE_HOME=$JAVA_HOME/jre
        PATH=$PATH:$JAVA_HOME/bin
        CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
        export JAVA_HOME
        export JRE_HOME
        export PATH
        export CLASSPATH
    ```

7. 激活配置 `source /etc/profile`

8. 检查JDK是否安装成功 `java -version`
