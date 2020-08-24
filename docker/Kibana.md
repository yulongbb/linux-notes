# Kibana

1. 创建网络 `docker network create elastic-network`

2. 拉取镜像 `docker pull kibana`

3. 启动镜像 `docker run -d --rm -p 5601:5601  --net elastic-network  --link elasticsearch:elasticsearch -e ELASTICSEARCH_URL=http://elasticsearch:9200 --name kibana kibana`
