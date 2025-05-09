# yolo直接导出
官方文档：https://docs.ultralytics.com/zh/modes/export/#usage-examples   
在上一步我们已经获得了yolo11n.pt
这一步我们将其转换为onnx文件

在转换时，使用python进行转换
示例代码
```  python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")  # load an official model
model = YOLO("path/to/best.pt")  # load a custom trained model

# Export the model
model.export(format="onnx")
```
这里，export函数有许多参数可以使用
官方文档中也提供了所有参数
我们需要注意的几个参数有：
format："onnx"
dynamic：True
imgsz:不设置
int8:True
simplify:True
device:cpu

运行export后，就会生成onnx文件


在X-AnyLabeling中使用时，我们需要修改yaml文件
因为官方还没有对最新版yolo的兼容，我们直接对着yolov8的配置文件修改即可
yaml文件
```
type: yolov8
name: yolov8l-r20230520
display_name: YOLO11n
model_path: yolo11n.onnx
nms_threshold: 0.45
confidence_threshold: 0.25
classes:
  - person
  - bicycle
```


# pt转onnx






