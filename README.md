_Classifying Sensitivity in Panoramic X-rays_

This project classifies the sensitivity of panoramic X-rays by analyzing biometric patterns in the images. Unlike approaches that rely on text content (which may feel unnatural), this method leverages advanced image processing and feature detection techniques to identify patterns such as:

Unique tooth structures: Specific arrangements, missing teeth, or dental restorations.
Jawbone anomalies: Rare or distinctive jawbone patterns.
Sinus patterns: Unique sinus shapes or structures.
Class-specific anomalies: Features like caries, deep caries, impacted teeth, and periapical lesions based on labeled data.

----------------------------------------------------------------------------------------------------------------------------------------

*How trustworthy is this detection?*

1. Preprocessing Enhances Detection: Techniques like CLAHE, Gaussian blur, and Canny edge detection improve edge visibility and feature clarity, ensuring robust structural analysis.
2. YOLO: YOLOv8, a state-of-the-art object detection model, reliably detects features when fine-tuned on a dental dataset, capturing patterns such as caries, lesions, and restorations.
3. Integration of Features: Combines structural contour-based features with YOLO detections and labeled classes to ensure comprehensive sensitivity classification.

However, there are few limitations that require attention:
1. Model Dependence: YOLO detections rely on the quality and diversity of the training dataset. Insufficient or biased training can lead to false positives or missed detections.
2. Simplistic Structural Analysis: Contour-based detection depends on edge clarity and can falter with noisy or low-quality images.
3. Class Context: While labels classify anomalies, sensitivity analysis does not yet factor in the clinical significance of specific features (e.g., distinguishing between mild and severe lesions).
4. Threshold Sensitivity: Heuristic thresholds (e.g., number of labels or structural features) may require refinement for different datasets or clinical contexts.

----------------------------------------------------------------------------------------------------------------------------------------

*Why this detection is important?*

This methodology bridges the gap between raw imaging data and actionable insights in dental radiology. It is particularly significant for:
- Privacy Protection: Identifying high-sensitivity images for secure handling under regulations like HIPAA or GDPR.
- Clinical Decision Support: Assists in flagging cases that require deeper review, such as those with anomalies or rare restorations.
- AI Enhancement: Facilitates the creation of high-quality datasets for training robust machine learning models.

----------------------------------------------------------------------------------------------------------------------------------------

*Dataset*
The dataset used for this project is from Roboflow Universe (link: https://universe.roboflow.com/dentex/dentex-3xe7e/dataset/2), specifically tailored for dental X-ray analysis. It consists of:
- Training Set: 873 images (81%)
- Validation Set: 40 images (4%)
- Test Set: 165 images (15%)

The dataset is labeled with bounding boxes and class annotations for:
- Caries (Class 0)
- Deep Caries (Class 1)
- Impacted (Class 2)
- Periapical Lesion (Class 3)

These annotations enable precise classification and analysis.

----------------------------------------------------------------------------------------------------------------------------------------

2) Methodology
   
*Preprocessing:*
- Contrast Enhancement: Applied CLAHE to enhance feature visibility.
- Noise Reduction: Used Gaussian blur to reduce noise while retaining critical details.
- Edge Detection: Applied Canny edge detection to extract structural features.

*Feature Detection:*
- Structural Features: Detected edges and contours (e.g., teeth, jaws, and sinuses) as bounding boxes.
- Deep Learning Detections: YOLOv8 was fine-tuned to detect anomalies like caries, lesions, and restorations.
  
*Sensitivity Classification:*
- High Sensitivity: Images containing distinct patterns such as multiple anomalies or restorations (e.g., num_labels > 5, num_yolo_detections > 5, or num_structural_features > 8).
- Moderate Sensitivity: Images with general patterns like typical teeth or jaw alignment (e.g., 1 <= num_labels <= 5 or 1 <= num_yolo_detections <= 5 or 3 <= num_structural_features <= 8).
- Low Sensitivity: Images with generic or no identifiable features.
  
*Visualization:*
- Visualized results with bounding boxes:
   - Green: Structural features (contours).
   - Blue: YOLO-detected features (e.g., anomalies or restorations).
- Bar chart of sensitivity distributions.

----------------------------------------------------------------------------------------------------------------------------------------

3) Code Implementation
   
The code includes the following components:

*Preprocessing:*
- Applied CLAHE, Gaussian blur, and Canny edge detection for structural feature extraction.

*Feature Detection:*
- Combined structural features with YOLOv8 detections for anomaly detection.

*Label Analysis:*
- Incorporated label content and class counts to refine sensitivity classification.
  
*Sensitivity Classification:*
- Classifies images into "High," "Moderate," or "Low" sensitivity using thresholds based on structural features, YOLO detections, and label content.

*Visualization:*
- Displays structural and YOLO detections along with a bar chart of sensitivity levels.

----------------------------------------------------------------------------------------------------------------------------------------

4) Results
   
- High Sensitivity: Images with dense and unique biometric features, such as anomalies or restorations.
- Moderate Sensitivity: Images with identifiable patterns but less unique content.
- Low Sensitivity: Generic images with minimal identifiable features.

A bar chart visualizes the sensitivity distribution across the dataset.

----------------------------------------------------------------------------------------------------------------------------------------

*Dependencies*

Programming Language: Python

Libraries:
- torch: For PyTorch-based computations.
- ultralytics: For YOLOv8 model detection.
- opencv-python: For image processing tasks.
- matplotlib: For data visualization.
- numpy: For numerical computations.
- Pillow: For image handling.
- scipy: For optimization tasks.

xoxo

