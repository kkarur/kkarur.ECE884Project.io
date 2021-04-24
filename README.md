# End-to-End Synthetic LIDAR Point Cloud Data Generation & Deep Learning Validation!

Generation of synthetic and segmented Point Cloud LiDAR data and Object detection is a custom implementation of the paper from Uber ATG using PyTorch 1.0. It represents the driving scene using lidar data in the Birds' Eye View (BEV) and uses a single stage object detector to predict the poses of road objects with respect to the car


# Project Overview

![image](https://user-images.githubusercontent.com/83134822/115968947-5340a900-a508-11eb-9d16-4c6aa75fa7db.png)



## Steps to Run Object Detection for Point cloud data

Create a folder “LidarProject” in your google drive.
Upload the project “PIXOR.zip” and “34epoch” into that location, and run the below command

```
from google.colab import drive
drive.mount('/content/drive')
```
Then you have to compile the c-library of the project using the below command

```
!pip install shapely numpy matplotlib
!unzip -qq /content/drive/MyDrive/LidarProject/PIXOR.zip
%cd PIXOR/srcs/preprocess
!make
!ls
%cd ..
```

You need KITTI library for this, to save time we have uploaded the library into google drive as well. If you just want to give it a try then you can use the following commands to get the library in google colab

```
!wget https://s3.eu-central-1.amazonaws.com/avg-kitti/data_object_velodyne.zip
!wget https://s3.eu-central-1.amazonaws.com/avg-kitti/data_object_label_2.zip
!unzip -qq data_object_velodyne.zip
!unzip -qq data_object_label_2.zip
!ls 

```
While in this operation you might find the below pop-up, you need not have to worry about it and choose “Ignore”, as we will not take full memory for our test run

![image](https://user-images.githubusercontent.com/83134822/115968633-cba66a80-a506-11eb-8d55-7b59841e17de.png)

Note: This will take a while, so to avoid this time delay as mentioned above we uploaded both the datasets on google drive in the folder that we created and ran the below command just to unzip
```
!unzip -qq /content/drive/MyDrive/LidarProject/data_object_velodyne.zip
!unzip -qq /content/drive/MyDrive/LidarProject/data_object_label_2.zip
!ls

```
Project expects files in certain folder so let’s go ahead and create them now

```
!mkdir data_object_velodyne
!mkdir test
!python3 copyfolder.py

```
Let’s now take the Point cloud data that we have created from unity and place it “test” folder marked in yellow box(you can drag and drop) as Project expects the *.csv file in that location. (You can find the test data in the project folder under “TestData”) run the command below

![image](https://user-images.githubusercontent.com/83134822/115968708-2770f380-a507-11eb-988a-f8f45fc11a9a.png)

```
!python3 csv2bin.py

```
Run the below command and you should find the output in the “srcs” folder (try refresh if you don’t see the Prediction.png file) 
```
!python3 object_detector.py
```

## Evaluation Results

3 car Detection
![image](https://user-images.githubusercontent.com/83134822/115968756-57b89200-a507-11eb-86f4-7cf9646ecb5d.png)
![image](https://user-images.githubusercontent.com/83134822/115968764-5be4af80-a507-11eb-85fb-d451237d2bde.png)

4 car Detection
![image](https://user-images.githubusercontent.com/83134822/115968776-6f901600-a507-11eb-929c-a91e33b00096.png)
![image](https://user-images.githubusercontent.com/83134822/115968779-7454ca00-a507-11eb-9e20-ac8fb1d9069e.png)





