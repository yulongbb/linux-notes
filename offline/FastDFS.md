# FastDFS

1. 安装依赖 `rpm -Uvh *.rpm --nodeps –-force`

2. 安装 `libfastcommon-1.0.7.tar.gz`

3. 解压 `tar zxvf libfastcommon-1.0.7.tar.gz`

4. 移动目录 `mv libfastcommon-1.0.7/ /usr/program/libfastcommon-1.0.7`

5. 进入目录 `cd /usr/program/libfastcommon-1.0.7`

    * 编译 `./make.sh`
    * 安装 `./make.sh install`
    * 设置软连接

        ```shell
        ln -s /usr/lib64/libfastcommon.so /usr/local/lib/libfastcommon.so
        ln -s /usr/lib64/libfastcommon.so /usr/lib/libfastcommon.so
        ln -s /usr/lib64/libfdfsclient.so /usr/local/lib/libfdfsclient.so
        ln -s /usr/lib64/libfdfsclient.so /usr/lib/libfdfsclient.so
        ```

6. 安装 tracker （跟踪器）服务 `FastDFS_v5.08.tar.gz`

    * 解压 `tar zxvf fastdfs-5.05.tar.gz`
    * 移动目录 `mv fastdfs-5.05/ /usr/program/fastdfs-5.05`
    * 进入目录 `cd /usr/program/fastdfs-5.05`
    * 编译 `./make.sh`
    * 安装 `./make.sh install`

7. 配置 tracker 服务

    * 复制配置文件 `cp /etc/fdfs/tracker.conf.sample /etc/fdfs/tracker.conf`
    * 创建文件夹 `mkdir -p /opt/fastdfs/tracker/data-and-log`
    * 编辑配置文件 `vi /etc/fdfs/tracker.conf`

        ```shell
        base_path=/opt/fastdfs/tracker/data-and-log
        ```

    * 启动 tracker 服务  `/usr/bin/fdfs_trackerd /etc/fdfs/tracker.conf`
    * 重启 tracker 服务  `/usr/bin/fdfs_trackerd /etc/fdfs/tracker.conf restart`
    * 查看是否有 tracker 进程 `ps aux | grep tracker`

8. storage （存储节点）服务部署

    * 复制配置文件 `cp /etc/fdfs/storage.conf.sample /etc/fdfs/storage.conf`
    * 创建文件夹

        ```shell
        mkdir -p /opt/fastdfs/storage/data-and-log
        mkdir -p /opt/fastdfs/storage/images-data
        ```

    * 编辑配置文件 `vi /etc/fdfs/storage.conf`

        ```shell
        group_name=group1
        base_path=/opt/fastdfs/storage/data-and-log
        store_path0=/opt/fastdfs/storage/images-data
        tracker_server= 192.168.99.106:22122
        ```

    * 启动storage服务 `/usr/bin/fdfs_storaged /etc/fdfs/storage.conf`
    * 重启storage服务 `/usr/bin/fdfs_storaged /etc/fdfs/storage.conf restart`
    * 查看是否有storage进程 `ps aux | grep storage`

9. 测试是否部署成功

    * 复制配置文件 `cp /etc/fdfs/client.conf.sample /etc/fdfs/client.conf`
    * 创建目录 `mkdir -p /opt/fastdfs/client/data-and-log`
    * 编辑 `vi /etc/fdfs/client.conf`

        ```shell
        base_path=/opt/fastdfs/client/data-and-log
        tracker_server=192.168.99.106:22122
        ```

    * 上传图片 `/usr/bin/fdfs_test /etc/fdfs/client.conf upload /opt/test.jpg`
    * 查看图片地址 `http://192.168.99.106/group1/M00/00/00/wKhjal3SjIuAVBa9AAj4Ya88lJ0199_big.jpg`

10. 安装 fastdfs-nginx-module_v1.16.tar.gz

    * 解压 `tar zxvf fastdfs-nginx-module_v1.16.tar.gz`
    * 移动目录 `mv fastdfs-nginx-module/ /usr/program/fastdfs-5.05/`
    * 编辑配置文件 `vi /usr/program/fastdfs-5.05/fastdfs-nginx-module/src/config`

        ```shell
        CORE_INCS="$CORE_INCS /usr/include/fastdfs usr/include/fastcommon/"
        ```

    * 复制文件

        ```shell
        cp /usr/program/fastdfs-5.05/conf/http.conf /etc/fdfs
        cp /usr/program/fastdfs-5.05/conf/mime.types /etc/fdfs
        ```

11. 安装 Nginx 和 Nginx 第三方模块

    * 创建文件夹 `mkdir -p /usr/local/nginx /var/log/nginx /var/temp/nginx /var/lock/nginx /var/temp/nginx/client`
    * 解压 `tar zxvf nginx-1.8.1.tar.gz`
    * 移动目录 `mv nginx-1.8.1/ /usr/program/nginx-1.8.1`
    * 编译配置

        ```shell
        ./configure \
        --prefix=/usr/local/nginx \
        --pid-path=/var/local/nginx/nginx.pid \
        --lock-path=/var/lock/nginx/nginx.lock \
        --error-log-path=/var/log/nginx/error.log \
        --http-log-path=/var/log/nginx/access.log \
        --with-http_gzip_static_module \
        --http-client-body-temp-path=/var/temp/nginx/client \
        --http-proxy-temp-path=/var/temp/nginx/proxy \
        --http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
        --http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
        --http-scgi-temp-path=/var/temp/nginx/scgi \
        --add-module=/usr/program/fastdfs-5.05/fastdfs-nginx-module/src
        ```

    * 编译 `make`
    * 安装 `make install`
    * 复制配置文件 `cp /usr/program/fastdfs-5.05/fastdfs-nginx-module/src/mod_fastdfs.conf /etc/fdfs`
    * 创建目录 `mkdir -p /opt/fastdfs/fastdfs-nginx-module/data-and-log`
    * 编辑配置文件 `vi /etc/fdfs/mod_fastdfs.conf`

        ```shell
        base_path=/opt/fastdfs/fastdfs-nginx-module/data-and-log
        group_name=group1
        url_have_group_name = true
        tracker_server=192.168.99.106:22122
        store_path0=/opt/fastdfs/storage/images-data
        ```

    * 编辑nginx配置文件

    ```shell
    user  root;
    server {
        listen 80;
        server_name  192.168.99.106;
            location /group1/M00 {
                ngx_fastdfs_module;
            }
    }
    ```

    * 重启 `/usr/local/nginx/sbin/nginx -s reload`
