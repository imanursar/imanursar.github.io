---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: How to improve Deep Learning result?
parent: ML DL AI
permalink: /ml_dl_ai/improve_dl
nav_order: 101
---

#  How to improve Deep Learning result?
Deep Learning
{: .badge .badge-pill .badge-primary }
Machine Learning
{: .badge .badge-pill .badge-secondary }
optimization
{: .badge .badge-pill .badge-secondary }

<img src="/assets/images/ml_dl_ai/improve/improve_01.webp" alt="drawing" width="500"/>


To unlock high-accuracy models in geospatial AI, we must look beyond just training. A successful model is built on solid preparation—from data preprocessing to smart label design and model selection. In This page, we will introduce some techniques how to improve our Deep Learning result from end-to-end process. Additionally, we will also discuss about How to measure the detected object? especially for round objects from remote sensing such as palm tree.


## Simple Deep Learning Development 

<img src="/assets/images/ml_dl_ai/improve/improve_02.webp" alt="drawing"/>


## Preprocessing
Data quality of input data sets the ceiling for model performance. Preprocessing ensures our imagery is clean, consistent, and focused before training. Especially important when training on remote sensing imagery with varying acquisition conditions.

<img src="/assets/images/ml_dl_ai/improve/improve_04.webp" alt="drawing" width="500"/>

**Examples**:​
- Normalize imagery (e.g., same resolution, scale, CRS).​
- Remove irrelevant information (clouds, shadows, no-data areas).​
- Clip and tile imagery for manageable input sizes (e.g., 256x256, 512x512).​
- Apply feature engineering, such as smoothing, sharpening, or color corrections if needed.​
- Radiometric correction​

## Feature Engineering – Elevating Model Understanding​
Raw RGB imagery often isn't enough. Feature engineering gives our model more context. By incorporating additional bands, we help the model focus on traits that separate we target object from its background. More meaningful features lead to more onfident predictions.

<img src="/assets/images/ml_dl_ai/improve/improve_05.webp" alt="drawing" width="500"/>

**Examples**:​
- Adding vegetation indices or terrain-derived layers (NDVI, GNDVI as extra channels) to better highlight objects like trees, water, or buildings.​
- Derive texture metrics using focal statistics, histogram equalization, clustering pixel image or edge detection.​
- Add non-visual band (e.g. NIR) 

**2 Geoprocessing tools that we can use in ArcGIS Pro namely:​**
- [Iso Cluster Unsupervised Classification](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/spatial-analyst/iso-cluster-unsupervised-classification.htm):
    Performs unsupervised classification on a series of input raster bands using the Iso Cluster and Maximum Likelihood Classification tools.​

