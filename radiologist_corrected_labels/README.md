# AI-Assisted Radiologist Curation of PANORAMA for PDAC Tumor Segmentation Benchmarking and Quantitative Imaging Research

## Overview

This repository contains radiologist-corrected pancreatic ductal adenocarcinoma (PDAC) tumor segmentations and accompanying case-level audit data derived from the public PANORAMA dataset.

The original PANORAMA labels were developed primarily to support pancreatic cancer detection research. Our study evaluated whether those labels were also suitable as reference annotations for volumetric tumor-segmentation benchmarking. Radiologists systematically reviewed the available CT-label pairs, documented image and annotation quality, and corrected the tumor boundaries for cases suitable for reliable volumetric assessment.

The resulting resource is intended to support reproducible evaluation of PDAC tumor-segmentation methods.

## Why 590 Cases Were Selected

The review included 679 PANORAMA CT examinations with tumor labels. Of these, 614 were evaluable for volumetric segmentation. The 65 non-evaluable examinations were excluded most commonly because no tumor was visible despite an assigned PDAC label (28/65, 43.1%) or because of stent-related limitations (27/65, 41.5%). Other reasons included an incorrect contrast phase, motion artifact, unreadable files, and other technical limitations.

Among the 614 evaluable examinations, 590 had adequate image quality for confident tumor-boundary delineation. Of the 24 examinations with inadequate image quality, 19 (79.2%) had suboptimal contrast timing. These 590 evaluable, adequate-quality examinations formed the final corrected segmentation cohort.

## How the Segmentations Were Corrected

Five radiologists assessed the CT-label pairs for evaluability, image quality, annotation completeness, tumor-volume capture, and segmentation errors. For the 590 evaluable cases with adequate image quality, Model-WS generated draft masks that radiologists edited to match the tumor boundaries visible on CT. The released masks are AI-assisted, radiologist-corrected reference segmentations. Model-BB and Swin UNETR were used only for downstream benchmarking and did not generate the curation drafts.

## Repository Contents

### Segmentations

`radiologist_corrected_labels/`

This directory contains 590 corrected PDAC tumor segmentations in compressed NIfTI format (`.nii.gz`). Each filename retains the corresponding PANORAMA case identifier so that the segmentation can be matched to the source CT examination.

### Data Sheets

`DataSheets/`

This directory contains the audit datasets, data dictionaries, and supporting documentation for the manual-label cohort, AI-generated-label cohort, and case-stratification data. These files document the review outcomes and relevant imaging and tumor characteristics.

## Source Imaging Data

The source CT examinations are not redistributed in this repository. They should be obtained through the official PANORAMA dataset. The identifiers in the segmentation filenames provide the linkage between the corrected annotations and their corresponding PANORAMA CT examinations.

The original PANORAMA labels and repository are available at:

https://github.com/DIAGNijmegen/panorama_labels

## Recommended Use

This resource is intended for research involving PDAC tumor-segmentation benchmarking, annotation-quality assessment, and evaluation of imaging-analysis methods.

When using this resource, investigators should clearly distinguish among the original 679 reviewed CT-label pairs, the 614 evaluable cases, and the final 590-case corrected segmentation cohort.

## Associated Manuscript

AI-Assisted Radiologist Curation of PANORAMA for PDAC Tumor Segmentation Benchmarking

The full citation will be added when the manuscript is published.

## Contact

Questions about the annotations, curation process, or associated study should be directed to the corresponding author of the manuscript.
