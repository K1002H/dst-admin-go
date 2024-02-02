# Deployment/部署
注意目录必须要有读写权限

### 脚本一键部署
[点击下载文件](https://github.com/hujinbo23/dst-admin-go/blob/main/docs/install/%E4%B8%80%E9%94%AE%E9%83%A8%E7%BD%B2%E8%84%9A%E6%9C%ACv4.6%E7%89%88%E6%9C%AC.sh.x)

### 二进制部署
请下载最新的release版本

[部署教程](https://blog.csdn.net/Dig_hoof/article/details/131296762)

[视频教程](https://www.bilibili.com/read/cv25125509)

### docker 部署

**第一次启动时会自动下载steamcmd和饥荒服务器，请耐心等待10-20分钟，你也可以使用挂载路径避免下载，可本地搭建使用wireguard与云组网为入口，自行进入容器设置wireguard配置文件**

```
docker pull k1002h/dst-admin-go:1.2.8
docker run -d \
    --name dst-admin-go \
    --cap-add=NET_ADMIN \
    --cap-add=NET_RAW \
    --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
    --restart Unless Stopped \
    -v $(pwd)/map:/root/.klei/DoNotStarveTogether \
    -p 8082:8082 \
    k1002h/dst-admin-go:1.2.8
```

***主机模式***

```
docker pull k1002h/dst-admin-go:1.2.8
docker run -d \
    --name dst-admin-go \
    --cap-add=NET_ADMIN \
    --cap-add=NET_RAW \
    --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
    --restart Unless Stopped \
    -v $(pwd)/map:/root/.klei/DoNotStarveTogether \
    --net=host \
    k1002h/dst-admin-go:1.2.8
```

**多房间版本 萌新勿用**

目前多房间版本，默认以**32位**启动，不提供steamcmd和饥荒服务器安装，需要自己手动安装
同时相比较普通版本缺少宕机自动恢复，自动更新，定时任务等（有时间在迁移过来）

+ steamcmd 请填写 /app/steamcmd
+ 饥荒路径填写 /app/dst-dedicated-server

```
docker pull hujinbo23/dst-admin-go:home.1.0.2
docker run -d -p8082:8083 hujinbo23/dst-admin-go:home.1.0.2
```
