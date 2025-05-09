# 安装与运行
## 配置环境
python3.10以上，下文使用的是ubuntu24.04自带的3.12.3     

```
sudo apt install python3.12-venv
```
创建虚拟环境，将虚拟环境创建在~下
```
~$ python3 -m venv x-anylabeling
```
激活虚拟环境
```
source x-anylabeling/bin/activate  #linux
x-anylabeling\Scripts\activate     #win
```
## 在虚拟环境下安装onnx
pip install PyQt5
pip install numpy
pip install onnxruntime
## 下载AnyLabeling
官网链接：https://github.com/CVHub520/X-AnyLabeling/tree/main   
安装链接：https://github.com/CVHub520/X-AnyLabeling/releases   
两个版本：Linux与Windows    
无论是哪个，都建议使用git clone     
```
## 扒库
git clone git@github.com:CVHub520/X-AnyLabeling.git   
## 进入cmd或terminal，进入clone文件夹
pip install -r requirements.txt
pip install -r requirements-gpu.txt
## 在clone文件夹下
pyrcc5 -o anylabeling/resources/resources.py anylabeling/resources/resources.qrc
## 防止冲突
pip uninstall anylabeling -y
```

# 运行
## 安装完成后运行app.py
python anylabeling/app.py












# 使用
软件的详细使用可以参考官方文档   
https://github.com/CVHub520/X-AnyLabeling/blob/main/docs/zh_cn/user_guide.md   
模型文件   
https://github.com/CVHub520/X-AnyLabeling/blob/v1.1.0/docs/custom_model.md   
模型文件需要下载的有yaml文件和onnx文件    
需要打开yaml文件，给modle_path设置为onnx的路径

每标注了一张图片，就会在指定文件夹（默认为当前文件夹）下生成对应的json文件   











