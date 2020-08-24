# ElasticSearch

1. 拉取镜像 `docker pull elasticsearch`

2. 启动镜像 `docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch`
