---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: MNF and PPI
parent: Geospatial
permalink: /geospatial/mnf_ppi
nav_order: 26
---

# MNF and PPI

geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
model
{: .badge .badge-pill .badge-info }
optimization
{: .badge .badge-pill .badge-info }

* Do not remove this line (it will not be displayed)
{:toc}

## Introduction
Minimum Noise Fraction (MNF) and Pixel Purity Index (PPI) are commonly used together in hyperspectral and multispectral spectral analysis to identify representative spectral signatures. The methods address different stages of the same problem: 
1. Improve the quality and structure of the spectral data
2. Identify pixels that may represent distinct materials

**MNF reduces noise and spectral dimensionality**; **PPI identifies candidate spectrally pure pixels**. 

In a Sentinel-2 vegetation and sand analysis, for example, MNF can reduce the spectral information to the most useful components before PPI searches for extreme pixels. The resulting candidate pixels can then be mapped back to the original Sentinel-2 bands and evaluated as potential objects endmembers. This workflow is commonly used because dimensionality reduction can reduce noise and computational cost before PPI-based endmember identification

## Goals
The objective is not simply to reduce the number of raster bands. The objective is to improve the quality of the spectral information and then identify pixels that are likely to represent relatively pure surface materials.

The combined workflow is particularly useful when the next stage requires spectral endmembers, such as spectral unmixing, material classification, or fractional cover estimation.

The basic process is:

> Original imagery → MNF → selected MNF components → PPI → candidate pure pixels → spectral interpretation → endmembers

**MNF addresses the quality and dimensionality of the spectral data**

**PPI addresses the identification of spectrally extreme pixels**

These are different problems and should not be treated as the same operation.

## What MNF does
MNF stands for Minimum Noise Fraction. It is also commonly described as a Noise-Adjusted Principal Components (NAPC) transformation.

Traditional PCA orders components according to variance. MNF instead considers the relationship between signal and noise and orders the transformed components according to image quality or signal-to-noise characteristics. The original MNF work was introduced by Green et al. in 1988.

In practical terms, MNF answers this question:
> Which spectral dimensions contain useful information, and which dimensions are dominated by noise?

MNF transforms helps retain meaningful spectral information while reducing the influence of noisy components and unnecessary dimensions. This matters because remotely sensed data often contains correlated bands and sensor noise. Some later components may contain little useful surface information but still increase computational cost and affect downstream analysis.

MNF transforms the original spectral space into a new coordinate system:

```
    B2 B3 B4 B5 B6 B7 B8 B8A 
            │ 
            ▼ MNF 
            │ 
            ├── MNF 1 High information 
            ├── MNF 2 High information 
            ├── MNF 3 Useful information 
            ├── MNF 4 Useful / moderate 
            ├── MNF 5 Lower signal 
            ├── ... 
            └── MNF 8 Potentially noise dominated
```

The first MNF components normally contain the strongest signal relative to noise. Later components generally contain less useful information, although the exact behaviour depends on the dataset and noise estimation.

## Why MNF is useful
MNF provides three main benefits.
1. **Noise reduction**: MNF separates information according to signal-to-noise characteristics. This makes it possible to exclude components dominated by noise before performing subsequent analysis. The decision to exclude components should be supported by eigenvalues, SNR, spatial appearance, and spectral behaviour rather than by component number alone.
2. **Dimensionality reduction**: Multispectral and hyperspectral bands are often correlated. MNF converts the original bands into a smaller set of transformed components. E.g. from 8 bands -> * components (MNF) -> 3 components (selected).
3. **Improving downstream spectral analysis**: E.g. if using PPI operates in a multidimensional spectral space. If that space contains substantial noise, random projections can identify pixels because of noise rather than because they represent meaningful surface materials. Using informative MNF components before PPI reduces this problem.

## What PPI does
PPI stands for Pixel Purity Index. It is an endmember candidate extraction technique. It searches for pixels that are located at the extremes of the spectral data distribution.

The basic assumption is straightforward:

> Pixels dominated by a single material are more likely to occur at the extremes of the spectral feature space than pixels containing mixtures of several materials.

PPI repeatedly projects pixels onto random directions and records pixels that occur at the extremes of those projections. Pixels receiving high PPI scores become candidates for spectrally pure or distinctive materials. After many iterations, pixels that repeatedly appear as extremes accumulate higher scores.

This distinction matters because a high PPI score does not automatically mean that a pixel is physically pure. A high-scoring pixel may represent vegetation, sand, soil, water, shadow, or another spectrally distinctive material. The selected pixels must therefore be inspected using their original spectral signatures and spatial context.

## Why PPI is useful
1. **Simple endmember candidate extraction**: PPI provides an objective way to identify spectrally extreme pixels.
2. **Does not require labelled training data**: The method does not require a predefined vegetation, sand, soil, or water training dataset.
3. **Works in multidimensional spectral space**: PPI can use several MNF components simultaneously.
4. **Useful before spectral unmixing**: Candidate pure pixels can provide initial endmembers for subsequent unmixing methods.

## Why combine MNF and PPI?
Using PPI directly on the original spectral bands can work, but it is not always the best approach.

The original data may contain:
- redundant bands
- atmospheric effects
- sensor noise
- correlated spectral information
- irrelevant spectral dimensions
- low-information components

MNF first transforms the data into a noise-aware feature space. PPI then operates on the selected MNF components.

## PPI thresholding
The PPI output itself does not identify vegetation, sand, soil, or other materials.It only gives each pixel a purity score. For example:

