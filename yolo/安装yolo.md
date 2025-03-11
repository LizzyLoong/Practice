# anaconda 
## 第一步：安装ubuntu主机系统或虚拟机系统   
## 第二部：安装Anaconda3   
在清华源网址下载Anaconda3-2021.11-Linux-x86_64.sh   
【清华源】https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/    
Ctrl+F Anaconda3-2021.11-Linux-x86_64.sh   
点击直接下载   
下载好后运行sh文件，首先chmod加权限，然后直接运行   
运行过程中，一路回车即可，有需要输入yes或no的直接输入yes。   
安装过程中只需要关注一下安装路径。默认的安装路径是/home/<Username>/anaconda3，这个路径是可以的。 
这里的<Username>指你的用户名。  
一路安装即可。   
## 第三部：环境配置
```sudo vim ~/.bashrc```
在文件末尾添加如下内容
```export PATH="/home/<Username>/anaconda3/bin:$PATH"```
这里需要把<Username>替换成你的用户名
我就是
```export PATH="/home/lizzy/anaconda3/bin:$PATH"```
保存后退出
然后输入
```source ~/.bashrc```
更新下环境
然后输入```conda list```，检查是否下载完成
有包名，则表示下载完成。
## 第四步：切换镜像
由于annaconda自带的下载工具pip默认使用的是外网的网址，接下来需要对其网址进行更新，用我们国的自带的网址，这样使用conda pip就非常快
```pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple```
由于annaconda也自带的conda工具默认使用的是外网的网址，我们也需要对其进行配置，方便接下来的环境管理与使用
```
conda clean -i
sudo vim ~/.condarc
```
进入配置文件后，直接用下面的配置信息进行替换
```
channels:
 - defaults
show_channel_urls: true
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
 pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
 simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```
输入conda安装第三方包测试：
```conda install scrapy```
测试时间比较长，大概3min
## 第五部：创建虚拟环境
```
conda create -n <环境名称自定义> python=<python的版本号>
```
例如：
```
conda create -n My_torch python=3.10
```
输入后回车，然后
```
source activate My_torch
```
## 第六步：finish
启用虚拟环境
```
conda activate <自定义的环境名称>
```
例如：
```
conda activate My_torch
```


# yolo
## 1.安装PyTorch
在linux中打开火狐浏览器里输入pytorch官网用来获取下载指令
【Pytorch官网】https://pytorch.org/
打开网站后往下拉就会有，
选择pip版本，选择cpu版本，下面得到安装命令
```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```
## 2.下载yolo
https://gitee.com/monkeycc/yolov5   
下载zip
解压到桌面下，并从终端进入文件夹
source ~/.bashrc
输入指令进入环境：
```
conda activate <你的环境>
```
例如我的：
```
conda activate My_torch
```
使用指令用清华源安装需要的环境：
```
pip install -U -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```
## 3.测试
通过VSCode打开yolo解压文件夹，
打开detect.py文件
设置python解释器，选择My_torch
点击运行，可以看到输出













# yoloV11
https://blog.csdn.net/StopAndGoyyy/article/details/143169639
https://github.com/ultralytics/ultralytics