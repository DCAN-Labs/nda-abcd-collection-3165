# Release Notes

## Introduction

The ABCC houses a community-shared and continually updated ABCD neuroimaging dataset available under Brain Imaging Data Structure (BIDS) standards. Source data are converted to BIDS from the [NIMH Data Archive (NDA) share of ABCD fast-track data](https://nda.nih.gov/edit_collection.html?id=2573). Only data that passed the Data Analysis Imaging Center (DAIC) quality control are included. As a community share, the ABCC enables researchers to access **available derivatives** and share their **own derivatives**. The ABCD-BIDS datasets are continually updated as new ABCD releases become available. A list of currently available datasets are provided below.

1. `BIDS inputs` The input DICOM data to this [BIDS version 1.2.0](https://www.nature.com/articles/sdata201644) data collection were retrieved from the [NIMH Data Archive (NDA) share of ABCD fast-track data](https://nda.nih.gov/edit_collection.html?id=2573) and were last accessed on May 1, 2019. BIDS input data were converted from DICOMs using [Dcm2Bids](https://github.com/cbedetti/Dcm2Bids).
2. `abcd-hcp-pipeline` BIDS derivatives data were derived from the [DCAN Labs ABCD-BIDS MRI (version 0.0.3) processing pipeline](https://doi.org/10.5281/zenodo.2587210) which outputs [Human Connectome Project (HCP) Minimal Preprocessing Pipelines-style data](https://doi.org/10.1016/j.neuroimage.2013.04.127) in both volume and surface spaces. This collection is independent from ABCD Data Collection 2573. Users may access ABCD DICOM files via the ABCD fast-track imaging data release in Collection 2573.
3. `abcd-task-hcp-pipeline` a modified version of the TaskfMRIAnalysis stage of the HCP-pipeline (Glasser et al., 2013) developed at University of Vermont by Anthony Juliano, was used to process task-fmri data from the minimally processed ABCD-BIDS (Feczko et al., 2020b) processing pipeline (v.1.0) data, as well as derived ABCC data (Feczko, 2020; ABCD-3165).
4. `freesurfer-5.3.0-HCP` segmentation statistics and surface morphometrics from the FreeSurfer stage within the [DCAN Labs ABCD-BIDS MRI processing pipeline](https://doi.org/10.5281/zenodo.2587210) are provided here.
5. `fMRIPrep` fMRIPrep v20.2.0 was run on all 10,038 participants whose visit one data was successfully converted to BIDS. The limited fMRIPrep processing errors were due to subjects that did not have any valid fMRI runs, but we did not do any manual quality control of outputs. 9,484 participants have at least one output. The data is available in 18 submissions (a summary, including number of files and submission size can be found [here](https://docs.google.com/spreadsheets/d/1NbZ28vBvGVJb9miivgsJ695VVoFBSBuBQmWigN5pg_c/edit#gid=678992105)).

A guiding principle for this collection is to release essential data for analysis.  This collection will be updated with waves of data preparation and processing.  As waves complete preparation or processing they will be uploaded and version-stamped with updated and versioned release notes.

## Release History

### Release 2.0.0 (6/22/2022)

**REVISIONS**

1. **Uploading 144 participants with new data due to revised fast track QC**: The initial release was processed prior to new updates to the fast track QC spreadsheet that affected the original inputs for 144 participants. This led to discrepancies in the number of timepoints reported for connectivity matrices (see below) relative to the inputs. The 144 participants were re-processed through the ABCD-BIDS pipeline at the Minnesota Supercomputing Institute (MSI). The `participants.tsv` file indicates which subjects were reprocessed. These subjects have new Gordon 10 and 5 minute connectivity matrices generated and replaced on the NDA. The old matrices remain valid, but may use different frames from the new matrices. The labels for the updated connectivity matrices were defined in @gordon2016 and generated using the [DCAN Labs cifti connectivity wrapper](https://github.com/DCAN-Labs/cifti-connectivity/) at a frame displacement (FD) threshold of 0.2 mm to filter out high-motion frames. An outlier detection procedure was used to exclude remaining frames 2 STD from the mean.
1. **Providing Connectivity matrices** for those participants with discrepancies in the number of timepoints used
1. **Uploading JSONs for the diffusion inputs** in some participants.
1. **Updated version of the participants.tsv to v1.0.2** includes correction to site and sex designation for a small subset of subjects based on new information from the DAIRC.

**NEW ADDITIONS**

1. **Individualized Network Maps Generated with Infomap and Template Matching (*Submission ID: 36448*)**
1. **Derivatives for the fmriprep pipeline:** fMRIPrep v20.2.0 was run on all 10,038 participants whose visit one data was successfully converted to BIDS. The limited fMRIPrep processing errors were due to subjects that did not have any valid fMRI runs, but we did not do any manual quality control of outputs. 9,484 participants have at least one output. The data is available in 18 submissions (a summary, including number of files and submission size can be found [here](https://docs.google.com/spreadsheets/d/1NbZ28vBvGVJb9miivgsJ695VVoFBSBuBQmWigN5pg_c/edit#gid=678992105)). Detailed information about the files included in each submission are on the second tab of that spreadsheet. Files with no submission name listed have not yet been uploaded.
1. **DWI sidecar JSON patch (Diffusion inputs) (*Submission IDs: 36449 - 36452*)**: The DWI acquisition parameters from subjects scanned on Philips and GE with MR Software release versions 5.3.0_5.3.0.0 and DV25.0_R02_1549.b respectively (n=423) are missing the required field, PhaseEncodingDirection. This omission is because they reported the axis and not direction; therefore we did a manual check of these images to check the phase encoding direction, so that these JSON inputs are BIDS compatible and can be processed by pipelines like QSIprep. These JSONs have been updated and uploaded.
1. **Level-2 task files from the ABCD-task-fMRI pipeline (*Submission IDs: 36458 - 36630*)**

### Release 1.1.1 (10/7/2020)

This was a small version 1.0.0 release of the `derivatives_qc.(json|tsv)` with additional BIDS derivatives quality control data including a "brain coverage score" for the `derivatives.func.runs_task-(MID|nback|rest|SST)_volume` data subsets.

### Release 1.1.0 (7/27/2020)

This was the next big release with the addition of:

1. 157 additional subjects due to updated fast track QC spreadsheet
1. `participants.(json|tsv)` version 1.0.0: BIDS standard participants files with matched groups
1. `sourcedata.func.task_events`: Task-based fMRI E-Prime files
1. `inputs.dwi.dwi`: DWI BIDS input data
1. `derivatives.anat.stats`: FreeSurfer stats files
1. `derivatives.anat.(T1w|T2w)`: T1 and T2 volumes
1. `derivatives.anat.wmparc`: white-matter volume ROIs
1. `derivatives.func.updated_motion_task-(MID|nback|SST|rest)`: Improved motion files (including outlier calculation)
1. `derivatives.func.pconns`: Curated parcellated connectivity files
1. `derivatives.func.runs_task-(MID|nback|SST|rest)_volume`: Minimally-processed fMRI volumes

### Release 1.0.0 (2/17/2020)

This was the initial release of DCAN Labs ABCD-BIDS inputs and derivatives containing **10,038 MRI sessions worth of NDA imagingcollection01 data** and **9,647 MRI sessions worth of NDA fmriresults01 data**.

#### Corrections

##### `task-rest_bold.json`

Discovered in the middle of June 2020, the modality-specific BIDS inherited `task-rest_bold.json` file at the top of the directory tree which is nested in almost every `task-rest` associated record in the NDA database has a typo in it.  The `"TaskDescription"` key has a value of `"See http://www.cognitiveatlas.org/task/id/tsk_4a57abb949e1a/"`.  However, this link goes to the stop signal task page on the Cognitive Atlas website.  Instead you should refer to [the Cognitive Atlas website for "rest eyes open"](http://www.cognitiveatlas.org/task/id/trm_4c8a834779883/).  This website describes the task as:

"Subjects rest passively with their eyes open. Often used as a baseline for comparison for other tasks."

##### `derivatives.func.runs_task-rest_volume`

This data subset was originally uploaded in Release 1.1.0, but was missing all runs chronologically numbered 3 and up.  We are uploading these missing data in Release 1.1.2.

#### `updated_dwi_input_json`

The DWI acquisition parameters from all subjects scanned on GE with MR Software release DV25.0_R02_1549.b (n=281) are missing the required field, PhaseEncodingDirection. This omission is because they reported the axis and not direction.
