x86
Python版本要求必须是3.10
创建文件夹~/tpu_mlir
终端中进入该文件夹
## 安装docker
如果已经满足ubuntu22.04和python3.10，直接跳转至安装tpu_mlir
```  bash
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```
```  bash
# 拉取镜像
docker pull sophgo/tpuc_dev:v3.2
# 新建容器
# 注意修改<myname>的值
docker run --privileged --name <myname> -v $PWD:/workspace -it sophgo/tpuc_dev:v3.2
```
这一步之后，我们就会进入docker的workspace
```bash
root@d9e9aac2c4d7:/workspace# 
```


## 安装tpu_mlir
### 方法一：慢速
```  bash
pip install tpu_mlir
```
### 方法二：快速
```  bash
# 从Github的Assets处下载最新的tpu_mlir-*-py3-none-any.whl,然后使用pip安装
pip install tpu_mlir-\*py3-none-any.whl
# 详细步骤见下
```
步骤  
#### 1.重开一个终端，进入tpu_mlir文件夹。此时不要关闭 安装mlir 的终端   
#### 2.将github上下载的whl文件放到：   <容器名称>:/要复制到的地址   
命令是
```bash
docker cp 文件地址 myname(容器名称):/要复制到的地址  
```
这里我的命令是
```
docker cp /home/ly/tpu_mlir/tpu_mlir-1.6-py3-none-any.whl myname:/workspace/tpu_mlir-1.6-py3-none-any.whl
```
#### 3.回到安装mlir的终端
#### 4.使用ls查看镜像里是否有wsl，然后使用pip install安装
``` bash
ls
# 返回值：tpu_mlir-1.6-py3-none-any.whl
pip install tpu_mlir-1.6-py3-none-any.whl
# 等待终端显示Successfully installed tpu-mlir-1.6
```
## ONNX模型的编译和转换
首先下载文件
yolov5.onnx:https://github.com/ultralytics/yolov5/releases/download/v6.0/yolov5s.onnx   
tpu_mlir_resource:https://github.com/sophgo/tpu-mlir/releases/   
下载下来的文档名字是tpu-mlir-resource.tar，解压之后需要修改名称，中间的连接符修改为下划线：tpu_mlir_resource   
在~/tpu_mlir下打开终端，进行复制
```bash
docker cp /home/ly/tpu_mlir/tpu_mlir_resource myname:/workspace.tpu_mlir_resource
docker cp /home/ly/tpu_mlir/yolov5s.onnx myname:/workspace/yolov5s.onnx
# 然后看一下是不是存在
ls
```
然后回到安装mlir的终端
先安装一下tpu_mlir[onnx]
```bash
root@d9e9aac2c4d7:/workspace# pip install tpu_mlir[onnx]
```
在docker中，新建文件夹model_yolov5s用于存放相关文件以及进行转化操作
```bash
root@d9e9aac2c4d7:/workspace# mkdir model_yolov5s && cd model_yolov5s
root@d9e9aac2c4d7:/workspace/model_yolov5s#
# 将图片和模型复制到model_yolov5s文件夹中
root@d9e9aac2c4d7:/workspace# cp -rf tpu_mlir_resource/dataset/COCO2017 .
#这里如果报错，说No such file or dir
root@d9e9aac2c4d7:/workspace/model_yolov5s# cd ..
root@d9e9aac2c4d7:/workspace# cp -rf yolov5s.onnx ./model_yolov5s
root@d9e9aac2c4d7:/workspace# cp -rf tpu_mlir_resource/image ./model_yolov5s
root@d9e9aac2c4d7:/workspace# cp -rf tpu_mlir_resource/dataset/COCO2017 ./model_yolov5s
root@d9e9aac2c4d7:/workspace# cd model_yolov5s
root@d9e9aac2c4d7:/workspace/model_yolov5s# ls
# 返回值： COCO2017   image   yolov5s.onnx

#再新建一个workspace文件夹
root@d9e9aac2c4d7:/workspace/model_yolov5s# mkdir workspace && cd workspace
root@d9e9aac2c4d7:/workspace/model_yolov5s/workspace#
```
### onnx模型转换成mlir模型
```bash
root@d9e9aac2c4d7:/workspace/model_yolov5s/workspace#
model_transform \
    --model_name yolov5s \
    --model_def ../yolov5s.onnx \
    --input_shapes [[1,3,640,640]] \
    --mean 0.0,0.0,0.0 \
    --scale 0.0039216,0.0039216,0.0039216 \
    --keep_aspect_ratio \
    --pixel_format rgb \
    --output_names 350,498,646 \
    --test_input ../image/dog.jpg \
    --test_result yolov5s_top_outputs.npz \
    --mlir yolov5s.mlir
```
然后会显示
[Success]:npz_tool.py ......
转换成功后会生成一个{model_name}_in_f32.npz文件。这里就是yolov5s_in_f32.npz文件
### 将mlir文件转换成f16的bmodel：
```bash
root@d9e9aac2c4d7:/workspace/model_yolov5s/workspace# 
model_deploy \
    --mlir yolov5s.mlir \
    --quantize F16 \
    --processor bm1684x \
    --test_input yolov5s_in_f32.npz \
    --test_reference yolov5s_top_outputs.npz \
    --model yolov5s_1684x_f16.bmodel
```
然后会显示
[Success]:npz_tool.py compare......
表示转换成功


# 使用校准表生成 INT8 对称模型
量化int8
通过calibration得到转换int8时的校准表
```bash
run_calibration yolov5s.mlir \
    --dataset ../COCO2017 \
    --input_num 100 \
    -o yolov5s_cali_table
```
运行完成后会生成名为 yolov5s_cali_table 的文件。   
```bash
root@d9e9aac2c4d7:/workspace/model_yolov5s/workspace# ls
# 会显示yolov5s_cali_table
```

然后转成INT8对称量化模型   
```bash
root@d9e9aac2c4d7:/workspace/model_yolov5s/workspace# 
model_deploy \
    --mlir yolov5s.mlir \
    --quantize INT8 \
    --calibration_table yolov5s_cali_table \
    --processor bm1684x \
    --test_input yolov5s_in_f32.npz \
    --test_reference yolov5s_top_outputs.npz \
    --tolerance 0.85,0.45 \
    --model yolov5s_1684x_int8_sym.bmodel
```
显示Success后即为转换成功

# 使用模型进行推理
#### onnx
```bash
detect_yolov5 \
    --input ../image/dog.jpg \
    --model ../yolov5s.onnx \
    --output dog_onnx.jpg
```
#### f16 bmodel
```bash
detect_yolov5 \
    --input ../image/dog.jpg \
    --model yolov5s_1684x_f16.bmodel \
    --output dog_f16.jpg
```
#### int8 bmodel
```bash
detect_yolov5 \
    --input ../image/dog.jpg \
    --model yolov5s_1684x_int8_sym.bmodel \
    --output dog_int8_sym.jpg
```