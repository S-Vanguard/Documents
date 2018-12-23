# 升级内核
[Linux：Centos7升级内核](https://www.tesun.net/centos7sheng-ji-nei-he/)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223230853959.png)  

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223231211350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)  
安装完成后把最新版本内核设为默认内核    
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223231508123.png)

# 安装docker
[cnetos7 安装 docker17.03.2](http://www.cnblogs.com/freefei/p/9263998.html)  

配置源  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223232221857.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

安装最新版本  

# docker基本操作
## 检查docker版本
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234148356.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)
## 运行镜像
运行hello world示例。这里我们本地没有hello world的docker，于是docker被拉取下来并部署  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223233751688.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)  
运行ubuntu docker  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234456876.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)  
## 显示本地镜像库内容
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234553149.png)  
## 获得帮助
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234631799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)
## 显示容器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223234818717.png)  
上面是显示运行中的容器，加上-a参数后将显示所有容器，包括已终止的。  
## 继续运行元容器并进入
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223235202199.png)

## 拉取MySQL镜像
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181223235518453.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

# 构建docker镜像练习
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

# MySQL与容器化
启动MySQL服务器：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224000354374.png)

运行MySQL客户端  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224002758239.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

进行数据库操作  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224003002940.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

创建卷并挂载  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224004319566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

# 自动编排容器
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
# docker网络
查看网络  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224011538832.png)

备制支持ifconfig和ping命令的ubuntu容器  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224012012110.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01yZml2ZTU1NQ==,size_16,color_FFFFFF,t_70)

由容器制作镜像  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018122401234773.png)

## 创建网络
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224012648513.png)

## 连通性检测
两个容器可以互相ping通  
u1 ping u2  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014404975.png)  

u2 ping u1  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014337376.png)  

断开网络后，二者就不能再连通了  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014615327.png)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181224014559762.png)  
