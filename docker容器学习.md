容器是镜像的一个运行实例，但是它带有额外的可写文件层。

##### 1. 创建容器

Docker的容器十分的轻量级，用户可以随时创建和删除容器

docker create命令新建一个容器，例如：

![docker create](http://upload-images.jianshu.io/upload_images/1708599-172697af26f3155d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

docker create命令新建的容器处于停止状态，需要使用docker start命令来启动

![docker start](http://upload-images.jianshu.io/upload_images/1708599-450c5b17ec9798e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

docker ps -a 查看容器的ID

![docker ps -a](http://upload-images.jianshu.io/upload_images/1708599-00cc8540b06a2bea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

新建并启动容器：
docker run -it 

![docker run](http://upload-images.jianshu.io/upload_images/1708599-2975ed4fe8cb238e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

守护态运行需要加入参数-d

![docker run -idt](http://upload-images.jianshu.io/upload_images/1708599-8d16f1c4dcfb782a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 2. 终止容器

docker stop +容器ID
docker ps -a查看容器ID

##### 3. 进入容器
attach命令

![docker attach](http://upload-images.jianshu.io/upload_images/1708599-ba448766425e5692.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

exec命令

![docker exec -it](http://upload-images.jianshu.io/upload_images/1708599-0402d4052f8d8bc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 4. 删除容器

docker rm产出一个处于停止状态的容器

##### 5. 导入和到处容器

docker export

![docker export](http://upload-images.jianshu.io/upload_images/1708599-86059de2e80d7aaf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

docker input

![docker input](http://upload-images.jianshu.io/upload_images/1708599-c2cbc065bcec1a19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)