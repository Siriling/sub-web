# Sub-web

# 目录

[一、简介](https://github.com/Siriling/dockerfiles/tree/main/subconverter#一简介)

[二、展示](https://github.com/Siriling/dockerfiles/tree/main/subconverter#二展示)

[三、使用](https://github.com/Siriling/dockerfiles/blob/main/subconverter/三使用)

[四、Nginx反向代理配置](https://github.com/Siriling/dockerfiles/tree/main/subconverter#四nginx反向代理配置)

[五、仓库地址](https://github.com/Siriling/dockerfiles/tree/main/subconverter#五仓库信息)

# 一、简介

一个订阅转换网站

- 前端：基于[CareyWang/sub-web](https://github.com/CareyWang/sub-web)前端实现的订阅地址拼接
- 后端：基于[tindy2013/subconverter](https://github.com/tindy2013/subconverter)后端实现的配置自动生成

# 二、展示

[https://sub.siriling.com:81](https://sub.siriling.com:81/)

## 功能说明

### 基础模式

- 使用的是我自定义的订阅配置文件，[点击查看](https://raw.githubusercontent.com/Siriling/sub-web/main/public/config/diy-rules2.ini)
- 使用的是我的远程后端程序

### 进阶模式

可自己选择**后端程序**和**订阅配置文件**

# 三、使用

## Docker部署

**如果需要SubConverter前后端整合+短链接，请使用docker compose进行部署，[点击查看](https://github.com/Siriling/dockerfiles/tree/main/subconverter)**

### docker

- 修改网站名称：添加`-e SITE_NAME='订阅转换'`
- 修改后端API：添加`-e API_URL='https://sub.siriling.com:81'`
- 修改短链接网站路径：根据需求自行修改`conf/config.js`中的相关配置
- subconverter挂载外部配置文件：参考容器内部路径:`/base/snippets/rulesets.txt`

```
docker run -d \
  --name subconverter \
  --restart=unless-stopped \
  --net='bridge' \
  -p 8080:80 \
  -p 25500:25500 \
  -v /root/appdata/subconverter/conf:/usr/share/nginx/html/conf \
  siriling/subconverter:latest
```

### docker compose

- 文件下载：[docker-compose.yml](https://raw.githubusercontent.com/Siriling/dockerfiles/main/subconverter/docker-compose.yml)
- 修改`MYURLS_DOMAIN`为你的域名
- 修改`MYURLS_TTL`为短链接有效期（单位：天）
- 修改`MYURLS_REDIS`为自己Redis链接（`IP:端口`）

```
docker-compose up -d
```

## 服务器部署

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

浏览器访问：http://localhost:8080

```shell
yarn serve
```

### 服务器上线发布

把网站发布到服务器，你需要把程序打包，执行以下打包命令，生成的dist目录即为打包后的文件目录

- 如需修改默认后端，请修改`src/views/Subconverter.vue`中`defaultBackend`配置项

```shell
yarn build
```

[四、Nginx反向代理配置](https://github.com/Siriling/dockerfiles/tree/main/subconverter#四nginx反向代理配置)

# 四、Nginx反向代理配置

Sub-web访问短链接出现跨域问题，需要在Nginx里修改，参考[myurls.conf](https://raw.githubusercontent.com/Siriling/dockerfiles/main/subconverter/myurls.conf)

```
location /{
 #...
 add_header Access-Control-Allow-Origin *;
 #...
}
```

# 五、仓库地址

- GitHub：[Siriling/sub-web](https://github.com/Siriling/sub-web)
- Docker：[siriling/subconverter](https://hub.docker.com/r/siriling/subconverter)
