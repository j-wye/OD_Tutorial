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
    !python train.py --weights '' --cfg models/yolov5m.yaml --data coco128.yaml --epochs 300 --batch-size 32
    ```
    `coco128` 이라는 dataset을 직접 학습을 진행한다.

    위와 같이 학습을 진행하면, pretrained model 말고 직접 learning을 통해 pt파일을 얻을 수 있다.
    
    해당 알고리즘을 개발한 사람이 공유한 weight파일을 pretrained model이라고 부르고, 기본적인 경우에는 이 pretrained model을 사용하는 것이 일반적으로 정확도가 더 높다.

    하지만 여기서는 직접 training 시켜서 진행하는 경우에 대해서 다룬다.

    <img src="./config/training.png">

    위의 사진에 맨 아래에 epoch가 0부터 299까지 나오고 순차적으로 하나씩 증가하면서 진행되고 있으면 학습이 시작되었다는 것을 알 수 있다.

    <img src="./config/training_last.png">
    
    위와 같이 저장되었다고 나타난다면 제대로 learning이 끝났다.

    ```python
    import cv2
    from google.colab.patches import cv2_imshow

    result_path = 'runs/train/exp/results.png'
    result = cv2.imread(result_path)
    cv2_imshow(result)
    ```
    <img src="./config/training_result.png">
    
    위의 코드를 통해 위의 이미지와 같은 학습의 결과가 나오는 것을 확인할 수 있다.
    

3. Detection

    Pretrained model을 사용하는 것이 아니라 직접 training을 시켜서 weight파일을 얻는 경우에는, /yolov5/runs/train/exp 폴더 안에 결과값이 저장된다.
    ```python
    import torch
    import cv2
    from google.colab.patches import cv2_imshow

    weight_file_path = '/runs/train/exp/weight/best.pt'
    model = torch.hub.load('ultralytics/yolov5', 'custom', path=weight_file_path force_reload=True, trust_repo=True)
    img_zidane = '/data/images/zidane.jpg'
    img_bus = '/data/images/bus.jpg'

    yolo_1 = model(cv2.imread(img_zidane))
    yolo_2 = model(cv2.imread(img_bus))
    img_1 = yolo_1.render()[0]
    img_2 = yolo_2.render()[0]
    cv2_imshow(img_1)
    cv2_imshow(img_2)
    ```
    위와 같이 코드를 작성하면, 직접 학습시킨 weight파일로 제대로 detection이 되는지 확인해 볼 수 있다.