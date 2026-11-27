---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Comparing Geospatial Detection Models
parent: Computer Vision
permalink: /computer vision/cgdm
nav_order: 102
---

#  Geospatial Detection Models
Computer Vision
{: .badge .badge-pill .badge-primary }
Model
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

# Models

## SAM-LoRA
  - **What is SAM-LoRA**: SAM-LoRA combines two ideas:
    - SAM (Segment Anything Model) - a powerful segmentation model developed by Meta AI. It uses a Vision Transformer (ViT) backbone (ViT-B, ViT-L, or ViT-H) to extract image embeddings and a lightweight decoder to produce segmentation masks from prompts (points, boxes, etc).
    - LoRA (Low-Rank Adaptation) - a parameter-efficient fine-tuning method. Instead of updating all SAM’s massive parameters (hundreds of millions), LoRA adds small trainable matrices to certain layers (like attention or MLPs). During fine-tuning, only these LoRA weights are trained - the original SAM weights remain frozen.

  - **Result**: SAM-LoRA enables task-specific fine-tuning (e.g., for land cover, building extraction, crop segmentation, etc.) with very low GPU cost and memory, while retaining SAM’s generalization.

### SAM Backbone: ViT-B, ViT-L, ViT-H
  The “b”, “l”, and “h” refer to base, large, and huge variants of the Vision Transformer backbone.

  | Backbone | Layers | Hidden Dim | Attention Heads | Parameters (encoder only) | Approx. GPU VRAM for inference | Notes |
  |-----------|---------|-------------|------------------|-----------------------------|-------------------------------|-------|
  | **ViT-B** | 12 | 768 | 12 | ~86M | ~8–10 GB | Lightest version, fast training, good for smaller datasets |
  | **ViT-L** | 24 | 1024 | 16 | ~304M | ~16–20 GB | Stronger representation, better mask precision |
  | **ViT-H** | 32 | 1280 | 16 | ~632M | 24–32 GB+ | Best accuracy, expensive compute and memory cost |

  | Feature | **ViT-B** | **ViT-L** | **ViT-H** |
  |----------|------------|------------|------------|
  | Model size | Small (86M) | Medium (304M) | Very large (632M) |
  | Accuracy | Good | Better | Best |
  | Speed | Fastest | Moderate | Slowest |
  | GPU required | ~8-10 GB | ~16-20 GB | ~24-32 GB+ |
  | Fine-tuning cost (with LoRA) | Very low | Moderate | High |
  | Recommended use | Quick prototyping, medium-res images | Complex scenes, high-res land cover | Research-grade, massive datasets, best precision |

  All three backbones follow the same architecture:
  - Patch embedding
  - Transformer encoder (multi-head attention + feed-forward layers)
  - Output image embedding

  The larger ViT models capture more contextual and spatial relationships (useful for complex textures or large scenes), but they are computationally heavier.

### Fine-Tuning Pipeline (Simplified)
  1. Load Pretrained SAM (ViT backbone)
  2. Add LoRA layers
  3. Freeze all base SAM parameters (only LoRA layers train).
  4. Train on your dataset (e.g. remote sensing, medical imagery, etc.)

### Example Use Cases

  | Use Case | Recommended Backbone | Reason |
  |-----------|----------------------|--------|
  | Building footprint extraction (urban) | **ViT-L** | Captures fine boundary + global context |
  | Land cover classification (multiple classes) | **ViT-B** or **ViT-L** | Balances speed and segmentation quality |
  | Tree canopy & vegetation mapping (sub-meter imagery) | **ViT-H** | Captures texture and canopy complexity |
  | Water body or road segmentation | **ViT-B** | Lightweight, sufficient accuracy |


# Dataset

  | YOLO                                                      | SAM                                     |
  | --------------------------------------------------------- | --------------------------------------- |
  | Needs annotated bounding boxes                            | No training dataset needed              |
  | Handles millions of tiles created from large orthomosaics | Uses prompts (point/box) for segmentation |
  | Works best with COCO-like dataset formats                 | Great for polygon masks when annotations don't exist |

# Core Architecture & Algorithm

  | YOLO                                                             | SAM                                     |
  | ---------------------------------------------------------------- | --------------------------------------- |
  | Backbone: CSPNet / Darknet / MobileBackbone depending on version | Backbone: ViT-H (or ViT-B/L for smaller variants)  |
  | Neck: PANet / BiFPN                                              | Image encoder → Prompt encoder → Mask decoder      |
  | Head: Anchor-free / Decoupled head                               |                                                    |
  | Predicts (x, y, w, h, class) directly in one shot                | Creates high-quality masks even without training   |
  | Strong for small-object detection in GSD < 10 cm imagery         | Ideal for extracting building footprints, roads, water bodies  |
  | Tile-based inference works extremely well                        |                                                    |

  - YOLO
    - Detection-first
    - Lightweight
    - Real-time
    - YOLOv8/v9 extremely optimized
    - Supports batch tile processing
    - For detection-heavy geospatial projects: YOLO wins.
    - Fast, light, scalable, and perfect for millions of tiles.

  - SAM
    - Segmentation-first
    - Heavy
    - High-quality masks
    - ViT-H backbone is heavy
    - Intense for wide tiles
    - Best for offline analysis
    - For high-quality segmentation: SAM wins.
    - Cleaner masks, zero labeling, ideal for urban planning & agriculture analytics.

## Use-Cases

  | YOLO                                                                                                | SAM                                                                                           |
  | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
  | **Agriculture**: Weed detection, fruit counting, crop gaps, machinery/cattle detection, spraying QC | **Agriculture**: Field boundaries, leaf/canopy masks, disease patches, plot polygons              |
  | **Urban**: Water tanks, vehicles, rooftop solar, encroachment, utility assets                       | **Urban**: Building footprints, roads, slum boundaries, tree canopy, water bodies                 |
  | **Infrastructure**: Poles/towers, road assets, construction progress, pipeline/bridge object checks | **Infrastructure**: Roof/road/bridge masks, drainage & railway corridor segmentation              |
  | **Environment**: Tree counting, wildlife spotting, waste detection, flood debris, mining objects    | **Environment**: Riverbanks, wetlands, forest cover, mining areas, flood extents, landslide scars |


## U-Net vs SAM

  | Concept | U-Net | SAM-LoRA |
  |--------|-------|----------|
  | Thinking level | A kid learning from scratch | A grown adult with massive prior knowledge |
  | Training data required | A lot, usually domain-specific | Small amount (LoRA fine-tuning) because SAM already knows much |
  | Model size | Small to medium | Extremely large (SAM backbone) but LoRA only adds tiny layers |
  | Accuracy on hard edges | Medium | Very high |
  | Generalization | Low (task-specific) | High (SAM was pretrained on huge datasets) |
  | Training cost | Cheap | Moderate (LoRA is cheap, but SAM is huge) |
  | Use case | Classic segmentation tasks | High-quality, adaptable segmentation |

