# CustomObjectDetection

Train YOLOv7 on a Custom Dataset (object detection)
This training is based on the YOLOv7 repository by WongKinYiu. This notebook shows training on our own custom objects. Many thanks to WongKinYiu and AlexeyAB for putting this repository together.

Steps Covered in this Tutorial
To train our detector we take the following steps:

Install YOLOv7 dependencies
Run YOLOv7 training
Evaluate YOLOv7 performance
Run YOLOv7 inference on test images

It's preferred to run the training & inference in a gpu environment. So use Google Colab / Kaggle / any cloud environment and choose GPU instances

 1. Create Virtual Environment "python -m venv Yolov7env", activate the virtual environment by navigating to Yolov7env/scripts folder

 2. Navigate back to Parent directory Yolov7 and Download YOLOv7 repository and install requirements

 3. install the dependencies by running pip install -r requirements.txt

 4. Change the current directory & point to Yolov7

 5. Refer to github repo https://github.com/krisroops/ImageHelper.git and download the sample images of objects you would like the model to detect

 6. go to your terminal (pycharm/jupiter/vscode) and pip install labelImg

 7. Start Annotating and generate labels for the images using labelImg. Make sure the IabelImg setting is pointing to YOLO & not PascalVoc

 8. Start creating bounding boxes or rectangles around the object that needs to be detected using Create Rect Box

 9. Create 2 directories & 2 sub directories in your local drive
    train | train -> images  , train ->labels
    val | val -> images  , val ->labels
    
    Move 80% of the annotated images to train-> images folders and the associated labels to train-> labels folder
    Move remaining 20% of the images to Val ->images folders and the associated labels to val->labels folder

 10. Download the weights: !wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7.pt
 11. Getting ready for Custom Training
    
    a) Navigate to data ->train folder and add images & labels from your local drive to folder under train directory
    b) Navigate to data ->val folder and add images & labels from your local drive to folder under val directory
    c) If there is labels.cache in the train/val folders delete it.
    d) Navaigate to data , create a copy of coco.yaml and rename it to custom_data.yaml
        i) change the number of classes nc to number of objects you want to detect
        ii) give the classnames to the names list.
    e) Navigate to cfg ->training folder, create a copy of yolo7.yaml and rename it to yolo7-custom.yaml. Open the file change the nc = number of objects to detect.

 12. Start Custom Training using the below command and wait patiently ...!
!python train.py --device 0 --batch-size 16 --epochs 100 --img 640 640 --data data/custom_data.yaml --hyp data/hyp.scratch.custom.yaml --cfg /cfg/training/yolov7-custom.yaml --weights yolov7.pt --name yolo7-custom

 13. Inferencing the trained model using the below command
!python detect.py --conf 0.5 --img-size 640 --weights runs/train/yolo7-custom11/weights/best.pt --source crushed_coke_can_3.jpeg --no-trace
    where conf is the confidence threshold, weight is the custom trained weight that you get from the training and source is the image you want to detect the object
        
    

    






