# ElasticSearch

1. 创建网络 `docker network create elastic-network`

2. 拉取镜像 `docker pull elasticsearch`

3. 启动镜像 `docker run -d --name elasticsearch  --net elastic-network  -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch`
