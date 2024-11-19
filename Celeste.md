# 在Lichee Pi 4A上运行 Terraria

## 实验准备

请参考 WPS 运行中的硬件准备和软件准备，完成系统烧录

### 软件环境准备

安装完成后，就可以在荔枝派上连接好显示屏启动游戏啦ヾ(≧▽≦*)o

#### 二进制翻译软件

```shell
# 为运行 X86 软件进行翻译准备  安装 Box64
git clone https://github.com/ptitSeb/box64.git
cd box64
mkdir build
cd build
cmake .. -D RV64=1 -D CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install -j$(nproc)
```


### 游戏执行
#### 1.游戏应用包下载链接
https://archive.org/details/celeste-v-1.4.0.0-linux
下载7-zip版本   
##### 2.解压压缩包与安装游戏
解压压缩包后进入解包文件夹
文件夹中有如下文件：Celeste.bin.x86_64  
运行
'''bash
box64 ./Celeste.bin.x86_64  
'''
等待打开游戏
#### 3.游戏运行结果
完全没有问题，游玩完美   
   


