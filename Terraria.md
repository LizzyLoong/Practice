# 在Lichee Pi 4A上运行 Terraria

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
#### 1.游戏应用包下载
https://archive.org/details/terraria-v-1.4.4.9-v-4-gog-linux-v-60321-gui   
下载7-zip版本   
##### 2.解压压缩包与安装游戏
解压压缩包后，有一个terraria_version.sh文件，   
'''bash
box64 ./terraria_v1_4_4_9_v4_60321.sh
'''
之后会打开terraria的安装程序   
安装就可以   
注意关注一下安装位置，默认安装在   
/home/UserName/GOG Games/Terraria   
开始安装，安装完成后进入上面提到的游戏安装文件夹中   
在该文件夹中有start.sh文件，运行游戏   
'''bash
box64 ./start.sh
'''
#### 3.游戏运行结果
加载游戏时有明显卡顿   
在等待几分钟后会进入游戏   
进入游戏后有卡顿，但是也能正常玩，只是帧率低    
音响有杂音   
   


