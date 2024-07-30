![](https://github.com/Casas846/NeuroTimber/blob/main/Logo.png)

# NeuroTimber

## English

### NeuroTimber: Estimating Stacked Timber Volume Using AI Detection and Diameter Distribution Models

#### Introduction
NeuroTimber is a cutting-edge project that aims to estimate the volume of stacked timber using advanced artificial intelligence techniques. By leveraging YOLOv9 for detection and Scipy for distribution fitting, NeuroTimber provides accurate and efficient volume estimation.

#### Methodology
1. **Installation of Necessary Packages**: 
   We begin by installing essential packages like numpy, OpenCV, torch, supervision, IPython, pandas, scipy, and matplotlib.
   ```python
   !pip install numpy opencv-python-headless torch supervision IPython pandas scipy matplotlib
   
2. **Cloning YOLOv9 Repository**:
   The YOLOv9 repository is cloned to access the required models.

!git clone https://github.com/SkalskiP/yolov9.git
%cd yolov9
!pip3 install -r requirements.txt -q

3. **Detection with YOLOv9**:
  We extend Supervision's Detections to handle YOLOv9 results, facilitating accurate detection of timber logs.

class ExtendedDetections(BaseDetections):
    @classmethod
    def from_yolov9(cls, yolov9_results):
        xyxy, confidences, ...

4.  **Volume Estimation**:
  The detected timber logs are analyzed using Scipy to fit diameter distributions, allowing precise volume estimation.

### Results
The NeuroTimber project successfully integrates YOLOv9 and Scipy to provide a robust solution for timber volume estimation. The methodology ensures high accuracy and efficiency, making it an invaluable tool for forestry and timber industries.
