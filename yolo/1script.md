整个的流程，允许行出来的结果展示，允许行出来训练好的默写行，标注好的图片或视频




大家好，这期视频
尝试通过yolo进行图像识别
我们要识别的对象是王者荣耀
首先在王者荣耀运行过程中截取几张图片
截取方式有许多种，比如通过ffmpeg来截取
也需要准备yolo环境来训练模型
这里已经训练好了，我放在简介里大家有需要可以自取
所以我们直接来运行
看看识别效果怎么样
在这里我们快速过一下代码
代码的具体内容请大家参考github
然后进入到result文件夹来运行程序
这里我们直接用READ ME文件里的内容
复制里面的命令运行




ssh root@192.168.42.1
cd milkv-duo-yolo11/duocode
cd duocode
vim v11.cpp
cd ../result
./sample_yolov8 ./

ssh root@192.168.42.1
cd milkv-duo-yolo11/result







$ ruyi venv -t gnu-plct milkv-duo -e qemu-user-riscv-upstream ./qemu-milkv
fatal error: cannot find the installed directory for the emulator

keyide
$ ruyi venv -t gnu-plct milkv-duo -e qemu-user-riscv-xthead ./xthead-qemu-milkv
lizzy@Lizzy-Ubuntu-10875:~/桌面/workspace$ . xthead-qemu-milkv/bin/ruyi-activate
«Ruyi xthead-qemu-milkv» lizzy@Lizzy-Ubuntu-10875:~/桌面/workspace$ riscv64-plct-linux-gnu-gcc -O3 hello.c -o milkv_qemu
«Ruyi xthead-qemu-milkv» lizzy@Lizzy-Ubuntu-10875:~/桌面/workspace$ ruyi-qemu ./milkv_qemu
qemu-riscv64: unable to find CPU model 'thead-c906'



riscv64-unknown-linux-gnu-gcc
lizzy@Lizzy-Ubuntu-10875:~/host-tools/gcc/riscv64-linux-x86_64/bin$ ./riscv64-unknown-linux-gnu-gcc -O3 v12.c -o sample_yolov8

