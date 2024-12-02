I am classifying the sensitivity of panoramic X-rays based on biometric patterns in the images rather than text content (which may be unnatural). This approach uses image processing and feature detection techniques to identify patterns such as:

- Unique tooth structures: Specific arrangements, missing teeth, or dental restorations.
- Jawbone anomalies: Distinct or rare bone patterns.
- Sinus patterns: Unique sinus shapes.
- Metadata, such as personally identifiable information (PII) if available.

*Dataset*
The dataset used for this project is from Roboflow Universe (link: https://universe.roboflow.com/dentex/dentex-3xe7e/dataset/2), specifically tailored for dental X-ray analysis. It consists of:
- Training Set: 873 images (81%)
- Validation Set: 40 images (4%)
- Test Set: 165 images (15%)

The images are pre-labeled with bounding boxes around the relevant dental regions, allowing for the detection of biometric patterns.

----------------------------------------------------------------------------------------------------------------------------------------
2) Methodology
   
*Preprocessing:*
- Contrast Enhancement: Applied CLAHE (Contrast Limited Adaptive Histogram Equalization) for improving visibility.
- Noise Reduction: Gaussian blur was used to smooth the images and reduce noise.
- Edge Detection: Canny edge detection highlighted key structures for analysis.

*Feature Detection:*
- Structural Features: Contour-based bounding box detection was used to identify potential regions of interest (e.g., teeth, jaws, sinuses).
- Deep Learning Detection: A pre-trained YOLOv8 model fine-tuned on dental X-rays was employed to detect advanced features, such as anomalies and restorations.
  
*Sensitivity Classification:*
- High Sensitivity: Images containing unique biometric features like missing teeth, anomalies, or restorations.
- Moderate Sensitivity: Images with general structures like typical tooth or jaw patterns without distinct anomalies.
- Low Sensitivity: Images with no identifiable features or only generic patterns.
  
*Visualization:*
- A bar chart visualizes the number of images in each sensitivity category ("High," "Moderate," and "Low").


----------------------------------------------------------------------------------------------------------------------------------------
3) Code Implementation
   
The code processes the panoramic X-rays, classifies their sensitivity, and visualizes the distribution of sensitivity levels. Below are the key components:

*Preprocessing and Feature Detection:*
- CLAHE, Gaussian blur, and Canny edge detection for structural analysis.
- YOLOv8 for advanced feature detection.
  
*Sensitivity Classification:*
- Combines structural and deep learning detections to classify images into "High," "Moderate," or "Low" sensitivity.

*Visualization:*
- A bar chart shows the distribution of sensitivity levels across the dataset.

----------------------------------------------------------------------------------------------------------------------------------------
4) Results
   
The dataset was classified into the following sensitivity levels:

- High Sensitivity: Images with unique biometric patterns.
- Moderate Sensitivity: Images with general biometric features.
- Low Sensitivity: Images with no distinguishing patterns.
- 
The sensitivity distribution was visualized using a bar chart.

----------------------------------------------------------------------------------------------------------------------------------------
*Dependencies*

Programming Language: Python

Libraries:
- torch for PyTorch-based computations
- ultralytics for YOLOv8
- opencv-python for image processing
- matplotlib for visualization
- numpy for numerical operations
- Pillow for image handling
- scipy for optimization

