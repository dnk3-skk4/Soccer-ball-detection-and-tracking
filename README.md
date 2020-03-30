# Soccer-ball-detection-and-tracking
A detection and tracking implementation using YOLOv3 detection and tracking using various tracking methods available in OpenCV.

I used a pre-trained yolov3 neural net by acquiring ```coco.names```, ```yolov3.cfg```, and ```yolov3.weights``` files and loaded the network using the following line of code:
```
y3_weights_path = './data/yolov3.weights'
y3_config_path = './data/yolov3.cfg'
coco_classes_path = './data/coco.names' # file with multiple classes
classes = None
with open(coco_classes_path, 'rt') as f:
  classes = f.read().strip('\n').split('\n')

# load the network
net = cv2.dnn.readNetFromDarknet(y3_config_path, y3_weights_path)

```

```

Note that the Yolov3 weights file exceeds that 25mb limit of github. If you wish to clone this repository, you will need to obtain a copy of the yolov3 weights file, name it 'yolov3.weights' and store it inside that data folder

```

# How it works in a nutshell

1. In the very first frame and only in the very first frame(done by choice), the user selects a region of interest, the ball in the picture. A tracking algorithm then initializes using ```bounding box``` set by the user and subsequently ```tracks``` the highlighted region for a set number of frames.
2. After every ```Nth frame```, the detector tries to detect the ball. If the center of the tracker's bounding box, falls outside the detector's bounding box, the tracker resets to the detector's bounding box.
3. If the ```detector fails to detect the ball twice```, it outputs 'No objects detected'
