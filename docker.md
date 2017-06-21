# 视频

- `sudo docker info` 查看docker信息
- ` docker --help `查看docker命令
- ` systemctl start docer` 启动docker

## 更改服务器地址

阿里云账号：wuwenchihdu

```
vi /etc/systemd/system/multi-user.target.wants/docker.service
```

找到

```
--registry-mirror=https://knpfug6n.mirror.aliyuncs.com
```

再重载和重启docker：

```
systemctl daemon-reload
systemctl restart docker
也可以
在 /etc/default/docker 中加入：
DOCKER_OPTS="--registry-mirror=https://knpfug6n.mirror.aliyuncs.com"
server docker restart
```

## 命令

- `docker images`	查看所有镜像。
- `docker rmi 镜像名称` 删除某个镜像。多个镜像的时候，镜像之间使用空格。
- `  docker run --name 容器名称 -d -p 本地端口:容器端口 镜像名称  ` 运行一个镜像，-d 表示后台运行，-p 表示端口间的绑定映射
- `docker ps -a`查看所有正在运行的容器。
- `docker exec -it 容器名称 /bin/bash` 使用bash进入容器里。
- `exit`退出容器
- `docker rm -f 容器名称` 停止一个容器