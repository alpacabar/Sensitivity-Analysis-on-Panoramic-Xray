_Classifying Sensitivity in Panoramic X-rays_

I am classifying the sensitivity of panoramic X-rays based on biometric patterns in the images rather than text content (which may be unnatural). This approach uses image processing and feature detection techniques to identify patterns such as:

- Unique tooth structures: Specific arrangements, missing teeth, or dental restorations.
- Jawbone anomalies: Distinct or rare bone patterns.
- Sinus patterns: Unique sinus shapes.
- Metadata, such as personally identifiable information (PII) if available.

----------------------------------------------------------------------------------------------------------------------------------------

*How trustworthy is this detection?*

1. Preprocessing Enhances Detection: Techniques like CLAHE, noise reduction, and edge detection improve feature visibility, supporting both structural and YOLO-based analysis.
2. YOLO: YOLOv8, a state-of-the-art object detection model, ensures reliable and real-time detections when fine-tuned on a dental dataset.
3. Combination of Structural and YOLO Features: Integrates structural contour-based features with YOLO to achieve a balance between traditional image analysis and deep learning.

However, there are few limitations that require attention:
1. Model Dependence: Detection accuracy is tied to the quality and diversity of the training dataset. Inadequate training may lead to false positives or missed detections.
2. Simplistic Structural Analysis: Contour-based detection relies on clear edges, which may fail in noisy or low-quality images.
3. Context Awareness: Sensitivity classification does not yet account for clinical context (e.g., known treatments vs anomalies).
4. Threshold Sensitivity: Current thresholds for classification (e.g., label counts, YOLO detections) are heuristic and may require refinement for specific datasets.

----------------------------------------------------------------------------------------------------------------------------------------

*Why this detection is important?*

This methodology bridges the gap between raw imaging data and actionable insights in dental radiology. It is particularly significant for:
- Privacy Protection: Identifying high-sensitivity images for secure handling under regulations like HIPAA or GDPR.
- Clinical Decision Support: Assisting in identifying cases requiring detailed review (e.g., anomalies, restorations).
- AI Enhancement: Enabling robust datasets for machine learning applications.

----------------------------------------------------------------------------------------------------------------------------------------

*Dataset*
The dataset used for this project is from Roboflow Universe (link: https://universe.roboflow.com/dentex/dentex-3xe7e/dataset/2), specifically tailored for dental X-ray analysis. It consists of:
- Training Set: 873 images (81%)
- Validation Set: 40 images (4%)
- Test Set: 165 images (15%)

The dataset includes pre-labeled bounding boxes for dental regions, enabling precise detection and classification of biometric patterns.

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
- High Sensitivity: Images containing unique biometric features like missing teeth, anomalies, or restorations (num_labels > 5 or num_yolo_detections > 5 or num_structural_features > 8)
- Moderate Sensitivity: Images with general structures like typical tooth or jaw patterns without distinct anomalies (1 <= num_labels <= 5 or 1 <= num_yolo_detections <= 5 or 3 <= num_structural_features <= 8)
- Low Sensitivity: Images with no identifiable features or only generic patterns 
  
*Visualization:*
- A bar chart visualizes the number of images in each sensitivity category ("High," "Moderate," and "Low").

----------------------------------------------------------------------------------------------------------------------------------------

3) Code Implementation
   
The code processes the panoramic X-rays, classifies their sensitivity, and visualizes the distribution of sensitivity levels. Below are the key components:

*Preprocessing:*
- CLAHE, Gaussian blur, and Canny edge detection for structural analysis.

*Feature Detection:*
- Combined YOLOv8 detections with structural feature analysis.
  
*Sensitivity Classification:*
- Integrated label content to refine classifications.

*Visualization:*
- A bar chart shows the distribution of sensitivity levels across the dataset.
- 
----------------------------------------------------------------------------------------------------------------------------------------

4) Results
   
The dataset was classified into the following sensitivity levels:

- High Sensitivity: Images with unique biometric patterns.
- Moderate Sensitivity: Images with general biometric features.
- Low Sensitivity: Images with no distinguishing patterns.
  
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



