# Sub-web

## 简介

一个订阅转换网站

## 说明

- 前端：基于[CareyWang/sub-web](https://github.com/CareyWang/sub-web)前端实现的订阅地址拼接
- 后端：基于[tindy2013/subconverter](https://github.com/tindy2013/subconverter)后端实现的配置自动生成

## 使用

## Docker运行

```shell
docker run -d -p 58080:80 --restart always --name subweb careywong/subweb:latest
```

自定义构建Docker镜像

- 注：每次修改代码，你都需要重新执行 docker build 来执行打包操作

```shell
docker build -t subweb-local:latest .

docker run -d -p 58080:80 --restart always --name subweb subweb-local:latest
```

## 服务器运行

需要安装[Node](https://nodejs.org/zh-cn/)和[Yarn](https://legacy.yarnpkg.com/en/docs/install)来安装依赖与打包发布。你可以通过以下命令查看是否安装成功。

```shell
node -v
yarn -v
```

### 安装依赖

```shell
yarn install
```

### 本地运行服务

浏览器访问<http://localhost:8080>

```shell
yarn serve
```

### 服务器上线发布

把网站发布到服务器，你需要把程序打包，执行以下打包命令，生成的dist目录即为打包后的文件目录

- 如需修改默认后端，请修改`src/views/Subconverter.vue`中`defaultBackend`配置项

```shell
yarn build
```

## 功能

### 基础模式

- 使用的是我自定义的订阅配置文件，[点击查看](https://raw.githubusercontent.com/Siriling/sub-web/main/public/config/diy-rules2.ini)
- 使用的是我的远程后端程序

### 进阶模式

可自己选择**后端程序**和**订阅配置文件**

## 自定义网站

按照需求修改项目路径下的`.env`文件
