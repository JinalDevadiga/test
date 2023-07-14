
# Leaf Segmentation and Classification

A YOLOv5s model that uses the Segmentation model to segment the leaves from the images and then classify each leaf using the Classification model.


## Table of Contents

- Process Flow
- Documentation
- Running Tests


## Process Flow

![Leaf-seg drawio](https://github.com/JinalDevadiga/test/assets/87411508/879096f1-c304-4400-a23b-9f41de5c8c27)

- Run the segment/predict.py with values for weights, test images and confidence threshold.
- The images would be passed to the YOLOv5 segmentation model.
- The NDarray of each cropped segmented image will be stored in a list.
- This list will be then passed to the YOLOv5s classification model.
- The classification model will the classify the image as 0, 1, 2 or reject.
- The results of the segmentation and classification model will be stored under the `yolov5/runs/` folder.
## Documentation
#### Storing cropped segmented images in the list
```python
# Cropped image classification
c = int(cls)  # integer class
label = None if hide_labels else (names[c] if hide_conf else f'{names[c]} {conf:.2f}')
                    
# Storing cropped images in the list
crop_img.append(save_one_box(xyxy, imc, file=save_dir / 'crops' / names[c] / f'{p.stem}.jpg', BGR=True))

```
#### Classification
```python
# Calling a function named `run` in classify /predict.py with the following parameters:
predict.run(
        nd_array=crop_img, 
        weights='/home/ubuntu/jinal/yolo-leaf-seg yolov5/runs/train-cls/exp27/weights/best.pt', 
        save_txt=True
    )
```
#### Best weights for classification:
- 01_reject: "/home/ubuntu/jinal/yolo-leaf-seg/yolov5/runs/train-cls/exp15/weights/best.pt" 
- 01_reject_aug: "/home/ubuntu/jinal/yolo-leaf-seg/yolov5/runs/train-cls/exp23/weights/best.pt"
- 012_reject: "/home/ubuntu/jinal/yolo-leaf-seg/yolov5/runs/train-cls/exp20/weights/best.pt"
- 012_reject_aug: "/home/ubuntu/jinal/yolo-leaf-seg/yolov5/runs/train-cls/exp27/weights/best.pt"

## Running Tests

To run test, run the following command

```bash
  python segment/predict.py --img 640 --weights 'weights' --source 'test_images' --conf-thres 0.15
```

## Author

- Jinal Devadiga
