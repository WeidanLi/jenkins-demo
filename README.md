该项目演示通过gitlab、Jenkins、maven、docker实现自动部署。

具体步骤如下：
1. 当gitlab的指定分支（比如：master分支）监听到有代码更新，通过设置webhook地址通知Jenkins。
2. Jenkins拉取gitlab-master分支的代码，联合maven中间件构建Docker镜像，上传到我们自己的DockerHub。
3. Jenkins构建完成（这时候镜像已经存储在我们的DockerHub上面了），连接到部署的机器，关闭老的项目，启动新的项目。

因为是在我自己的电脑上启动相对应的虚拟机进行实现，所以可以说一切从零开始搭建。观看教程的你如果中间哪一步企业已经构建完了，可以利用现有的环境进行稍加配置实现CI自动化部署。

## 一. 安装Gitlab环境

### 1. 使用Docker运行Gitlab环境：

```
sudo docker run --detach \
    --hostname gitlab.weidan.com \
    --publish 443:443 --publish 80:80 --publish 22:22 \
    --name gitlab \
    --restart always \
    --volume /srv/gitlab/config:/etc/gitlab \
    --volume /srv/gitlab/logs:/var/log/gitlab \
    --volume /srv/gitlab/data:/var/opt/gitlab \
    gitlab/gitlab-ce:latest
```

### 2. 增加防火墙规则

命令中看到需要几个端口，这时候需要再防火墙开放这几个端口以供Gitlab使用：

```
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=22/tcp --permanent
firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --reload
```

### 3. 修改本机hosts

修改本机hosts的方法不同系统是不同的，Windows是在C:/Windows/system32/drivers/etc/hosts，OSX是在/etc/hosts中。
按照我上面定义的hostname去添加，我这里因为ip是192.168.1.50，域名是gitlab.weidan.com
所以在hosts中增加`192.168.1.50 gitlab.weidan.com`即可

### 4. 配置项目



## 二. 安装Jenkins环境

## 三. 配置Jenkins环境






