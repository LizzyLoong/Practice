# 在Lichee Pi 4A上运行 Bastion

## 实验准备

请参考 WPS 运行中的硬件准备和软件准备，完成系统烧录

### 软件环境准备

安装完成后，就可以在荔枝派上连接好显示屏启动游戏啦ヾ(≧▽≦*)o

#### 1. 二进制翻译软件

```shell
sudo apt update

sudo apt install net-tools		# 默认安装了
sudo apt install git			# 未默认安装
sudo apt install ssh openssh-server

# ifconfig
ip addr show

# Tip: VSCode 不支持对 RISCV 架构的远程 所以通过 ssh 完成

# 为运行 X86 软件进行翻译准备  安装 Box64
git clone https://github.com/ptitSeb/box64.git
cd box64
mkdir build
cd build
cmake .. -D RV64=1 -D CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install -j$(nproc)

# 把 Box64 更新到系统变量中
vim ~/.bashrc

# 把该内容写到 .bashrc 文件的最后一行
export PATH=$PATH:/home/sipeed/box64/build

# 在命令行刷新 .bashrc 文件
source ./bashrc
```



#### 2. 嵌入式设备的 openGL 支持

[ptitSeb/gl4es: GL4ES is a OpenGL 2.1/1.5 to GL ES 2.0/1.1 translation library, with support for Pandora, ODroid, OrangePI, CHIP, Raspberry PI, Android, Emscripten and AmigaOS4. (github.com)](https://github.com/ptitSeb/gl4es) 

```shell
git clone https://github.com/ptitSeb/gl4es.git
cd gl4es
mkdir build
cd build
cmake .. -D CMAKE_BUILD_TYPE=RelWithDebInfo
make -j4

# 在安装过程中可能出现 fatal error: X11/Xlib.h: 没有那个文件或目录 的报错
# 因为目前的荔枝派没有默认安装 X11 库
# X11 是Unix系统上的窗口系统，它提供图形用户界面的支持

sudo apt-get install libx11-dev

# 安装好后重新编译 gl4es 即可
```



### 游戏执行
#### 1.游戏应用包下载链接
[link] https://archive.org/details/kingdom-rush-bonus-v-5.6.12-gog-linux-v-52189-gui  
下载7-zip版本
##### 2.解压压缩包
解压压缩包后，生成的文件夹里会有一个.sh文件   
运行   
'''bash
box64 ./<filename.sh>
'''
运行后会打开gog的游戏安装程序，安装即可   
安装时记得关注游戏安装位置，默认为 “ ~/GOG Games ”   
安装完成后打开游戏安装目录，里面会有一个文件叫 start.sh   
运行
'''bash
box64 ./start.sh
'''
即可开始游戏。
#### 3.游戏运行结果
加载游戏时略有卡顿   
时有闪退。  
 
