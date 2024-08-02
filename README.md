![](https://github.com/Casas846/NeuroTimber/blob/main/Logo.png)

# NeuroTimber

### NeuroTimber: Estimating Stacked Timber Volume Using AI Detection and Diameter Distribution Models

#### Introduction
NeuroTimber is an execution platform designed to assist users in estimating the volume of stacked timber. This platform allows users to upload their own detection models and diameter data at specific heights derived from stem taper analysis. By integrating YOLOv9 for object detection and Scipy for fitting statistical distributions, NeuroTimber provides a flexible and efficient framework for users to process their timber data and obtain volume estimates.

The methodology involves several key steps. Users first upload their trained YOLOv9 detection models and corresponding labels, along with stem diameter data and video footage of stacked timber. NeuroTimber then processes the video to detect and count the logs, fits statistical distributions to the stem diameter, and calculates the estimated volume of the timber stack based on these detections and distributions. This approach ensures that users can leverage their specific models tailored to their unique datasets and requirements.

#### Required Uploads
To use this repository, please ensure you upload the following files:

1. Detection Model (.pt file): This is the YOLOv9 model trained for log detection.
2. Model Labels (.yaml file): The corresponding labels for the detection model.
3. Stem Diameter Data (.xlsx file): An Excel file containing diameter data obtained from stem taper analysis of trees in the pre-harvest inventory.
4. Stacked Timber Video (.mp4): A video of the stacked timber for which you want to estimate the volume.

Users can test this platform with their own files or our sample files, available for download at the following link: https://drive.google.com/drive/folders/1Bj0P8ypXSGoexGWXApSrmuHzK8K8bJBv?usp=sharing

####  Installation and Setup

1. Install necessary packages
```python
!pip install numpy opencv-python-headless torch supervision IPython pandas scipy matplotlib
```

2. Clone the YOLOv9 repository to access the models
```python
!git clone https://github.com/SkalskiP/yolov9.git
%cd yolov9
!pip3 install -r requirements.txt -q
```

3. Set the paths for the uploaded files and replace it in the execution platform
```python
weights = '/content/yolov9-c-wooddetection-converted.pt' #Detection Model
data = '/content/wooddetection.yaml' #Model Labels 
SOURCE_VIDEO_PATH = '/content/Test_Video.mp4' #Input Video Processing 
TARGET_VIDEO_PATH = '/content/Demo_Video.mp4' #Output Video Processing 
data_path = '/content/dados.xlsx' #Pre-Harvest Forest Inventory Data 
```

4. Set Log Length and replace it in the execution platform
```python
log_length = 6  # Customize log length in meters as needed
```
####  Volume Estimation Process Explanation

1. Volume Observed for Each Class

This line calculates the observed volume for each class of logs.
```python
volume_observed = (np.pi / 40000) * (class_number ** 2) * log_length
```
Where:\
.  class_number: Represents the diameter class of the logs.\
.  log_length: The customizable length of the logs.\
.  np.pi / 40000: A scaling factor for the calculation.\

2. Estimated Volume for Each Class

This line calculates the estimated volume for each class by multiplying the observed volume with the probability and the log count. 
```python
volume_estimated = probability * log_count * volume_observed
```
Where:\
.  probability: The likelihood of a log being in a particular class.\
.  log_count: The number of logs in that class.\
.  volume_observed: The previously calculated observed volume for the class.

3. Total Estimated Volume

This line accumulates the estimated volume for each class into a total estimated volume.
```python
total_volume_estimated += volume_estimated
```
Where:\
.  volume_estimated: The estimated volume for the current class.\
.  total_volume_estimated: The running total of the estimated volume across all classes.

# Contacts
For any colaborations, questions, feedback, comments, or inquiries, please contact me at:

Gianmarco Goycochea Casas\
Federal University of Viçosa, Brazil\
Email: gianmarco.casas@ufv.br
