# mage
一个基于 `docker` 的 `go-kratos` 本地开发运行环境。


## 使用
### 1. 按需修改 .env 配置
- 按需修改或添加其他服务配置

### 2.启动服务
- 启动全部服务
```bash
docker-compose up -d
```
- 按需启动部分服务
```bash
docker-compose up -d etcd golang mysql redis
```

### 3.运行代码
将项目代码放置 `CODE_PATH_HOST` 指定的本机目录，进入 `golang` 容器，运行项目代码。
~~~bash
docker exec -it mage_golang_1 bash
~~~