![](https://github.com/Casas846/NeuroTimber/blob/main/Logo.png)

# NeuroTimber

### NeuroTimber: Estimating Stacked Timber Volume Using AI Detection and Diameter Distribution Models

#### Introduction
NeuroTimber is a cutting-edge project that aims to estimate the volume of stacked timber using advanced artificial intelligence techniques. By leveraging YOLOv9 for detection and Scipy for distribution fitting, NeuroTimber provides accurate and efficient volume estimation.

#### Methodology
1. **Installation of Necessary Packages**: 
   We begin by installing essential packages like numpy, OpenCV, torch, supervision, IPython, pandas, scipy, and matplotlib.\
   
   ```python
   # Install necessary packages
   !pip install numpy opencv-python-headless torch supervision IPython pandas scipy matplotlib
   
3. **Cloning YOLOv9 Repository**:
   The YOLOv9 repository is cloned to access the required models.

   ```python
   # Clone the YOLOv9 repository to access the models
   !git clone https://github.com/SkalskiP/yolov9.git
   %cd yolov9
   !pip3 install -r requirements.txt -q
   
4. **Detection with YOLOv9**:
   We extend Supervision's Detections to handle YOLOv9 results, facilitating accurate detection of timber logs.

   ```python
   # Extending Supervision's `Detections` to Handle YOLOv9 Results
class ExtendedDetections(BaseDetections):
    @classmethod
    def from_yolov9(cls, yolov9_results):
        xyxy, confidences = yolov9_results.xyxy[0].cpu().numpy(), yolov9_results.pred[0][:, 4].cpu().numpy()
        return cls(
            xyxy=xyxy,
            confidences=confidences,
            class_ids=yolov9_results.pred[0][:, 5].cpu().numpy().astype(int)
        )

5.  **Volume Estimation**:
   The detected timber logs are analyzed using Scipy to fit diameter distributions, allowing precise volume estimation.

   ```python
   # Fitting diameter distributions using Scipy
   from scipy.stats import genextreme, powernorm, pearson3, genhyperbolic, johnsonsu, skewnorm, nct, gennorm, exponnorm, norm, dweibull, dgamma, t

   # Example distribution fitting
   data = [log['diameter'] for log in detected_logs]
   params = genextreme.fit(data)

#### Results
The NeuroTimber project successfully integrates YOLOv9 and Scipy to provide a robust solution for timber volume estimation. The methodology ensures high accuracy and efficiency, making it an invaluable tool for forestry and timber industries.
