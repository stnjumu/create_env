# FNA - 目标检测NAS

原项目地址：

https://github.com/JaminFong/FNA


fork项目地址：
https://github.com/stnjumu/FNA_copy


环境配置参考：不能直接使用pip安装，会报各种错误
https://zhuanlan.zhihu.com/p/219774377

下面以Anaconda为例(也可以在docker里面使用Anaconda去配置)

conda create -n fna python=3.7

conda init

重启shell

conda activate fna

conda install pytorch=1.1 cudatoolkit=10.0 torchvision -c pytorch

pip install Cython

git clone https://github.com/open-mmlab/mmcv.git

cd mmcv/

git reset --hard e5ca884

python setup.py install

cd ..

git clone https://github.com/open-mmlab/mmdetection.git

cd mmdection/

git reset --hard 53c647e

PYTHON=python3 ./compile

python3 setup.py install

cd ..

安装完毕。

可以conda list检查一下mmcv和mmdetection的版本

解决配置过程中的一些error:

ImportError: libGL.so.1: cannot open shared object file: No such file or directory

apt update

apt install -y libgl1-mesa-dev

ImportError: libgthread-2.0.so.0: cannot open shared object file: No such file or directory

apt install libglib2.0-dev