# PANORAMA AI Annotation Audit Dataset

## Overview

This repository contains the REDCap-style data dictionary for the **PANORAMA AI Annotation Audit Study**. The form is designed to evaluate the quality, completeness, and usability of AI-generated or PANORAMA-provided tumor annotations on CT examinations for pancreatic ductal adenocarcinoma (PDAC).

The audit workflow supports structured review of CT evaluability, annotation completeness, segmentation deficiencies, and CT image quality for downstream imaging research and AI model validation.

---

## Source File

- **Data dictionary file:** `Data Dictionary AI.csv`
- **Primary REDCap form:** `panorama_audit`
- **Clinical focus:** PDAC tumor annotation review
- **Use case:** AI annotation quality assessment and dataset curation

---

## Form Information

**Form Name:** `panorama_audit`

The form captures the following audit domains:

- Case identification
- Reader assignment
- CT evaluability
- Reasons for non-evaluable CT examinations
- Annotation completeness
- Estimated tumor volume captured by annotation
- Primary annotation deficiency type
- CT image quality for volumetric tumor segmentation

---

## Variables Included

| Variable Name | Field Type | Description |
|---------------|------------|-------------|
| `record_id` | Text | Auto-numbered unique record identifier |
| `case_id` | Text | PANORAMA case identifier |
| `reader_id` | Dropdown | Assigned reader ID |
| `ct_evaluable` | Radio | Whether CT is evaluable for PDAC annotation review |
| `non_eval_reason` | Dropdown | Reason for CT non-evaluability |
| `non_eval_notes` | Text | Free-text explanation if other non-evaluability reason is selected |
| `annotation_completeness` | Dropdown | Completeness of the PANORAMA-provided annotation |
| `volume_captured` | Dropdown | Estimated proportion of tumor volume captured |
| `deficiency_type` | Checkbox | Primary annotation deficiency type |
| `image_quality` | Radio | Whether CT quality is adequate for volumetric segmentation |
| `quality_reason` | Checkbox | Reason for inadequate image quality |
| `quality_notes` | Text | Free-text explanation if other image quality reason is selected |

---

## Variable Definitions

### `record_id`
Auto-numbered unique study identifier.

### `case_id`
PANORAMA case identifier.

**Instruction:** Enter the PANORAMA case identifier exactly as shown in the filename.

### `reader_id`
Assigned reader performing the annotation audit.

**Options**

- `1` = R1
- `2` = R2
- `3` = R3
- `4` = R4
- `5` = R5

---

## CT Evaluability

### `ct_evaluable`
Determines whether the CT examination is evaluable for PDAC annotation review.

**Options**

- `1` = Yes
- `0` = No

A CT is considered non-evaluable if any of the following apply:

- Pancreas is absent from the field of view
- Slices are missing, truncated, or corrupted
- Contrast phase is incorrect
- File is unreadable
- No visible tumor is present despite the PDAC label

### `non_eval_reason`
Displayed when `ct_evaluable = 0`.

**Options**

- `1` = No pancreas in field of view
- `2` = Incomplete anatomical coverage, slices missing or truncated
- `3` = Wrong contrast phase, such as non-contrast or arterial phase
- `4` = Corrupted or unreadable file
- `5` = No visible tumor despite PDAC label
- `6` = Other, specify in notes
- `7` = Stent
- `8` = Significant motion artifacts
- `9` = Significant streak artifacts

### `non_eval_notes`
Free-text field displayed when `non_eval_reason = 6`.

Use this field to specify the reason when “Other” is selected.

---

## Annotation Assessment

### `annotation_completeness`
Assesses whether the PANORAMA-provided annotation captures the full radiologically apparent 3D tumor extent.

Displayed when `ct_evaluable = 1`.

**Options**

- `1` = Complete, captures ≥90% of radiologically apparent tumor
- `2` = Partial, captures 50-89% of tumor
- `3` = Grossly incomplete, captures <50% of tumor
- `4` = Over-segmented tumor

