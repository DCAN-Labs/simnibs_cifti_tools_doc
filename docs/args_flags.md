# Users Guide

This guide is organized into a full arguments table as well as sections that break this down based on required, targeting options, and hardware configuration. Next we have included documentation regarding available options for TMS coil selection for simulations. Finally we have included documentation about settings file setup with a sample settings file script.

## Full Arguments Table

| Flag                | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `--SID`         | Subject ID.                                |
| `--VISIT`     | Session identifier.                    |
| `--simnibs_container` | Path to the SimNIBS v3 Singularity container (`.sif`).                    |
| `--simnibs_version` | SimNIBS version string (e.g., `3`).                                        |
| `--OUTPUT_FOLDER` | Root Output directory        |
| `--P_SCT_REPO` | Path to where Simnibs Cifti Tools repository is cloned.      |
| `--brain_target`       | Specify how you would like optimal targeting to be performed.                    |
| Available options:     |   *all, dlpfc, Salience, any combination of functional brain networks as a comma separated*                       |
| `--user_provided_table`       | Specify a full path to the a csv table that included index and another column to sort as inclusion/exclusion.          |
| `--user_inclusion_column`       | Specify the column in the user_provided_table to filter by. The rows in that column need to either be 0/1 or exclude/include.      |
| `--hemi_list`       | Specify the hemispheres of interest.                    |
| Available options:     |   *L,R*                       |
| `--lobe_list`       | Specify the lobes of interest.                    |
| Available options:     |   *Cingulate, Frontal, Insula, Occipital, Parietal, Temporal, any combination of these as a comma separated list*                       |
| `--hemisphere_lobe_mask`       | Specify how you would like optimal targeting to be performed.                    |
| Available options:     |   *"L_Cingulate, L_Frontal, L_Insula, L_Occipital, L_Parietal, L_Temporal, R_Cingulate, R_Frontal, R_Insula, R_Occipital, R_Parietal, R_Temporal*  | 
| Options continued:    |   *any combination of the above as a comma separated list*             |
| `--threshold`       | Specify which threshold you would like to calculate the optimal targeting solution to be set to                  |
| `--coil_name`       | Coil name (must match an existing SimNIBS coil).                                        |
| `--P_L_mdthk_atlas`       | Specify a full path to the left midthickness surface file in atlas space                  |
| `--P_R_mdthk_atlas`       | Specify a full path to the right midthickness surface file in atlas space                  |
| `--P_L_mdthk_native`       | Specify a full path to the left midthickness surface file in native space                  |
| `--P_R_mdthk_native`       | Specify a full path to the right midthickness surface file in native space                  |
| `--P_L_pial_atlas`       | Specify a full path to the left pial surface file in atlas space                  |
| `--P_R_pial_atlas`       | Specify a full path to the right pial surface file in atlas space                  |
| `--P_L_pial_native`       | Specify a full path to the left pial surface file in native space                  |
| `--P_R_pial_native`       | Specify a full path to the right pial surface file in native space                  |
| `--P_L_white_atlas`       | Specify a full path to the left white surface file in atlas space                  |
| `--P_R_white_atlas`       | Specify a full path to the right white surface file in atlas space                  |
| `--P_L_white_native`       | Specify a full path to the left white surface file in native space                  |
| `--P_R_white_native`       | Specify a full path to the right white surface file in native space                  |
| `--P_L_inflated`       | Specify a full path to a left inflated surface file in 32k resolution                  |
| `--P_R_inflated`       | Specify a full path to a right inflated surface file in 32k resolution                  |
| `--P_T1w`       | Specify a full path to the T1w file                  |
| `--P_T2w`       | Specify a full path to the T2w file                  |
| `--P_F_dlabel`       | Specify a full path to the functional dlabel file                  |
| `--P_A_dlabel`       | Specify a full path to the aparc aseg dlabel file in 32k resolution                  |
| `--P_A_dlabel_2009`       | Specify a full path to the apar aseg a2009s dlabel file                  |
| `--brain_target_2`       | Specify which additional functional brain target you would like simulated.                   |
| `--find_the_best_by`       | Specify how to optimize the target.                   |
| Available options:   |   *cummulative_energy_within_target, percent_target_covered, relative_energy_in_target, relative_energy_off_target, relative_area_in_target, relative_area_off_target*                       |
| `--scan_islands`       | Enter a 1 if you'd like to use this additional processing step                   |
| `--dry_run`       | Include this argument if you would like to see how your settings would run without actual execution or sending off jobs.            |
| `--help`   |    Display the help message                       |

