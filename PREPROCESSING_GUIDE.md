# Data Preprocessing Guide

This guide describes the methodology used to prepare microscopy images for training the Detectron2 model.

## Overview

The preprocessing pipeline converts raw microscopy images into COCO-format annotations suitable for instance segmentation training.

**Pipeline**: Raw Images → Manual Annotation → Binary Masks → COCO JSON → Training Dataset

## Image Preparation

### Image Acquisition

Microscopy images specifications used for this study (but can be adapted according to the objectives):
- Modality: Bright-field microscopy
- Subject: Brain organoids
- Format: JPEG
- Resolution: 519×693 pixels
- Bit depth: 8-bit
- Color: RGB

### Image Standardization

All images must be standardized to consistent dimensions. Original high-resolution images have been resized to 519×693 pixels.

## Annotation Methodology

### Tool: FIJI/ImageJ

Manual annotation is performed using FIJI (Fiji Is Just ImageJ), an open-source image processing platform.

**Download**: https://fiji.sc/

### Annotation Process

**Load Image**: Open the microscopy image in FIJI.

**Define Boundaries**: Using selection tools (Freehand or Polygon), manually trace the complete boundary of each organoid visible in the image.

**Create Binary Mask**: Convert the selection to a binary mask where white pixels (value 1) represent the organoid region and black pixels (value 0) represent the background.

**Save Mask**: Save the binary mask as an 8-bit JPEG with a consistent naming convention matching the original image filename.

### Annotation Guidelines

Consistency principles:
- Maintain uniform edge definition across all images
- Include or exclude boundary pixels consistently
- Handle overlapping or touching organoids using the same approach throughout
- Exclude out-of-focus or low-quality organoids

Quality standards:
- Clear, continuous boundaries
- No gaps or holes in masks
- Accurate representation of organoid shape
- Consistent annotation across similar cases

## COCO Format Conversion

### Mask to Polygon

Binary masks must be converted to polygon coordinates for COCO format compatibility.

Process:
1. Extract contours from binary mask
2. Identify largest contour (primary organoid)
3. Approximate polygon to reduce point count
4. Flatten coordinates to sequential list format

Output format: [x1, y1, x2, y2, ..., xn, yn]

### COCO JSON Structure

The COCO annotation file contains three main sections:

**Images**: Metadata for each image including filename, dimensions, and unique ID.

**Annotations**: Segmentation data for each organoid including polygon coordinates, bounding box (x, y, width, height), area, category ID, and image ID reference.

**Categories**: Class definitions. For this project: {"id": 1, "name": "organoid"}

### Dataset Organization

The final dataset structure:

```
organoid/
├── train/
│   ├── [images].jpg
│   └── via_region_data.json
├── val/
│   ├── [images].jpg
│   └── via_region_data.json
└── class_names.json
```

Split ratio: 80% training, 10% validation and 10% test

## File Structure Requirements

### class_names.json

Contains category definitions:
```
{
  "1": "class_1"
}
```

### via_region_data.json

COCO-format annotation file containing complete image and annotation metadata. Generated for both training and validation sets separately.

## Quality Control

### Validation Checks

Before training, verify:
- All images have corresponding annotations
- Polygon coordinates are valid (minimum 3 points)
- No duplicate image IDs
- All referenced images exist in the directory
- Bounding boxes fall within image dimensions
- Category IDs match class definitions

## Creating Your Own Dataset

To train a custom model:

1. Acquire microscopy images of your target objects
2. Standardize image dimensions and format
3. Annotate using FIJI/ImageJ to create binary masks
4. Convert masks to COCO polygon format
5. Organize into train/val directories
6. Create class_names.json file
7. Validate dataset structure and annotations

Implementation details and conversion scripts are available in the project notebooks.

## Additional Resources

- FIJI/ImageJ: https://fiji.sc/
- COCO Format Specification: https://cocodataset.org/#format-data

## Contact

For questions regarding data preparation:

**Email**: fontanieraxelpro@gmail.com
