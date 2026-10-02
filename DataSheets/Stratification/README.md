# PANORAMA Tumor Annotation Dataset

## Overview

This repository contains the data dictionary for the **PANORAMA Tumor Annotation Study**, designed to capture imaging-based pancreatic cancer characteristics and reader-corrected tumor annotations. The dataset supports quality assurance, segmentation validation, and radiologic characterization of pancreatic ductal adenocarcinoma (PDAC).

---

## Data Collection Form

**Form Name:** `panorama_annotation`

The form records tumor characteristics, annotation provenance, and reviewer corrections for PANORAMA cases.

---

## Variables

| Variable Name | Description | Type |
|--------------|-------------|------|
| `record_id` | Unique study record identifier | Text |
| `case_id` | PANORAMA case identifier | Text |
| `label_source` | Original source of segmentation label | Radio |
| `reader` | Reader performing annotation correction | Dropdown |
| `epicenter` | Primary tumor location within pancreas | Checkbox |
| `attenuation` | Tumor attenuation pattern on CT | Radio |
| `cbd_dilatation` | Presence of common bile duct dilatation | Yes/No |
| `mpd_dilatation` | Presence of main pancreatic duct dilatation | Yes/No |
| `parenchymal_atrophy` | Presence of pancreatic parenchymal atrophy | Yes/No |
| `t_stage` | Tumor T stage according to AJCC 8th edition | Radio |

---

## Variable Definitions

### `record_id`
Unique REDCap/study record identifier. Enter the PANORAMA case identifier exactly.

### `case_id`
PANORAMA case identifier.

### `label_source`
Indicates whether the original segmentation label distributed within PANORAMA was manually created or AI-generated.

**Options**
- `1` = Manual (PANORAMA)
- `2` = AI-generated (PANORAMA)

### `reader`
Reader responsible for reviewing and correcting annotations.

**Options**
- `1` = R1
- `2` = R2
- `3` = R3
- `4` = R4
- `5` = R5

### `epicenter`
Primary anatomical location of the pancreatic tumor.

**Options**
- `1` = Head, Uncinate, or Neck
- `2` = Body
- `3` = Tail
- `4` = Multifocal / spanning ≥2 segments
- `5` = Diffuse / indeterminate

**Note:** This is a checkbox field, so multiple selections may be possible depending on study protocol.

### `attenuation`
Tumor attenuation characteristics on CT imaging.

**Options**
- `1` = Hypodense
- `2` = Isodense
- `3` = Hyperdense

### `cbd_dilatation`
Presence of common bile duct dilatation.

**Options**
- Yes
- No

### `mpd_dilatation`
Presence of main pancreatic duct dilatation.

**Options**
- Yes
- No

### `parenchymal_atrophy`
Presence of pancreatic parenchymal atrophy.

**Options**
- Yes
- No

### `t_stage`
Tumor stage according to the **AJCC 8th edition** staging system.

**Options**
- `1` = T1, tumor 2 cm or smaller
- `2` = T2, tumor over 2 cm up to 4 cm
- `3` = T3, tumor over 4 cm
- `4` = T4, celiac axis, superior mesenteric artery, or common hepatic artery involvement
- `5` = TX, cannot be assessed

**Note:** T4 is defined by arterial involvement regardless of tumor size.

---

## Required Fields

The following variables are marked as required in the data dictionary:

- `label_source`
- `reader`
- `epicenter`
- `attenuation`
- `cbd_dilatation`
- `mpd_dilatation`
- `parenchymal_atrophy`
- `t_stage`

---

## Intended Use

This dataset is intended for:

- Tumor segmentation quality assessment
- Manual versus AI annotation comparison
- Inter-reader agreement studies
- Radiologic characterization of PDAC
- Development and validation of AI-based imaging biomarkers

---

## Study Context

PANORAMA is a pancreatic cancer imaging research initiative focused on improving early detection, tumor characterization, and AI-assisted radiologic analysis through standardized imaging annotation and review.

---

## File Information

- **Source file:** `Data Dictionary.csv`
- **Primary form:** `panorama_annotation`
- **Data type:** REDCap-style data dictionary
- **Clinical focus:** Pancreatic tumor imaging annotation

