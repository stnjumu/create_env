# Create_env 环境管理

此项目用于总结用到的conda环境，目前有

~~~python
python_all_310 # python=3.10 常用环境，尽可能安装所有可能用到的包。
pytorch_36 # pytorch python=3.6，pytorch稳定环境，pytorch框架推荐使用。
~~~

命名规则：全小写，使用下划线分隔，数字表示python版本，.符号可省略
  但多个复杂的版本号时不推荐省略，如：mmdet

## 使用方法

可使用

~~~anaconda
conda env create -f environment.yml # 由.yml文件创建环境
conda env export | grep -v "^prefix: " > environment.yml # 导出环境至.yml文件，但此命令导出的yml文件中包非常多，依赖的包都在
# 以下3句未测试使用过，https://qastack.cn/programming/42352841/how-to-update-an-existing-conda-environment-with-a-yml-file
conda env update --file local.yml # 添加某些包而改动配置文件后更新环境，需先激活环境
conda env update --name myenv --file local.yml # 同上，但无需激活环境
conda env update -f local.yml --prune # 改动配置文件后更新环境，--prune标志移除这个local.yml中不存在的包

pip install -i requirements.txt
~~~

一键部署环境。

注意：多个库版本要求的项目不适合一键部署环境，
例如：在pytorch, cudatoolkit, torchvision等版本的对应上，这个推荐按照pytorch官网安装
例如：mmdet, mmcv, CUDA, pytorch四者版本都需对应，推荐按照ObjectDetection/mmdet/下步骤安装。
## 解析

例如：

~~~anaconda
name: pytorch_36
channels:
- pytorch
- defaults
dependencies:
- python=3.6
- pytorch=1.4.0
- scipy
- numpy
- pandas
- matplotlib
- pip
- pip:
  - dominate==2.4.0
  - torchvision==0.5.0
  - Pillow==6.1.0
  - visdom==0.1.8
~~~

中嵌套使用了pip安装

~~~anaconda
  - dominate==2.4.0
  - torchvision==0.5.0
  - Pillow==6.1.0
  - visdom==0.1.8
~~~

注意pytorch+Pillow有些坑，最好这样安装。。。

## conda或pip安装太慢怎么办？

[Anaconda国内镜像汇总（conda & pip）](https://blog.csdn.net/qq_326324545/article/details/121288800 "提示信息文本")

下面亲测有效：

anaconda命令行输入
```conda config```
生成.condarc文件，位置~/.condarc
找不到该文件的可以conda info看看"user config file"的路径

将下面复制到该文件即可：

~~~
# This is a sample .condarc file.
# It adds mirror-channel(Tsinghua University) of anaconda and enables
# the show_channel_urls option.
 
# channel locations. These override conda defaults, i.e., conda will
# search *only* the channels listed here, in the order given.
# Use "defaults" to automatically include all default channels.
# Non-url channels will be interpreted as Anaconda.org usernames
# (this can be changed by modifying the channel_alias key; see below).
# The default is just 'defaults'.
channels:
  - defaults
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
 
# Show channel URLs when displaying what is going to be downloaded
# and in 'conda list'. The default is False.
show_channel_urls: true
 
# For more information about this file see:
# https://conda.io/docs/user-guide/configuration/use-condarc.html
~~~

## 注意事项

### Windows安装

windows下如果使用Anaconda Prompt中进入conda环境中使用pip安装包，会错误地安装在base环境中，请使用vscode地powershell终端进入conda环境再使用pip安装，会直接安装到该conda环境中。

另外，我的PC使用pip需要关闭代理，笔记本使用pip却需要打开代理，奇怪。
