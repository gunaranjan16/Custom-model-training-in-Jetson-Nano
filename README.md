# Custom-model-training-in-Jetson-Nano
Here custom object detection model is trained with classes like cars, bikes ,trucks, pedestrians which are needed for our project




+ You have to do this process in your external Linux environment, other than jetson nano board
# Expand memory (recommended)
- for that, ensure sufficient memory is available, if not increase memory using gparted tool
- sudo apt-get install gparted
- sudo gparted
- expand memory and save


# Install dependencies
-make sure python3 is installed
install dependencies below-
- sudo apt install python3-pip
- pip3 install opencv-python
- pip3 install imutils
- pip3 install matplotlib
- pip3 install torchvision
- pip3 install torch
- pip3 install boto3
- pip3 install pandas
- pip3 install urllib3
- sudo apt-get install pyqt5-dev-tools
- sudo apt-get install python3-lxml
- sudo apt install git
# Clone jetson official github repository for training
- git clone https://github.com/mailrocketsystems/jetson-train.git(Clone this github repository)
- create a video in .mp4 format that covers all the possible views of each objects you are going to train 
- place the video inside jetson-train/videos in .mp4 format and remember what the name of the file is.
- now we have to convert the video file to frame by frame images using prepare_dataset.py python file
- in the 20th line of code, we have a predefined count 10, you can increase the count to decrease the number of images to be generated and vice-versa.(This is to control the number of frames )
- cd jetson-train/
- python3 prepare_dataset.py
- it will ask model name,give the model name as per your wish(don't duplicate).
- now video will play,and it will store several images inside the model file you mentioned.(wait till the video is ended)

# Annotating using Label image tool
- now we have to give the annotation to each image we've captured
- Install LabelImg via pip:
pip install labelImg
- Launch it by running:
labelImg
- this will open label image tool
- open dir and choose path as jetson-train/data/model_name/JPEGimages/
- it will load all the image files in the file list
- click change save dir and choose path as jetson-train/data/model_name/Annotations/
- it will save all annotations inside directory
- click create rect box (Ctrl+W)and draw boundary to the object, give name to object and click save
- paste rectbox for each repeating image and draw new for new object
- do it for all images and save each.

# Training custom objects
Do this is high speed cpu/gpu(Definitely not Jetson nano)
- create labels.txt file inside jetson-train/data/model_name (gedit labels.txt)
- list the name of objects you are going to train in the labels.txt file, one name in one line and top left alligned,and save.
- open a new terminal at jetson-train
- python3 train_ssd.py --dataset-type=voc --data=data/model_name/ --model-dir=models/model_name --batch-size=2 --workers=2 --epochs=300
- close all other applications on the system
- it will take some time
- open terminal at jetson-train
- python3 result.py
- give model_name
- it will show results graph and it will give best check point
- copy best check point and labels.txt file
