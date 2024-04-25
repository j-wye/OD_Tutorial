## Training

1. yolov5 folder download with git clone
    ```python
    from google.colab import drive
    drive.mount('/content/drive')
    %cd /content/drive/MyDrive
    ```
    ```
    !git clone https://github.com/ultralytics/yolov5
    ```
    <img src="./config/yolov5_download.png">
    
    위의 사진과 같이 *yolov5*가 *MyDrive* 폴더 안에 존재해야 한다.

    이렇게 되었을 때, `%cd yolov5` 를 입력해 현재 위치를 *yolov5* 폴더로 이동한다.

2. Training
    ```python
    !python train.py --weights '' --cfg models/yolov5m.yaml --data coco128.yaml --epochs 300 --batch-size 128
    ```
    `coco128` 이라는 dataset을 직접 학습을 진행한다.

    위와 같이 학습을 진행하면, pretrained model 말고 직접 learning을 통해 pt파일을 얻을 수 있다.
    
    해당 알고리즘을 개발한 사람이 공유한 weight파일을 pretrained model이라고 부르고, 기본적인 경우에는 이 pretrained model을 사용하는 것이 일반적으로 정확도가 더 높다.

    하지만 여기서는 직접 training 시켜서 진행하는 경우에 대해서 다룬다.

    <img src="./config/training.png">

3. Detection
