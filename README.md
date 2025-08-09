# README

## 1. 登录阿里云 Container Registry
```shell
$ docker login --username=yao****@aliyun.com registry.cn-hangzhou.aliyuncs.com
```
用于登录的用户名为阿里云账号全名，密码为开通服务时设置的密码。

您可以在访问凭证页面修改凭证密码。

注意：使用 RAM 用户（子账号）登录镜像仓库时，不支持企业别名带有英文半角句号（.）。

## 2. 从Registry中拉取镜像
```shell
$ docker pull registry.cn-hangzhou.aliyuncs.com/yao3060/wordpress:[镜像版本号]
```

## 3. 将镜像推送到Registry
```shell
$ docker login --username=yao****@aliyun.com registry.cn-hangzhou.aliyuncs.com
$ docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/yao3060/wordpress:[镜像版本号]
$ docker push registry.cn-hangzhou.aliyuncs.com/yao3060/wordpress:[镜像版本号]
```
请根据实际镜像信息替换示例中的[ImageId]和[镜像版本号]参数。

## 4. 选择合适的镜像仓库地址
从ECS推送镜像时，可以选择使用镜像仓库内网地址。推送速度将得到提升并且将不会损耗您的公网流量。

如果您使用的机器位于VPC网络，请使用 registry-vpc.cn-hangzhou.aliyuncs.com 作为Registry的域名登录。

## 5. 示例
使用"docker tag"命令重命名镜像，并将它通过专有网络地址推送至Registry。
```shell
$ docker images
REPOSITORY                                                         TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
registry.aliyuncs.com/acs/agent                                    0.7-dfb6816         37bb9c63c8b2        7 days ago          37.89 MB
$ docker tag 37bb9c63c8b2 registry-vpc.cn-hangzhou.aliyuncs.com/acs/agent:0.7-dfb6816
```
使用 "docker push" 命令将该镜像推送至远程。
```shell
$ docker push registry-vpc.cn-hangzhou.aliyuncs.com/acs/agent:0.7-dfb6816
```
