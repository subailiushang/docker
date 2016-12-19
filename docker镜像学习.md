##### 1. 获取镜像
镜像是Docker运行容器的前提。
*命令：docker pull NAME:[TAG]*
如果不指定标签TAG，默认下载最新版本的镜像。
例如：
![docker pull](http://upload-images.jianshu.io/upload_images/1708599-4f621ee9b4ffb509.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 实际上下载的是 httpd:latest镜像文件
* 行首的字母数字组合代表了各层文件的ID号（层是实现增量保存和更新的基础）

也可以选择从其他注册的服务器仓库进行下载
例如：

![docker pull](http://upload-images.jianshu.io/upload_images/1708599-dc693a682cf3ab58.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2. 查看镜像信息
*命令：docker images*

![docker images](http://upload-images.jianshu.io/upload_images/1708599-f1f9c43a274a167a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* REPOSUITORY：显示来自于哪个仓库
* TAG：显示镜像的标签
* IMAGE ID：显示镜像的ID号（唯一）
* 镜像创建时间
* 镜像大小

TAG信息用于标记来自同一仓库的不同镜像

![docker tag](http://upload-images.jianshu.io/upload_images/1708599-3e033db4db4e7422.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看到centos和centos-test的image id是一样的，说明实际上它们指向了同一个镜像文件，在这里相当于别名和快捷方式。

##### 3. 搜寻镜像文件
*命令：docker search NAME*

![docker search](http://upload-images.jianshu.io/upload_images/1708599-5d65cdb34bf9a47d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 4. 删除镜像
*命令：docker rmi*

![docker rmi](http://upload-images.jianshu.io/upload_images/1708599-c15a111a1e0a39f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当一个镜像拥有多个标签时，只是删除了当前的一个标签
当只剩下一个标签时，docker rmi将会删除当前镜像文件

##### 5. 创建镜像
* 基于已有的镜像的容器创建
* 基于本地模板导入
* 基于dockerfile创建

###### 5.1 基于已有镜像的容器i创建

运行一个centos镜像并且安装ifconfig命令：
*命令：docker run*
*参数：
-i ：标准输入
-t ：开启一个tty终端*

![docker run](http://upload-images.jianshu.io/upload_images/1708599-02685d61d67abfa1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

*命令：docker commit*
*参数：
-a 作者信息
-m 提交信息
-p 提交时暂停容器运行*

![docker commit](http://upload-images.jianshu.io/upload_images/1708599-2e9ab736c1eff6a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 5.2 基于本地模板导入
docker import
存出和载入镜像使用：
docker save
docker load

![docker save](http://upload-images.jianshu.io/upload_images/1708599-e10b0920ca4d5d8b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上传镜像使用：
docker push
需要注册相应的账号，相当于github的仓库管理平台