# HoshinoBot 搭配 go-cqhttp

项目地址：[HoshinoBot](https://github.com/Ice-Cirno/HoshinoBot)  [go-cqhttp](https://github.com/Mrs4s/go-cqhttp)

本文仅介绍如何使用docker-compose下使用Hoshino以及go-cqhttp,关于项目作用请前去项目地址中学习，顺便支持一下原作者们

## 直接使用

首先需要将文件取出

```bash
docker run --rm \
           -v ${PWD}:/tmp/Hoshino \
           pcrbot/hoshinobot \
           mv /HoshinoBot/ /tmp/Hoshino/Hoshino
```

```bash
docker run -it \
           -v ${PWD}/gocqhttp_data:/data \
           pcrbot/gocqhttp:ffmpeg
```

Hoshino文件夹以及gocqhttp_data文件夹下进行修改

~~不是很理解为啥docker-compose映射不出容器文件~~

#### Hoshino文件夹

修改文件夹`/Hoshino/hoshino/config`中的bot.py文件夹中

```pyhton
PORT = 8080
#HOST = '127.0.0.1'      # 注释掉此行
HOST = '0.0.0.0'      

DEBUG = False           # 调试模式

SUPERUSERS = [10000]    # 填写超级用户的QQ号，可填多个用半角逗号","隔开
NICKNAME = ''           # 机器人的昵称。呼叫昵称等同于@bot，可用元组配置多个昵称
```

#### gocqhttp_data

修改文件夹`/gocqhttp_data`中的config.yml文件，找到

```yml
servers:
  - ws-reverse:
      universal: ws://qqbot_hoshino_1:8080/ws/ #修改此项
      api: ws://your_websocket_api.server
      event: ws://your_websocket_event.server
      reconnect-interval: 3000
      middlewares:
        <<: *default 
```



修改完成之后即可使用`docker-compose up -d`启动容器，然后查看`gocqhttp_data`文件夹下的图片，并扫码登陆即可

### 进阶使用

~~由于某些原因~~仓库的镜像总是落后一个或者好几个版本，所以如果想用最新版本的hoshino或者go-cqhttp的话，可能需要自己打包

##### go-cqhttp

官方虽然没有提供官方镜像，但是提供了官方dockerfile，只需要clone go-cqhttp的最新源码，在go-cqhttp的文件夹中执行`docker build -t pcrbot/gocqhttp:ffmpeg .` 即可

##### Hoshinobot

Hoshino咖啡佬并没有给出过官方dockerfile，所以需要我们自己手写，我这边提供了一份我自己~~抄~~写的一份dockerfile，直接在有dockerfile的目录里clone Hoshino的源码，然后执行`docker build -t pcrbot/hoshinobot:latest .`即可