- [Segment Mean Shift](https://pro.arcgis.com/en/pro-app/3.4/tool-reference/image-analyst/segment-mean-shift.htm):
    Groups adjacent pixels that have similar spectral characteristics into segments.​
Each output raster from above tools can be combine with original raster using `CompositeBands` tools.​


## Choosing the Right Model Type​

- **Object detection**

Object detection is the process of locating features in an image. The model be able to detect the location of different objects. This process typically involves drawing a bounding box around the features of interest. 

<img src="/assets/images/ml_dl_ai/improve/improve_06.webp" alt="drawing" width="500"/>

- **Semantic segmentation​**

Semantic segmentation occurs when each pixel in an image is classified as belonging to a class. In GIS, this is often referred to as pixel classification, image segmentation, or image classification.

<img src="/assets/images/ml_dl_ai/improve/improve_07.webp" alt="drawing" width="500"/>

- **Instance segmentation​**

Instance segmentation is a more precise object detection method in which the boundary of each object instance is drawn. This type of deep learning application is also known as object segmentation.

<img src="/assets/images/ml_dl_ai/improve/improve_08.webp" alt="drawing" width="500"/>

Different deep learning tasks solve different problems. Choosing the right model type ensures we’re solving ours efficiently. ArcGIS supports various deep learning models—U-Net, Mask R-CNN, and YOLO—each with strengths depending on our task. Choosing the right backbone, like ResNet or MobileNet, lets we balance performance with processing speed.

**Examples**:​
- Object Detection (YOLO, Faster R-CNN): Output = bounding boxes.​
- Semantic Segmentation (U-Net, DeepLab): Output = class per pixel.​
- Instance Segmentation (Mask R-CNN): Output = individual object masks.​

**In example for each model type:​**
- Object detection ​
  - [Faster R-CNN](https://developers.arcgis.com/python/latest/guide/faster-rcnn-object-detector/)
  - [Single-shot detector (SSD)​](https://developers.arcgis.com/python/latest/guide/how-ssd-works/)
  - [YOLOv3​](https://developers.arcgis.com/python/latest/guide/yolov3-object-detector/)
  - [RetinaNet​](https://developers.arcgis.com/python/latest/guide/how-retinanet-works/)
- Semantic segmentation​
  - [U-net​](https://developers.arcgis.com/python/latest/guide/how-unet-works/)
  - [SamLoRA​](https://developers.arcgis.com/python/latest/guide/finetune-sam-using-samlora/)
- Instance segmentation​
  - [Mask R-CNN​​](https://developers.arcgis.com/python/latest/guide/how-maskrcnn-works/)

​
## Training Data Variability Analysis ​
Before labeling or training, we need to visually analyze the diversity of the objects and environments across the imagery. This helps ensure the model sees enough variation to generalize.

<img src="/assets/images/ml_dl_ai/improve/improve_10.webp" alt="drawing" width="500"/>

**Examples**:​
- Examine imagery across regions and time​
- Identify intra-class variability: object size, shape, orientation, illumination, background complexity.​
- Palm trees may look different in highland vs lowland terrain or on different soil types.​
- Use Export Training Data for Deep Learning to sample image chips and view in a mosaic.​


## Clear and Consistent Labels​
Even the best model will underperform if our labels are inconsistent. Avoid overlapping or ambiguous polygons. Label edges cleanly and follow class definitions strictly. This builds a reliable ground truth that the model can learn from with confidence.

<img src="/assets/images/ml_dl_ai/improve/improve_11.webp" alt="drawing" width="500"/>

**Examples**:​
- Avoid overlapping, duplicated, or imprecise labels.​
- Match labels to model type (bounding box for detection, polygons for segmentation).​
- Keep class definitions tight and documented.​
- Use Label Objects for Deep Learning, refine with Snapping, Edit Vertex, and Topology tools to maintain clean geometries.​


## Labeling - One Model, One Variant​
When object appearances vary widely—for example, young vs mature palm trees—it’s often best to train separate models for each variant. This approach is effective for high intra-class variability.

<img src="/assets/images/ml_dl_ai/improve/improve_12.webp" alt="drawing" width="500"/>

**Examples**:​
- Isolate object variants with distinct shapes, colors, or patterns.​
- Train separate models for each variant to increase precision.​
- Train one model for young palm trees and another for mature palms due to canopy shape and size differences.​
- Use separate folders for each model's training dataset. ​


## Labeling - All Variants, Single Label​
If our task doesn't require distinguishing between subtypes, combining variants under one label simplifies training and deployment. This reduces labeling complexity and model size. But this also reduce accuracy and precision.

<img src="/assets/images/ml_dl_ai/improve/improve_13.webp" alt="drawing" width="500"/>

Examples:​
- Merges all object appearances into a single class.​
- All types of palm trees are labeled as one class for simple plantation mapping.​
- Set all labels to a single class code (e.g., `palm_tree = 1`) during Export Training Data for Deep Learning. Use fewer classes to reduce training complexity.


## Labeling - All Variants, Different Labels​
When classifying object subtypes matters, each variant needs its own label. This enables the model to differentiate with greater detail. This helps the model distinguish fine-grained differences and adds classification value to your output.

<img src="/assets/images/ml_dl_ai/improve/improve_14.webp" alt="drawing" width="500"/>

**Examples**:​
- Label each subtype: `palm_tree`, `palm_tree_medium`, and `palm_tree_crowded`.​
- Include a class_value attribute in the label dataset. Use multi-class detection or segmentation during training by setting class mapping


## Importance of Including All Variability​
A model can only learn what it has seen. If key variations are missing from the training data, even the best architecture will fail to generalize. 

<img src="/assets/images/ml_dl_ai/improve/improve_15.webp" alt="drawing" width="500"/>

**Examples**:​
- Include edge cases: occlusions, different orientations, partial shadows.​
- Avoid over-representation from one scene (e.g., all samples from the same plantation). ​
- Stratified sampling by region, types, and ages type before labeling.​


## Transfer Learning​
Transfer learning allows you to stand on the shoulders of giants. Start with a pretrained model and fine-tune it to your data. In ArcGIS, we can load a pretrained model and fine-tune it to your specific dataset. 

<img src="/assets/images/ml_dl_ai/improve/improve_16.webp" alt="drawing" width="500"/>

Example:​
- Use multiple milestones (e.g. difference labels type, difference region) that train and evaluate single model for each milestone use pretrained weights from previous milestone.​
- Use **Train Deep Learning Model** with `pretrained_model` parameter to load them.


## Additional Best Practices​
Beyond those techniques, a few small strategies can make a big difference in model reliability and real-world performance

<img src="/assets/images/ml_dl_ai/improve/improve_17.webp" alt="drawing" width="500"/>

**Examples**:​
- Use **data augmentation**: rotation, flips, noise, brightness.​
- Retrain iteratively after error analysis (e.g. add more training samples from misses objects, and retrain.)​
- Visualize **confidence maps** to spot uncertain predictions. Turn on `confidence raster output` in **Classify Pixels Using Deep Learning** or **Detect Objects Using Deep Learning**. Use it in error inspection workflows.​


## How to Optimize Our Inference Process​
The processing time for deep learning in ArcGIS depends on several key factors:​
​
- Tile size or image resolution used during both training and inference.​
- Hardware specifications of the device in use.​
- GPU capabilities (e.g., VRAM size, processing speed).​
- Disk read/write performance.​
- Selected model architecture and backbone (e.g., ResNet, MobileNet).​
- Batch size settings for prediction and training.​
- Concurrent system load, such as other applications running alongside ArcGIS Pro.

<img src="/assets/images/ml_dl_ai/improve/improve_18.webp" alt="drawing" width="500"/>

Example Performance Metrics (Using NVIDIA RTX A2000 12GB ≈ RTX 3060)​:

​- **Object Detection​**
  - Training: ≈ 2 – 3 hours.​
  - Inference: ≈ 30 minutes to 1 hour.​

- **Semantic or Instance Segmentation​**
  - Training: ≈ 1 – 2 days.​
  - Inference: ≈ 2 – 3 hours.​


## Trade-Off between Cost vs Quality ​

<img src="/assets/images/ml_dl_ai/improve/improve_19.webp" alt="drawing"/>


## Model Limitations & Failure Zones​
Even with strong training, deep learning models can fail—especially in unseen conditions. Knowing where and why this happens is key to improvement.

<img src="/assets/images/ml_dl_ai/improve/improve_20.webp" alt="drawing"/>20

**Examples**:​
- Causes: unseen backgrounds, poor lighting, extreme object deformation.​
- Visualize errors using prediction overlays and confidence maps.​
- Flag and relabel failure zones for retraining (closed feedback loop) and to guide future labeling.


## Final and Complete Deep Learning Development 

<img src="/assets/images/ml_dl_ai/improve/improve_03.webp" alt="drawing"/>


## How to measure the detected object?​

- [Using Minimum Bounding Geometry​](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/minimum-bounding-geometry.htm)
​
  Creates a feature class containing polygons which represent a specified minimum bounding geometry enclosing each input feature or each group of input features.​


- Using **custom script**:

  - Calculate boundary area coverage​
  - Measure the center point of boundary area​
  - Measure the radius from the area ​(radius = math.sqrt(area / pi))​
  - Utilize buffer with center point and radius to create circle


## Final Thoughts

By applying structured practices—clear labeling, preprocessing, feature engineering, and leveraging transfer learning—we turn GIS deep learning from experimental to production-ready. The ArcGIS ecosystem gives us the full pipeline to do this efficiently.

Deep learning in GIS is both art and science. It takes thoughtful preparation, the right tooling in ArcGIS, and iterative refinement. With these principles, your model’s performance will go beyond expectations.