### Required Arguments

This section contains the minimum required arguments necessary to run the tool with default settings for all other configurations.

* --SID
* --VISIT
* --P_SCT_REPO
* --brain_target
* --P_L_mdthk_native
* --P_R_mdthk_native
* --P_L_pial_native
* --P_R_pial_native
* --P_L_white_native
* --P_R_white_native
* --path_L_inflated
* --path_R_inflated
* --P_T1w
* --P_T2w
* --P_F_dlabel
* --P_A_dlabel
* --P_A_dlabel_2009

### Targeting Options

The below arguments allow for customization of brain targeting.

* --brain_target
  * all
  * dlpfc
  * 'A space separated list of desired networks enclosed in a parenthesis'
    * "Salience"
* --brain_target_2
  * An additional brain network to simulate.
* --find_the_best_by
* --hemisphere_lobe_mask

### Hardware Configuration

Coil types and such

* --coil_name
* --threshold

## Available TMS Coils

**(Pulled from the SimNIBS repository updated Sept 30, 2025)**  
Use one of the following values with the `--coil_name` flag.

---

### **Magstim**

- `Magstim_70mm_Fig8.ccd`
- `Magstim_70mm_Fig8_Dreal.ccd`
- `Magstim_70mm_Fig8_Dreal_Drakaki22.ccd`
- `Magstim_D50_Alpha_Bl.ccd`
- `MagStim_D70.ccd`
- `MagStim_DCC.ccd`

---

### **MagVenture**

- `MagVenture_MC_B70.ccd`
- `MagVenture_MC-125.ccd`
- `MagVenture_MC-125_new.ccd`
- `MagVenture_MC_B65_HO8.ccd`
- `MagVenture_C-100.ccd`
- `MagVenture_C-B60.ccd`
- `MagVenture_C-B70.ccd`
- `MagVenture_Cool-B35.ccd`
- `MagVenture_Cool-B65.ccd`
- `MagVenture_Cool-B70.ccd`
- `MagVenture_Cool-D-B80.ccd`
- `MagVenture_MCF-75.ccd`
- `MagVenture_MCF-B65.ccd`
- `MagVenture_MCF0B65_new.ccd`
- `MagVenture_MMC-140-II.ccd`
- `MagVenture_MRI-B91.ccd`
- `MagVenture_MST_Twin.ccd`

---

### **Deymed**

- `Deymed_120BFV.ccd`
- `Deymed_50BF.ccd`
- `Deymed_70BF.ccd`

---

### **MagMore**

- `MagMore_PMD25-decentral.ccd`
- `MagMore_PMD45-EEG.ccd`
- `MagMore_PMD70.ccd`

---

### **How to Use**

Specify any coil from the lists above:

```bash
--coil_name Magstim_70mm_Fig8.ccd
```

## Settings Script setup

To use this tool in a reproducable way it is recommended to create a bash script that contains all of the desired arguments and settings which are desired. It is possible to run this software from the command line using the desired arguments however this is discouraged for lack of ease while troubleshooting and rerunning.

A settings script begins with the path to where your cloned version of Simnibs Cifti Tools is calling the settings_file_reader.sh.

```bash
/projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/wip_k_branch/simnibs_cifti_tools/preprocessing/settings_file_reader.sh
```

From here you add the argument with its matching response like below.

