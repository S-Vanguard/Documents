@[toc]
# 基础操作
## 升级内核
[Linux：Centos7升级内核](https://www.tesun.net/centos7sheng-ji-nei-he/)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223230853959.png)  

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223231211350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)  
安装完成后把最新版本内核设为默认内核    
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223231508123.png)

## 安装docker
[cnetos7 安装 docker17.03.2](http://www.cnblogs.com/freefei/p/9263998.html)  

配置源  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223232221857.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

安装最新版本  

## docker基本操作
### 检查docker版本
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234148356.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)
### 运行镜像
运行hello world示例。这里我们本地没有hello world的docker，于是docker被拉取下来并部署  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223233751688.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)  
运行ubuntu docker  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234456876.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)  
### 显示本地镜像库内容
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234553149.png)  
### 获得帮助
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234631799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)
### 显示容器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234818717.png)  
上面是显示运行中的容器，加上-a参数后将显示所有容器，包括已终止的。  
### 继续运行元容器并进入
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223235202199.png)

### 拉取MySQL镜像
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223235518453.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

## 构建docker镜像练习
创建一个新文件夹，创建一个dockerfile,并写入以下内容
```
FROM ubuntu
ENTRYPOINT ["top", "-b"]
CMD ["-c"]
```
构建镜像  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223235818968.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

运行镜像  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224000020269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

## MySQL与容器化
启动MySQL服务器：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224000354374.png)

运行MySQL客户端  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224002758239.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

进行数据库操作  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224003002940.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

创建卷并挂载  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224004319566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

## 自动编排容器
下载docker-compose
```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.17.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224005011173.png)

编写stack.yml编排文件  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224005559112.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

运行```docker-compose -f stack.yml up```开始自动部署  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224013840298.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

部署成功  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224013943486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

新部署的容器  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014053705.png)
## docker网络
查看网络  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224011538832.png)

备制支持ifconfig和ping命令的ubuntu容器  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224012012110.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

由容器制作镜像  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018122401234773.png)

### 创建网络
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224012648513.png)

### 连通性检测
两个容器可以互相ping通  
u1 ping u2  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014404975.png)  

u2 ping u1  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014337376.png)  

断开网络后，二者就不能再连通了  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014615327.png)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014559762.png)  
# 实战
在我们的项目中，运行的代码被分配到三个docker中：静态文件服务器，后端服务器，数据库服务器。
- 静态文件服务器：负责前端网页部分的传输
- 后端服务器：处理查询请求
- 数据库服务器：保存后端数据
## 创建静态文件服务器docker
dockerfile文件
```
FROM node:8

# Create app directory
RUN mkdir -p /home/swapi
WORKDIR /home/swapi

# Bundle app source
COPY . /home/swapi
RUN npm install

EXPOSE 8888
# CMD [ "npm", "start" ]
CMD ["node", "bin/index.js", "8888", "http://192.168.134.129:8080"]
```
这个容器是一个继承自node:8的容器，然后在容器内创建一个```/home/swapi```的文件夹，并把工作区转移到这里。接下来，我们使用```COPY```命令把前端文件从本机拷贝到docker内。  
这些安装工作完成后，```EXPOSE 8888```命令把容器的8888对外暴露出来，提供访问服务。最后一句```CMD```语句的作用是在docker内运行一个node服务器，提供静态文件服务器。
## 创建后端服务器docker
```
# Use an official Golang runtime as a parent image
FROM golang:latest

# Make the working directory
RUN mkdir -p go/src/server

# Set the working directory to /go/src/server
WORKDIR /go/src/server

# Copy the current directory contents into the container at /go/src/server
COPY . /go/src/server

# Get all packets and install
RUN go get -u -v 
RUN go install -v

# Make port 8080 available to the world outside this container
EXPOSE 8080

CMD server run
```
后端的部署与静态文件部署类似，但有一点不同的是，静态文件服务器继承的是node容器，后端容器继承的是golang的容器。布置的过程类似，同样是按照新建文件夹，复制文件，构建文件，暴露端口，运行服务器的顺序进行。  
部署过程：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224101452204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)
## 创建数据库docker
```
FROM mysql:5.7.21

#设置登录密码
ENV MYSQL_ROOT_PASSWORD 123456
#定义工作目录
ENV WORK_PATH /opt/starWar
#定义会被容器自动执行的目录
ENV AUTO_RUN_DIR /docker-entrypoint-initdb.d

# 创建文件夹
RUN mkdir -p $WORK_PATH

#将所需文件放到容器中
COPY starWar.sql $WORK_PATH/
COPY setup.sh $AUTO_RUN_DIR/

#给执行文件增加可执行权限
RUN bash $AUTO_RUN_DIR/setup.sh
```
数据库docker的部署比前面两个稍微复制一些。数据库docker使用的是MySQL数据库，其中部署的时候需要配置一些环境参数，如MySQL登陆密码，WORK_PATH目录等。最后运行一个setup的脚本文件开启MySQL服务器。  
setup.sh文件如下
```bash
mysql -uroot -p$MYSQL_ROOT_PASSWORD &
source $WORK_PATH/starWar.sql;
service start mysql
```
## 自动编排docker
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224102555802.png)
## 部署结果
制备好上面三个部分的docker  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224102509639.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)  
服务都已开启  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224101903639.png)  

在外部访问网页  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224102538789.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)   
进行api查询  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224103428489.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)   
