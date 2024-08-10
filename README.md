<h1 align="center">
  <br>
Protecting the Great Barrier Reef – Using YOLO to Detect Invasive Species![image](https://blogger.googleusercontent.com/img/a/AVvXsEj6-rQw5r22Bt47BUTtW5bn_dcWT7zMeADwtvsAHS3kBt6w8eWTmCM649ZcJcvosIMup6flKFIaI8p4M9ZzH1yXpEaMRjvwwfVZ_hMqgXCxtwNzEK25vTa-J2ly20by3M1zx7rTymo-tBI6Fq-mj1SJfCOXsOz0Ou1Esi4h2omvQSW98AjsONsVS-EA)
  <br>
</h1>

<p align="center">This project will utilize real-time object detection models (YOLO) to detect invasive starfish species invading the Australian Great Barrier Reef. 
                  We will show hyperparameter tuning process using Optuna and the various functionalities provided by Ultralytics.
                  As well as compare results between the YOLOv10 model and its predecessors, and between YOLOv10 model sizes![image](https://github.com/user-attachments/assets/44e29946-352f-44dc-ab5e-fa47d55206e9)
</p>

## Dataset

Our dataset comprising 4,917 frames of videos filmed underwater, 
and for each image we have a text file consists the bounding box of the starfish, if it has some, in the format [(x_center, y_center, weight, height)]. Values are normalized relative to image height and width.

[Dataset Source](https://universe.roboflow.com/great-barrier-reef/great-barrier-reef-o5scc)

### Model

We fine-tuned the pretrained model Yolov10, implemented by ultralytics
[Yolov10](https://github.com/THU-MIG/yolov10)

### Results

#TBD

## Execute

To get started, you need to install the required libraries:

Install the YOLOv10 package directly from its GitHub repository and the desired pretrained model (in our example, the nano-version of yolov10)
```python
!pip install -q git+https://github.com/THU-MIG/yolov10.git
!wget -P . -q https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10n.pt
```

## Prepare Data

```Folder structure
datasets/
├── train/
│   ├── images/
│   │    ├── image1.jpg
│   │    ├── image2.jpg
│   │    |   ...
│   │    └── image100.jpg
│   └── labels/
│        ├── image1.txt
│        ├── image2.txt
│        |   ...
│        └── image100.txt  
├── valid/
│   ├── images/
│   │    ├── image101.jpg
│   │    ├── image102.jpg
│   │    |   ...
│   │    └── image200.jpg
│   └── labels/
│        ├── image101.txt
│        ├── image102.txt
│        |   ...
│        └── image200.txt  
├── test/
│   ├── images/
│   │    ├── image201.jpg
│   │    ├── image202.jpg
│   │    |   ...
│   │    └── image300.jpg
│   └── labels/
│        ├── image201.txt
│        ├── image202.txt
│        |   ...
│        └── image300.txt  
└── data.yaml
```

data.yaml should be in the format:
```
names:
- starfish
nc: 1

test: /path/to/datasets/test/images
train: /path/to/datasets/train/images
val: /path/to/datasets/valid/images
```

# Execute
```python
model = YOLOv10('path/to/pretrained_model')
results = model.train(data='path/to/data.yaml',
                      epochs=2,
                      imgsz=640,
                      batch=32,
                      lr0=learning_rate,
                      momentum=0.9,
                      optimizer=optimizer_name,
                      patience=10,
```
There are many optional arguments to pass in addition to the specified below, for more information visit ultralytics documnetation: [ultralytics](https://docs.ultralytics.com/modes/train/)
## Future Work

TBD

## Authors

- Itai Osiroff
- Idan Oren
