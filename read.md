#The yolo accept bbox in below format
# The height and width should be scaled from 0 to 1
# The bbox coordinates should be rotated by 270

#coco.yaml file contains path to train, val, and test files 

train: /mnt/X/..../train.txt


#train.txt should contains the paths for each image.png

class_index_starting_from_zero x_centre  y_centre  width_of_bbox  height_of_bbox
5 0.5 0.5 0.26 0.75
0 0.54 0.7 0.5 0.9



#To train on single GPU
python train.py --batch-size 20 --img 1024 1024 --data cocc.yaml --cfg yolov4-p5.yaml --weights yolo/weights/yolov4-p5.pt --sync-bn --device 0 --name yolov4-p5 --labelsPath 'path/to/labels/image.txt'


#To test
python test.py --weights runs/exp53_yolov4-p5/weights/best.pt --data data/coco.yaml --batch-size 4 --img-size 1024 --conf-thres 0.2 --device 0 --labelsPath 'path/to/labels/image.txt'

# To detect
python detect.py --weights runs/exp53_yolov4-p5/weights/best.pt --source 'path/to/png or jpg/' --output 'path/to/write/detections/' --img-size 1024 --conf-thres 0.25

