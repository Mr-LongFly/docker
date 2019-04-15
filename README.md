# 构建ssr+gost的docker镜像
构建步骤：
1.在服务器上新建一个文件夹
2.进入创建文件夹
3.下载好Dockerfile文件(gost.json和shadowsocks.json可自己编写)
使用docker的构建命令：docker build --no-cache -t 31891692/ssr:ssr-gost .
  31891692：为远程仓库名
  ssr:ssr-gost:镜像名:标签

# 嫌麻烦可以使用我的镜像
下载命令：docker pull 31891692/ssr:ssr-gost

# 镜像使用步骤
1.下载
2.编写gost.json和shadowsocks.json文件
3.启动容器：docker run -itd --name ssr -p 8080:8080 -p 8080:8080/udp 31891692/ssr:ssr-gost
