# LicheePi4A_Celeste

1. 配置 `locales`

   ```
   sudo apt install locales
   sudo dpkg-reconfigure locales
   ```

2. 安装 box64，参考 [COMPILE.md](https://github.com/ptitSeb/box64/blob/main/docs/COMPILE.md#for-risc-v)。

   ```bash
   git clone https://github.com/ptitSeb/box64.git
   cd box64
   mkdir build
   cd build
   cmake .. -D RV64=1 -D CMAKE_BUILD_TYPE=RelWithDebInfo
   make -j$(nproc)
   sudo make install
   ```

   

3. 安装 [gl4es](https://github.com/ptitSeb/gl4es)：

   ```
   git clone https://github.com/ptitSeb/gl4es
   cd gl4es
   mkdir build
   cd build 
   cmake .. -DCMAKE_BUILD_TYPE=RelWithDebInfo
   make -j$(nproc)
   ```

4. 购买Celeste，下载 Linux 版 https://www.celestegame.com

5. `chmod +x 游戏包中的start.sh`

6. 运行游戏
   ```
   # 运行 Celeste
   box64 ./Celeste.bin.x86_64
   # 运行 Celeste加上帧数显示
   GALLIUM_HUD=fps box64 ./Celeste.bin.x86_64
   # 运行 Celeste终端打印帧数
   LIBGL_FPS=1 box64 ./Celeste.bin.x86_64
   ```