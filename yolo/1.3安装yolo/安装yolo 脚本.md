大家好，这期视频给大家展示YOLO的安装
打开ubuntu 首先安装anaconda


在哪里下载都可以
这里选择清华园镜像

下载好后运行sh脚本
首先给脚本加权限
然后才能运行
运行过程中，一路回车即可，有需要输入yes或no的直接输入yes。   
安装过程中只需要关注一下安装路径。默认的安装路径是/home/<Username>/anaconda3，这个路径是可以的。 
这里的<Username>指你的用户名。  

安装完成后我们需要来配置一下环境
sudo vim ~/.bashrc
在文件末尾添加如下内容
export PATH="/home/<Username>/anaconda3/bin:$PATH"
这里需要把<Username>替换成你的用户名



保存后退出
然后输入
source ~/.bashrc
更新下环境
然后输入conda list，检查是否下载完成
有包名，则表示下载完成。



配置完环境，我们需要创建虚拟环境
conda create -n <环境名称自定义> python=<python的版本号>
例如：
conda create -n My_torch python=3.10
输入后回车，然后
source activate My_torch


现在来安装pytorch
输入pytorch官网用来获取下载指令
打开网站后往下拉就会有 选择pip版本
选择cpu版本 然后得到安装命令





然后安装yolo
在git上搜索yolo，选择任意版本下载
这里为了方便测试，我使用yolo v5


输入指令进入环境：
conda activate <你的环境>
例如我的：
conda activate My_torch
使用指令用清华源安装需要的环境：
pip install -U -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
最后进行测试
通过VSCode打开yolo解压文件夹，
打开detect.py文件
设置python解释器，选择My_torch
点击运行，可以看到输出
测试运行的运行结果在该文件夹下的runs文件夹下，可进行查看