PPI score 
- 0 → rarely an extreme pixel 
- 100 → occasionally extreme 
- 500 → frequently extreme 
- 5000 → repeatedly extreme

A threshold can then be applied to identify candidate pixels. For example, using the 99.9th percentile, This selects approximately the highest 0.1% of PPI scores.

The result of PPI is a binary raster:
- False → not selected
- True  → candidate pure pixel

This should be interpreted as a candidate mask, not a definitive material classification. A pixel with a high PPI score is spectrally extreme. It is not automatically a physically pure vegetation or sand pixel.

## Limitations
### MNF limitations
- **Noise estimation affects the result**: If the estimated noise covariance does not represent the actual image noise, the component ordering may not be reliable.
- **MNF does not create new physical information**: MNF is a mathematical transformation. It does not recover information that is absent from the sensor data.
- **Component selection requires judgement**: An arbitrary rule such as "always keep the first three components" is not universally valid. Component selection should consider SNR, eigenvalues, spatial coherence, and the objective of the analysis.
- **Sensitive to preprocessing**: Clouds, shadows, atmospheric contamination, saturated pixels, water adjacency, and invalid pixels can affect the statistics. Quality masking should occur before MNF.

### PPI limitations
- **High PPI does not guarantee physical purity**: PPI identifies spectral extremes. It does not know whether an extreme pixel represents vegetation, sand, soil, water, building material, or noise.
- **Results depend on the number of iterations**: More iterations generally provide a more stable PPI estimate, but increase processing time. The appropriate value depends on image size and spectral dimensionality.
- **Threshold selection is subjective**: A 99.9th percentile threshold is a practical starting point, not a universal standard. Different scenes may require different thresholds.
- **Mixed pixels can still be selected**: A mixed pixel can be spectrally extreme relative to the rest of the image. Therefore, PPI candidates require validation.
- **Spatial context is not the primary criterion**: PPI operates on spectral characteristics. It does not inherently understand object boundaries, land-cover geometry, or spatial semantics.

## Use case MNF + PPI
The method is particularly appropriate when the project needs to identify spectral endmembers.

| Application                 | Purpose                                               |
| --------------------------- | ----------------------------------------------------- |
| Vegetation analysis         | Identify representative vegetation spectra            |
| Soil and sand mapping       | Identify exposed soil and sand endmembers             |
| Mineral mapping             | Identify candidate mineral spectra                    |
| Hyperspectral analysis      | Reduce noisy spectral dimensions                      |
| Spectral unmixing           | Generate initial endmembers                           |
| Fractional vegetation cover | Estimate vegetation abundance                         |
| Urban material analysis     | Identify concrete, asphalt, roof, and other materials |
| Wetland mapping             | Separate vegetation, water, soil, and sediment        |
| Geological mapping          | Identify spectrally distinct surface materials        |
| Change analysis             | Compare material-specific spectral responses          |

# Code

## Data
For this example, we load 2 raster image and combine them into a multilayer raster and treat them as a input data for MNF and PPI process.

```python
with rasterio.open("output.tif") as src:
    cube_1 = src.read().astype(np.float32)
    profile = src.profile.copy()
print(cube_1.shape)

with rasterio.open("lst_celsius.tif") as src:
    cube_2 = src.read().astype(np.float32)
    profile = src.profile.copy()
print(cube_2.shape)

cube = np.concatenate([cube_1, cube_2], axis=0)
print(cube.shape)
```

These are the dimension of both raster and a multilayer raster with format (channel, row, column).

```
(1, 1200, 1200)
(1, 1200, 1200)
(2, 1200, 1200)
```

## MNF code
First, we get multilayer raster and feed that into MNF code, with parameters that support our analysis to distinct between signal and noise.

```python
MNF_selected, mnf_values, mnf_transform_matrix = maps.mnf(main_data, type='spectral', n_components=5, snr=5)
```

This function requires the following parameters:
- **main_data** (`array`):      Multilayer raster in numpy array format
- **type** (`string`):          Decide using custom and spectral library ["custom","spectral"]
- **n_components** (`int`):     number of components to reduce data dimensionality while preserving signal quality
- **snr** (`int`):              Threshold signal-to-noise ratio (SNR) to retain.

### Result

```python
shape of valid mask: (1200, 1200)
shape of data: (98518, 2)
noise shape: (2, 2)
[[4.64031454e+02 9.28062765e+00]
 [9.28062765e+00 1.85612525e-01]]
noise shape: (98518, 2)
```

## PPI code
From MNF process, we get multilayer raster in numpy array from MNF output. This data could be an input as PPI code, to Calculate Pixel Purity Index and determine endmember pixel from the raster.

```python
ppi_raster = maps.ppi(main_data, MNF_selected, type='spectral', thres=99.9, threshold_value=2.5, niters=1000)
```

This function requires the following parameters:
- **main_data** (`array`):      Multilayer raster in numpy array format
- **MNF_selected** (`array`):      the output from MNF process
- **type** (`string`):          Decide using custom and spectral library ["custom","spectral"]
- **thres** (`float`):     a treshold value to distince between common pixel with endmember pixel
- **threshold_value** (`float`):              If this value is zero, only the two most extreme pixels will have their indices incremented for each random vector. If the value is greater than zero, then all pixels whose projections onto the random vector are with threshold data units of either of the two extreme pixels will also have their indices incremented.
- **niters** (`int`):     Number of iterations to perform. Each iteration corresponds to a projection of the image data onto a random unit vector.

### Result

<img src="/assets/images/geospatial/mnf_ppi/mnf_ppi_01.webp" alt="drawing"/>