```bash
simnibs_cifti_tools/preprocessing/settings_file_reader.sh \
--SID sub-fake01
```

This process continues ensuring you add a `\` symbol a space after the prior argument pairing then starting the next argument on a new line until you have completed adding all of the required arguments and updated the targeting options for the specific task.

Save this script with any file name you would like. This script gets executed to start the process. Below is a sample way to do so if the script were named **test_settings_script.txt**

```bash
bash test_settings_script.txt
```

### Sample settings file

To use replace 'sub-fake01' with the actual subjectID & replace 'ses-fake01' with the actual session identifier.
After running the intial steps to obtain the necessary input files.

```bash
path_to_sct_repo=/projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/wip_k_branch/simnibs_cifti_tools

${path_to_sct_repo}/preprocessing/settings_file_reader.sh \
--SID sub-fake01 \
--VISIT ses-fake01 \
--OUTPUT_FOLDER /full_path/desried_simulations_output_location \
--P_SCT_REPO ${path_to_sct_repo} \
--work_location /full_path/desired_work_location/sub-fake01 \
--brain_target dlpfc \
--threshold 99.5 \
--P_F_dlabel /full_path/data/TemplateMatching/sub-fake01/sub-fake01_ses-fake01_task-restMENORDICrmnoisevols_space-fsLR_den-91k_desc-denoised_bold_spatially_interpolated_template_matched_Zscored_scanthresh3_recolored.dlabel.nii \
--P_A_dlabel /full_path/input_data/sub-fake01/fake01.aparc.32k_fs_LR.dlabel.nii \
--P_A_dlabel_2009 /full_path/input_data/sub-fake01/fake01.aparc.a2009s.32k_fs_LR.dlabel.nii \
--P_T1w /full_path/data/ses-fake01/anat/sub-fake01_ses-fake01_run-01_T1w.nii.gz \
--P_T2w /full_path/data/ses-fake01/anat/sub-fake01_ses-fake01_run-01_T2w.nii.gz \
--P_L_mdthk_native /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_hemi-L_desc-msmsulc_midthickness.surf.gii \
--P_R_mdthk_native /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_hemi-R_desc-msmsulc_midthickness.surf.gii \
--P_L_pial_native /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_hemi-L_desc-msmsulc_pial.surf.gii \
--P_R_pial_native /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_hemi-R_desc-msmsulc_pial.surf.gii \
--P_L_white_native /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_hemi-L_desc-msmsulc_white.surf.gii \
--P_R_white_native /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_hemi-R_desc-msmsulc_white.surf.gii \
--path_L_inflated /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_L_desc-hcp_inflated.surf.gii \
--path_R_inflated /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_R_desc-hcp_inflated.surf.gii \
--P_L_mdthk_atlas /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_L_desc-hcp_midthickness.surf.gii \
--P_R_mdthk_atlas /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_R_desc-hcp_midthickness.surf.gii \
--P_L_pial_atlas /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_L_pial.surf.gii \
--P_R_pial_atlas /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_R_pial.surf.gii \
--P_L_white_atlas /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_L_white.surf.gii \
--P_R_white_atlas /full_path/input_data/sub-fake01/sub-fake01_ses-fake01_run-01_space-fsLR_den-32k_R_white.surf.gii \
--brain_target_2 Somato-cognitive-action_net \
--scan_islands 1 \
--coil_name 'Magstim_70mm_Fig8.ccd';
```

## Key flags Old

| Flag                | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `--subject`         | Subject ID used throughout the FEM pipeline.                                |
| `--subject_dir`     | Path to subject directory containing FreeSurfer outputs.                    |
| `--output_dir`      | Directory where all FEM and optimization results are written.               |
| `--simnibs_container` | Path to the SimNIBS v3 Singularity container (`.sif`).                    |
| `--simnibs_version` | SimNIBS version string (e.g., `3`).                                        |
| `--coil_name`       | Coil name (must match an existing SimNIBS coil).  
