# Jetson Nano에서 YOLOv8 사용해보기

### 가상 환경을 만들기 위해 Anaconda3 설치하기
* YOLOv8을 사용하기 위해서는 Python 3.8 이상이 필요
* Jetson Nano는 Python이 구버전
* Jetson Nano는 arch linux

```bash
wget wget https://github.com/Archiconda/build-tools/releases/download/0.2.3/Archiconda3-0.2.3-Linux-aarch64.sh

./Archiconda3-0.2.3-Linux-aarch64.sh
```

### 가상 환경 만들기
```bash
conda create -y -n yolo python=3.8

conda activate yolo
```
### 필요한 패키지 설치하기
```bash
sudo apt install libopenblas-base libopenmpi-dev libomp-dev torch torchvision
```

### YOLOv8을 사용하기 위한 레포지토리 클론
```bash
git clone https://github.com/Tory-Hwang/Jetson-Nano2

cd Jetson-Nano2/V8

pip install -r requirements.txt
pip install ultralytics ffmpeg-python
```

### USB 카메라 인식을 위한 코드 수정
```bash
vi detectY8.py
```

```python
def predict(cfg=DEFAULT_CFG, use_python=False):
  brtsp = False # True -> False
  if brtsp:
    #cfg.source ='https://www.youtube.com/watch?v=yTIQMnnaBZo'
    cfg.source ='rtsp://admin:satech1234@192.168.0.151:554/udp/av0_0'
  else:
    cfg.source = 0
  cfg.imgsz = 640
  cfg.show    = True
  cfg.iou     = 0.45
  cfg.conf    = 0.15
  cfg.data    = "coco128.yaml" # coco128.kor.yaml -> coco128.yaml
  cfg.model   = 'yolov8n.pt'
```

### 실행하기
```bash
python detectY8.py
```
