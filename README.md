# 一个自用docker-compose文件说明

首先你会需要一个docker,以及会需要一个docker-compose

```shell
curl -sSL https://get.docker.com/ | sh
```

安装好docker以后，开始安装docker-compose

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

```shell
sudo chmod +x /usr/local/bin/docker-compose
```

或者有python的可以更加快速一点

```shell
pip install docker-compose
```

准备完成好后，可以参见文件夹中的readme和docker-compose.yml中的文件说明了