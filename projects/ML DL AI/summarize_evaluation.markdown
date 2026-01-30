---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# layout: default
title: Summarize Evaluation Model
parent: ML DL AI
permalink: /ml_dl_ai/summarize_evaluation
nav_order: 100
---

#  Summarize Evaluation Model
machine learning
{: .badge .badge-pill .badge-primary }
supervised learning
{: .badge .badge-pill .badge-secondary }
evaluation
{: .badge .badge-pill .badge-secondary }


## Key Concepts: TP, FP, FN, TN
For a given class (say “Road”):

- **True positives (TP)**: Predicted positive and are actually positive
- **False positives (FP)**: Predicted positive and are actually negative
- **True negatives (TN)**: Predicted negative and are actually negative
- **False negatives (FN)**: Predicted negative and are actually positive

| Term | Meaning | Example (for class = Road) |
| ----------------------- | ------------------------------------------ | -------------------------- |
| **TP (True Positive)**  | Pixel truly *Road*, predicted *Road*       | A ✅                        |
| **FP (False Positive)** | Pixel *not Road*, but predicted *Road*     | D ❌                        |
| **FN (False Negative)** | Pixel *Road*, but predicted something else | B ❌                        |
| **TN (True Negative)**  | Pixel *not Road*, predicted *not Road*     | C ✅ (for “Road” class)     |


## Metrics Explained (with intuition)

### **Accuracy**
**Meaning:**
Fraction of correctly classified pixels over all pixels.

**Formula:**
Accuracy= (TP+TN)/(TP+TN+FP+FN)

**Interpretation:**
- How many pixels the model got right overall.
- Can be misleading if some classes dominate (e.g. background pixels).

**Layman Example:**
If 95% of your image is background and the model always predicts “background,” accuracy will be 95%, even if it misses all buildings or roads.

| Measures | Best When | Sensitive To |
|-------------------------- |-------------------------- |-------------------------- |
| Overall correctness            | Balanced datasets            | Dominant background |

---

### **Precision**
**Meaning:**
Of all pixels predicted as this class, how many are actually correct?

**Formula:**
Precision=TP​/(TP+FP)

**Interpretation:**
- High precision means few false alarms.
- The model predicts a class only when it is confident.

**Layman Example:**
If you predict 100 “road” pixels and 90 are truly roads, precision = 0.9.

| Measures | Best When | Sensitive To |
|-------------------------- |-------------------------- |-------------------------- |
| How precise predictions are            | You want few false positives (false alarms)            | False Positives (FP) |

---

### **Recall (Sensitivity)**
**Meaning:**
Of all true pixels of this class, how many did the model correctly find? and it focuses on the false negatives.

**Formula:**
Recall=TP/(TP+FN​)

**Interpretation:**
- High recall means most real objects are detected.
- May include more incorrect predictions.

**Layman Example:**
If there are 100 true “road” pixels and you correctly predict 90 of them, recall = 0.9.

| Measures | Best When | Sensitive To |
|-------------------------- |-------------------------- |-------------------------- |
| How complete predictions are   | You want full detection      | False Negatives (FN)                  |

---

### **F1 Score**
**Meaning:**
Balanced measure combining precision and recall.

**Formula:**
F1 = 2×(Precision×Recall)/(Precision+Recall)​

**Interpretation:**
- High only when both precision and recall are high.
- Drops sharply if either precision or recall is low.
- Useful as a single overall metric. Good overall measure when you need both accuracy and completeness.

**Layman Example:**
- Precision = 0.9, Recall = 0.9 → F1 = 0.9
- Precision = 0.9, Recall = 0.5 → F1 = 0.64 — big drop.

| Measures | Best When | Sensitive To |
|-------------------------- |-------------------------- |-------------------------- |
| Balance of precision/recall    | General performance          | Both FP + FN        |

---
### **IoU (Intersection over Union)**
**Meaning:**
How much overlap is there between predicted and actual pixels for a class?

**Formula:**
IoU = TP/(TP+FP+FN)​

**Interpretation:**
- Compares overlap between predicted mask and ground truth mask.
- IoU is the overlap area ÷ combined area.
- Higher IoU → better overlap → more accurate mask.

**Layman Example:**
If your model’s “road” mask overlaps 80% with the true “road” mask, IoU = 0.8.

