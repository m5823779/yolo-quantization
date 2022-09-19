# Yolo v7 / Yolo v5 Quantization using OpenVINO POT

This repo using OpenVINO POT tool to quantize yolo-v7 series or yolo-v5 series onnx model to IR model

## requirement
```
pip install openvino-dev==2022.1
```

## Usage:

1) download yolo repo
```
Yolo v5:
git clone https://github.com/ultralytics/yolov5

Yolo v7:
git clone https://github.com/WongKinYiu/yolov7
```

2) download pre trained weights (tiny version for example)
```
Yolo v5:
wget https://github.com/ultralytics/yolov5/releases/download/v6.2/yolov5s.pt

Yolo v7:
wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-tiny.pt
```

3) place ```yolovX_quantize.py``` into Yolo root folder

4) execute ```train / test / val``` script to create ```labels.cache```

5) (Optional) for yolo v5 replace code ```self.segments[i][:, 0] = 0``` to ```self.segments[i][0][:, 0] = 0``` into file ```<yolo_v5_repo>/utils/dataloaders.py```

6) Pytorch to ONNX 
```
Yolo v5:
python export.py --weights <path_to_model>.pt --include torchscript onnx

Yolo v7:
python export.py --weights <path_to_model>.pt --grid --simplify  --img-size 640 640
```

7) ONNX to OpenVINO IR model
```
mo.exe --input_model <path_to_model>.onnx
```

8) modify config (model & dataset path) in ```yolovX_quantize.py```

9) ```python yolovX_quantize.py```
