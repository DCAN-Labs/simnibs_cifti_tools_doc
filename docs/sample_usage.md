
# OAT Subject Processing Guide

This guide walks you through processing OAT subjects with Simnibs Cifti Tools to obtain optimal stimulation targets by island for the AMN and SCAN networks.

## Prerequisites

Before starting, ensure you have:
- fMRIprep outputs for the subject
- XCPD outputs for the subject  
- FreeSurfer outputs (recon-all completed)
- Sufficient storage for intermediate and final outputs
- Access to the required template files

---

## Step 1: Generate Annotation Files

Run the `make_annot_dlabel.sh` script to create annotation files from FreeSurfer outputs.

### Usage
```bash
bash make_annot_dlabel.sh <subject_id> <output_dir> <path_freesurfer> <session>
```

### Arguments
| Argument | Description |
|----------|-------------|
| `subject_id` | Subject ID (everything after "sub-", e.g., "OAT001") |
| `output_dir` | Directory for output files (recommended: fmriprep derivatives directory) |
| `path_freesurfer` | Path to FreeSurfer subject directory containing `label/` and `surf/` folders |
| `session` | Session identifier (e.g., "01", "02") |

### Required FreeSurfer Files
The script expects the following files in your FreeSurfer directory:
- `label/lh.aparc.annot`
- `label/lh.aparc.a2009s.annot`
- `label/rh.aparc.annot`
- `label/rh.aparc.a2009s.annot`
- `surf/lh.white`
- `surf/rh.white`

---

## Step 2: Resample Native Surfaces

Resample high-resolution native surfaces to 32k resolution for use by the pipeline. 
**If this isn't already done by the imaging processing pipeline**

### Usage
```bash
bash resample_native_surfaces.sh <path_saved_files>
```

### Prerequisites
- fMRIprep outputs must include: `*hemi-L_space-fsLR_desc-msmsulc_sphere.surf.gii` and `*hemi-R_space-fsLR_desc-msmsulc_sphere.surf.gii`
- Access to template files:
  - `/projects/standard/miran045/shared/code/external/templateflow/tpl-fsLR/tpl-fsLR_hemi-L_den-32k_sphere.surf.gii`
  - `/projects/standard/miran045/shared/code/external/templateflow/tpl-fsLR/tpl-fsLR_hemi-R_den-32k_sphere.surf.gii`

---

## Step 3: Create Subject Config Files

Copy the template config file and customize it for your subject for both PFM and Probabilistic Atlas analyses:

```bash
cp /projects/standard/darro015/shared/projects/OAT/experiments/simnibs_cifti_tools/config_files/sub-OAT001_settings.config /projects/standard/darro015/shared/projects/OAT/experiments/simnibs_cifti_tools/config_files/sub-YOURSUBJECT_settings.config
```

Edit the config file to set:
- Input data paths (fMRIprep, XCPD, FreeSurfer)
- Output directory
- Working directory

---

## Step 4: Run the Pipeline

Execute the Simnibs Cifti Tools pipeline for both PFM and Probabilistic Atlas analyses:

```bash
bash /projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/wip_k_branch/simnibs_cifti_tools/preprocessing/settings_file_reader.sh --config /projects/standard/darro015/shared/projects/OAT/experiments/simnibs_cifti_tools/config_files/sub-YOURSUBJECT_settings.config
```

---

## Step 5: Prepare Results for Box

After the pipeline completes and you've reviewed the results, use the `prepare_results_for_box.sh` script to restructure and rename files for uploading to Box.

### Usage
```bash
bash prepare_results_for_box.sh <target_dir> <destination_dir> <AMN_L_target> <AMN_R_target> <SCAN_L_target> <SCAN_R_target>
```

target_dir should be the same location as what was listed as work_location in your config file.

### Arguments
| Argument | Description |
|----------|-------------|
| `target_dir` | Full path to the Simnibs Cifti Tools output directory |
| `destination_dir` | Full path where outputs will be saved for Box upload |
| `AMN_L_target` | Island number chosen for left AMN |
| `AMN_R_target` | Island number chosen for right AMN |
| `SCAN_L_target` | Island number chosen for left SCAN |
| `SCAN_R_target` | Island number chosen for right SCAN |

---

## Quick Reference

| Step | Script | Estimated Time |
|------|--------|-----------------|
| 1 | make_annot_dlabel.sh | ~5 min |
| 2 | resample_native_surfaces.sh | ~5 min |
| 3 | Config setup | ~5 min |
| 4 | Pipeline execution | ~6-24 hours |
| 5 | prepare_results_for_box.sh | ~5 min |

---

## Troubleshooting

- **Missing FreeSurfer files**: Ensure recon-all completed successfully
- **Template access denied**: Check permissions for the templateflow directory
- **Pipeline errors**: Check the working directory logs for detailed error messages