| Measures | Best When | Sensitive To |
|-------------------------- |-------------------------- |-------------------------- |
| Overlap area | General segmentation quality assessment  | Missing overlap (FP and FN) |

---
### **mIoU (Mean Intersection over Union)**
**Meaning:**
The average IoU across all classes.
**Formula:**
𝑚𝐼𝑜𝑈=1𝑁∑𝑖=1𝑁𝐼𝑜𝑈𝑖

**Interpretation:**
- Compute IoU separately for each class (road, building, vegetation, etc.).
- Take the average across all classes.
- Standard benchmark metric in semantic segmentation.

**Layman Example:**
If IoU for road = 0.8, vegetation = 0.7, building = 0.6 → mIoU = 0.7.

| Measures | Best When | Sensitive To |
|-------------------------- |-------------------------- |-------------------------- |
| Average overlap across classes | Multi-class balance          | Class imbalance     |

---
### **Dice Coefficient (a.k.a. F1 Score for segmentation)**
**Meaning:**
Measures how well the predicted mask overlaps the true mask, giving more weight to overlap than IoU.

**Formula:**
Dice=2TP/(2TP+FP+FN)

**Interpretation:**
- Equivalent to F1 score at the pixel level.
- More sensitive to overlap than IoU.
- Especially effective for small or imbalanced objects.

**Layman Example:**
- If predicted and true masks mostly overlap, Dice is close to 1.
- If they barely overlap, Dice approaches 0.

| Measures | Best When | Sensitive To |
|-------------------------- |-------------------------- |-------------------------- |
| Weighted overlap               | Small object detection       | Small-class errors  |


## More Deep explain for Metrics

| Measure / Plot | Guidance | Explanation |
|-------------------------- |-------------------------- |-------------------------- |
| **Discrimination**  |||
| AUROC               | ✅       | Quantifies discrimination, which is a key component of statistical model performance.  |
| AUPRC, PAUROC               | ❌       | These measures attempt to move beyond a statistical assessment, but violate decision-analytic principles.  |
| ROC curve, PR curve               | -       | These plots provide limited additional information over AUROC.  |

| **Calibration**  |||
| O:E ratio               | -       | An interpretable measure, but only a partial assessment of calibration; essential either for internal validation, O:E ratio is often (close to) 1.  |
| Calibration intercept, calibration slope        | -        | These measures are harder to interpret and provide a partial assessment of calibration; for internal validation, quantifying calibration slope can be used as in indication of overfitting.  |
| ECI, ICI, ECE               | -       | These measures summarize the smoothed (or grouped in case of ECE) calibration plot, concealing the nature and direction of miscalibration.|
| Calibration plot/reliability diagram   | ✅      | This is by far the most insightful approach to assess calibration, in particular when smoothing rather than grouping is used; for internal validation, a plot is preferred but merely reporting the calibration slope is acceptable; for external validation a calibration plot is strongly recommended, with indications of uncertainty, e.g. by 95% confidence intervals.|

| **Overall**  |||
| Loglikelihood, Brier, R2 measures     | -       | These proper measures are fine, yet it makes sense to conduct a separate evaluation of discrimination and calibration. Such measures are more convenient when comparing models, which was not the key focus of this work.|
| Discrimination slope, MAPE  | ❌       | These measures are improper, which means that incorrect models can have better values for these measures than the correct model.  |
| Risk distribution plots  | ✅     | Displaying the distribution of the risk estimates for each outcome category provides valuable insights into a model's behavior.  |

| **Classification**  |||
| Classification accuracy, balanced accuracy, Youden index, DOR, kappa, F1, MCC  | ❌       | These measures are improper at clinically relevant decision thresholds; in addition, some measures are hard to interpret.|
| Sensitivity/recall and specificity  | -       | While improper on their own, they can be reported descriptively if reported together. However, largely theoretical measures as they condition on the outcome that is predicted. |
| PPV/precision and NPV  | -     | While improper on their own, they can be reported descriptively if reported together. PPV and NPV are more practical measures because they condition on the classification. |
| Classification plots  | -     | Classification plots plot could be presented descriptively, showing either sensitivity and specificity or PPV and NPV by threshold. |

| **Clinical Utility**  |||
| NB or standardized NB (with a decision curve), EC (with a cost curve) | ✅   | Important measures to quantify to what extent better decisions are made. Decision curves of NB allow one to show potential clinical utility at various clinically relevant decision thresholds relative to default decisions (and competing models).|