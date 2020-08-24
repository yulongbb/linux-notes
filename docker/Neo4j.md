# Neo4j

1. 拉取镜像 `docker pull neo4j`

2. 启动镜像 `docker run --name neo4j -d -p 7474:7474 -p 7687:7687 --volume=$HOME/neo4j/data:/data  neo4j`
