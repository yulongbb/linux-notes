# FastDFS

1. 拉取镜像 `docker pull morunchang/fastdfs`

2. 运行tracker `docker run -d --name tracker --net=host morunchang/fastdfs sh tracker.sh`

3. 运行storage `docker run -d --name storage --net=host -e TRACKER_IP=103.240.16.226:22122 -e GROUP_NAME=storagegroup morunchang/fastdfs sh storage.sh`

4. 修改配置

    * `docker exec -it storage  /bin/bash`
    * `vi /data/nginx/conf/nginx.conf`
    * 配置

        ```shell
        location /storagegroup/M00 {
        proxy_next_upstream http_502 http_504 error timeout invalid_header;
            proxy_cache http-cache;
            proxy_cache_valid  200 304 12h;
            proxy_cache_key $uri$is_args$args;
            proxy_pass http://fdfs_group1;
            expires 30d;
        }
        ```

    * 重启storage `docker restart storage`