### `volume_captured`
Visual estimate of the tumor volume captured by the annotation.

Displayed when annotation completeness is complete, partial, or grossly incomplete.

**Options**

- `1` = 100%
- `2` = 90-99%
- `3` = 75-89%
- `4` = 50-74%
- `5` = 25-49%
- `6` = Less than 25%

### `deficiency_type`
Identifies the primary segmentation deficiency.

Displayed when the annotation is partial, grossly incomplete, or over-segmented.

**Options**

- `1` = Craniocaudal truncation, tumor extends above or below annotated slices
- `2` = Lateral under-segmentation, annotation does not reach lateral tumor boundaries
- `3` = Missed component, separate tumor focus or satellite not annotated
- `4` = Over-segmentation, annotation substantially exceeds tumor boundaries

---

## Image Quality Assessment

### `image_quality`
Determines whether the CT is of adequate quality for reliable volumetric tumor segmentation.

Displayed when `ct_evaluable = 1`.

**Options**

- `1` = Yes
- `0` = No

**Note:** This assessment should focus on the CT image quality itself and should be considered separately from annotation completeness.

### `quality_reason`
Displayed when `image_quality = 0`.

**Options**

- `1` = Suboptimal contrast timing
- `2` = Other, specify in notes

### `quality_notes`
Free-text field displayed when `quality_reason(2) = 1`.

Use this field to describe other reasons for inadequate image quality.

---

## Required Fields

The following fields are marked as required in the data dictionary:

- `record_id`
- `case_id`
- `reader_id`
- `ct_evaluable`
- `non_eval_reason`, when CT is non-evaluable
- `annotation_completeness`, when CT is evaluable
- `volume_captured`, when annotation completeness is complete, partial, or grossly incomplete
- `deficiency_type`, when annotation is partial, grossly incomplete, or over-segmented
- `image_quality`, when CT is evaluable
- `quality_reason`, when image quality is inadequate

---

## Branching Logic Summary

| Field | Display Condition |
|-------|-------------------|
| `non_eval_reason` | `[ct_evaluable] = '0'` |
| `non_eval_notes` | `[non_eval_reason] = '6'` |
| `annotation_completeness` | `[ct_evaluable] = '1'` |
| `volume_captured` | `[annotation_completeness] = '1'`, `'2'`, or `'3'` |
| `deficiency_type` | `[annotation_completeness] = '2'`, `'3'`, or `'4'` |
| `image_quality` | `[ct_evaluable] = '1'` |
| `quality_reason` | `[image_quality] = '0'` |
| `quality_notes` | `[quality_reason(2)] = '1'` |

---

## Intended Applications

This audit dataset can be used for:

- AI-generated tumor annotation quality assurance
- Manual review of AI or PANORAMA-provided segmentations
- Dataset curation before model development
- Identification of non-evaluable CT examinations
- Estimation of tumor annotation completeness
- Assessment of image quality for segmentation-based research
- Inter-reader reliability and quality-control studies
- PDAC imaging biomarker and radiomics workflows

---

## Recommended Workflow

1. Confirm the PANORAMA case identifier.
2. Assign the correct reader ID.
3. Determine whether the CT is evaluable.
4. If non-evaluable, select the reason and provide notes if needed.
5. If evaluable, assess annotation completeness.
6. Estimate the tumor volume captured by the annotation.
7. Identify the primary deficiency type if annotation is incomplete or over-segmented.
8. Assess whether CT image quality is adequate for volumetric segmentation.
9. Document image quality limitations when applicable.

---

## Study Context

The PANORAMA AI Annotation Audit form provides a structured method for reviewing tumor annotations and CT image quality in pancreatic cancer imaging datasets. It is intended to support robust quality control, reproducible imaging annotation workflows, and reliable downstream AI-based PDAC research.
