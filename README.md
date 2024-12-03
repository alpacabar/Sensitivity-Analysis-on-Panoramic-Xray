_Classifying Sensitivity in Panoramic X-rays_

I am classifying the sensitivity of panoramic X-rays based on biometric patterns in the images rather than text content (which may be unnatural). This approach uses image processing and feature detection techniques to identify patterns such as:

- Unique tooth structures: Specific arrangements, missing teeth, or dental restorations.
- Jawbone anomalies: Distinct or rare bone patterns.
- Sinus patterns: Unique sinus shapes.
- Metadata, such as personally identifiable information (PII) if available.

----------------------------------------------------------------------------------------------------------------------------------------
*How trustworthy is this detection?*

1. Preprocessing Enhances Detection: Contrast enhancement (CLAHE), noise reduction, and edge detection improve the visibility of features, allowing both contour analysis and YOLO to work effectively.
2. YOLO: YOLO (You Only Look Once) is a state-of-the-art object detection model designed for real-time and robust detection tasks.
Fine-tuning YOLO on a dental dataset (like your panoramic X-rays) improves its ability to identify anomalies, restorations, and structural patterns.
3. Combination of Structural and YOLO Features: Combining contour-based detection (structural features) with YOLO ensures a balance between simple geometric feature extraction and deep learning-driven insights.

However, there are few limitations that require attention:
1. Model Dependence: The trustworthiness of YOLO detections depends heavily on the quality and diversity of the training dataset. If the model isn't well-trained on panoramic X-rays, false positives or missed detections are more likely.
2. Simplistic Structural Analysis: Contour-based detection relies on edge clarity, which can be affected by noise or poor image quality, leading to either under-detection or over-detection of features.
3. No Context Awareness: The classification doesn’t account for clinical context (e.g., is a missing tooth part of a known treatment or an anomaly?).
4. Threshold Sensitivity: The sensitivity thresholds for "High," "Moderate," and "Low" are heuristic and might need adjustment for different datasets or clinical needs.

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



