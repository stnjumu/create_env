# extention packages for env

此文件夹中为独立的python包，按需安装。

添加包命令
conda env update --file local.yml # 添加某些包而改动配置文件后更新环境，需先激活环境
conda env update --name myenv --file local.yml # 同上，但无需激活环境