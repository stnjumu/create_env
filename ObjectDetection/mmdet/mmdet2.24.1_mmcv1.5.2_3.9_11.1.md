2022.5.31尝试安装最新版的mmdet
新版本附带了很多常用分析脚本

# 创建环境
conda create -n mmdet2.24.1_mmcv1.5.2_3.9_11.1 python=3.9 -y
conda activate mmdet2.24.1_mmcv1.5.2_3.9_11.1
# 安装pytorch
conda install pytorch==1.10.0 torchvision==0.11.0 torchaudio==0.10.0 cudatoolkit=11.1 -c pytorch -c conda-forge
# 安装mmcv
pip install mmcv-full==1.5.2 -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.10.0/index.html

# 安装mmdet
# 需要新建项目文件夹
git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
git reset --hard 73b4e65    # 回退版本到v2.24.1
pip install -r requirements/build.txt   # 安装依赖
pip install -v -e .  # or "python setup.py develop"   # 编译并安装mmdet，dev开发模式
# 注：python setup.py install会安装到python环境中，并删除mmdet文件
# python setup.py develop是dev模式，python环境中的mmdet包只是链接到本地的mmdet文件，修改本地文件即修改mmdet库；