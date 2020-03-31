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

Note: 'yolov3.weights' exceed github's storage limit. The notebook will not execute without it. A copy needs to be obtained from https://pjreddie.com/darknet/yolo/ or other sources.

```

# How it works in a nutshell

1. In the very first frame and only in the very first frame(done by choice), the user selects a region of interest, the ball in the picture. A tracking algorithm then initializes using ```bounding box``` set by the user and subsequently ```tracks``` the highlighted region for a set number of frames.
2. Every ```10 frame``` afterwards, the detector tries to detect the ball. If the center of the tracker's bounding box, falls outside the detector's bounding box, the tracker resets to the detector's bounding box.
3. While the ball is tracking, the tracker's name is displayed at the bottom left. If the detector ```fails to detect twice```, it the bottom right displays ```No objects detected``` instead.

# Additional Notes
The detection is pretty time consuming causing the video to stutter in a live feed, this is because the detection is utilizing the CPU instead of the GPU. You can change the tracker anytime in the video, which affects the overall framerate.

# Sample

Snippet of the user selecting the ROI in the first frame

![](images/BG_change.png)

Snippet of tracker changing

![](images/Tracker_change.png)

Long clip sample

![](images/run.png)
