# image-recognition

本项目用来演示在树莓派进行图像的识别

## 安装方法

在树莓派上运行

curl -s https://raw.githubusercontent.com/flyingtimes/image-recognition/master/one_step_install.sh|bash

这是一个脚本，会自动帮你把源代码下载下来，如果没有安装docker，会自动安装docker，并下载相关的docker镜像。tensorflow所需的所有组件都已经在docker中预先准备好了，您只要运行程序就行了
#### 注意，由于这个docker镜像是armv7专用的，因此在其他x86机器上运行是不行的

## 运行程序

bash imgdetect.sh  [你的图片文件名]

#### imgdetect.sh脚本说明：
docker run -it -v $PWD:/images clarkchan/rpi-tensorflow-imagenet python /images/classify_image.py --image_file=/images/$1 --num_top_predictions=1

	-v $PWD:/images 将本路径映射到镜像里面的/images目录下
	clarkchan/rpi-tensorflow-imagenet  运行的镜像名称
	python /images/classify_image.py   在镜像中运行classify_image.py
	--image_file=/images/$1            要处理的图片文件名,文件名从命令行获取
	--num_top_predictions=1            返回可能性最大的‘1’个推测结果

#### build_docker目录说明：
这个文件夹是用来创建docker镜像文件本身的，如果仅仅是使用这个镜像文件来开发python程序，则可以忽略这个文件夹，直接从dockerhub上下载镜像就足够用了

这里面有两个镜像，一个是rpi-tensorflow, 这是一个基础文件镜像，包含了rpi版本的ubuntu，还有tensorflow安装程序；另外一个是rpi-tensorflow-imagenet,这个在rpi-tensorflow基础上，增加了将结果转换为中文的translation插件，以及将谷歌最新训练好的模型预先放置到tmp目录下面。