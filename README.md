# SPAOM 2026 Community Workshop 6

## QuPath: A Great Tool for Spatial Omics Image and Data Analysis
### Part I · Multiplexed immunofluorescence Image Analysis​

This repository contains the materials for **SPAOM 2026 Community Workshop 6**, a hands-on introduction to multiplexed fluorescence image analysis in QuPath.

The practical exercise covers:

- creation and use of a QuPath project;
- cell segmentation with the Cellpose extension;
- import of pre-generated Cellpose detections from GeoJSON;
- marker-based cell phenotyping;
- supervised object classification;
- threshold-based and supervised tumor detection;
- distance-to-tumor and nearest-neighbor spatial analysis;
- Extra: visualization of spatial measurements with histograms and scatter plots.

## Repository structure

```text
cw6_spaom_2026/
├── cw6_qupath/
│   ├── classifiers/
│   │   └── .gitkeep
│   ├── data/
│   │   └── .gitkeep
│   ├── geojson_masks/
│   │   └── melanoma_cropped.geojson
│   ├── scripts/
│   │   └── cellpose_segmentation.groovy
│   └── project.qpproj
├── images/
│   └── melanoma_cropped.ome.tiff
└── docs/
    └── SPAOM2026_QuPath_Practical_Guide.docx
```

## Software requirements

Install the following software before the workshop:

- **QuPath 0.7.0**
- the QuPath **Cellpose extension**, if Cellpose segmentation will be run locally;
- a working Cellpose/Python environment compatible with the extension;
- **Git LFS**, only if the image is distributed directly through this repository.

Participants who cannot run Cellpose locally can use the pre-generated detections provided in:

```text
cw6_spaom_2026/cw6_qupath/geojson_masks/melanoma_cropped.geojson
```

## Download the workshop materials

### Option A: Download the repository as a ZIP

1. Open the GitHub repository.
2. Click **Code**.
3. Select **Download ZIP**.
4. Extract the ZIP file to a local folder with write permissions.

> If the OME-TIFF image is stored with Git LFS, confirm that the downloaded archive includes the actual image and not only an LFS pointer file. If the image is distributed separately, follow the data-download instructions below.

### Option B: Clone with Git

```bash
git lfs install
git clone https://github.com/ORGANIZATION/REPOSITORY.git
cd REPOSITORY
```

Replace `ORGANIZATION/REPOSITORY` with the final repository address.

## Image data

The workshop uses:

```text
cw6_spaom_2026/images/melanoma_cropped.ome.tiff
```

Because OME-TIFF images can be very large, the image may be distributed using Git LFS or through an external institutional repository.

If the image is downloaded separately:

1. Download `melanoma_cropped.ome.tiff` from:


2. Copy the image into:

```text
cw6_spaom_2026/images/
```

3. Confirm that the final path is:

```text
cw6_spaom_2026/images/melanoma_cropped.ome.tiff
```

4. Do not rename the image before opening the QuPath project.

## Open the QuPath project

1. Start QuPath.
2. Go to **File > Project > Open project**.
3. Select:

```text
cw6_spaom_2026/cw6_qupath/project.qpproj
```

Alternatively, drag `project.qpproj` onto the QuPath window.

### If QuPath cannot find the image

The project may contain an image path created on another computer. If the image is shown as missing:

1. Open the project in QuPath.
2. Use the option to update or repair the image URI.
3. Select:

```text
cw6_spaom_2026/images/melanoma_cropped.ome.tiff
```

4. Confirm that the image opens and that its image type is set to **Fluorescence**.

## Cellpose segmentation

The segmentation script is located at:

```text
cw6_spaom_2026/cw6_qupath/scripts/cellpose_segmentation.groovy
```

To run the script:

1. Open the workshop image in QuPath.
2. Create and select the required parent annotation, if instructed in the practical guide.
3. Open the QuPath Script Editor.
4. Open `cellpose_segmentation.groovy`.
5. Review the Cellpose model path and segmentation parameters.
6. Run the script.
7. Inspect the resulting cell detections before continuing with phenotyping.

> The Cellpose model path may be computer-specific and may need to be edited locally.

## Backup segmentation: import the GeoJSON detections

If Cellpose cannot be installed or run during the workshop, use the pre-generated segmentation:

```text
cw6_spaom_2026/cw6_qupath/geojson_masks/melanoma_cropped.geojson
```

Importing the detections is straightforward:

1. Open `melanoma_cropped.ome.tiff` in QuPath.
2. Drag and drop `melanoma_cropped.geojson` directly onto the corresponding image in the QuPath viewer.
3. Confirm that the imported cell objects align correctly with the nuclei and tissue.

> The GeoJSON coordinates are specific to `melanoma_cropped.ome.tiff`. Import the file only onto the corresponding workshop image.

## Classifiers

Saved QuPath classifiers are stored in:

```text
cw6_spaom_2026/cw6_qupath/classifiers/
```

This folder may contain single-measurement, composite, object, or pixel classifiers created during the practical exercise. Classifier availability may depend on the stage of the workshop and the distributed project version.

## QuPath data

Image-specific QuPath analysis data are stored in:

```text
cw6_spaom_2026/cw6_qupath/data/
```

Do not manually rename, reorganize, or delete the files in this folder. QuPath manages these resources as part of the project.

## Recommended workflow

1. Open the QuPath project.
2. Repair the image path if required.
3. Open `melanoma_cropped.ome.tiff`.
4. Run Cellpose segmentation or import the provided GeoJSON detections.
5. Review the segmentation quality.
6. Run threshold-based cell phenotyping.
7. Generate supervised object-classifier training examples.
8. Create the tumor compartment using thresholding or supervised pixel classification.
9. Calculate signed distance to the tumor border.
10. Calculate nearest-neighbor distances between cell populations.
11. Explore the results using **Show plots**.

## Troubleshooting

### The project opens, but the image is missing

Update the image URI and point QuPath to:

```text
cw6_spaom_2026/images/melanoma_cropped.ome.tiff
```

### Cellpose does not run

Use the pre-generated GeoJSON detections supplied in `geojson_masks/`.

### The imported GeoJSON does not align with the image

Confirm that:

- the file is imported onto `melanoma_cropped.ome.tiff`;
- the image has not been cropped, resized, rotated, or transformed;
- the correct GeoJSON file was selected.

### Unrelated classes appear in Train pixel classifier

QuPath can detect classified training annotations present in the loaded image. Before training the tumor pixel classifier, retain only the training annotations required for `Tumor_ML` and the selected background class. Hiding unrelated annotations changes only their visibility and may not exclude them from training.

### The classifier output is difficult to inspect

Temporarily hide cell detections, cell-classification overlays, and unrelated training annotations. Re-enable them after the tumor mask has been validated.

## Workshop materials

The practical guide is expected at:

```text
cw6_spaom_2026/docs/SPAOM2026_QuPath_Practical_Guide.docx
```


## Contact

Workshop instructors:

- **Maria Calvo de Mora Roman**, CNIO
- **Ana Cayuela Lopez**, CNIO

Questions and corrections can be submitted through the GitHub repository's **Issues** section.
