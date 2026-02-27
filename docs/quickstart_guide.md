# Quickstart Guide

The goal of this section is to help users get started using this tool as quickly as possible focusing on the bare essentials.

## Required Input Files

The mandatory input files include a T1, T2, inflated, the Native 32k resolution pial, white, and midthickness surfaces for both left and right hemispheres, and three Dlabel files. For guidance regarding imaging inputs see [Imaging files](./dependancies.md).

## Required Arguments

In order for this tool to run each of the required arguments need to be supplied. These are shown in the below tables.
These arguments need to be supplied after each other and after pointing to the main script. For example
```bash
path_to_sct_repo/preprocessing/settings_file_reader.sh --P_T1w full_path/T1w.nii.gz --brain_target dlpfc ...
```

### Optimization Settings

The mandatory optimization settings include the desired brain target, threshold, and where to store outputs. 

| Category | Argument | Options |
| -------- | ------- | ------- |
| Brain target | --brain_target | all, dlpfc, or any combination of functional brain networks as a comma separated list |
| Threshold | --threshold | any percentage greater than 0 and less than 100. i.e. 99.5 |

List of incorporated functional networks acceptable as `--brain_target` as used in this pipeline:

```text
Auditory_net, Cingulo-Opercular_net, Default_Mode_net, Dorsal_Attention_net, Frontoparietal_net, Medial_Temporal_Lobe_net, Parietal_Medial_net, Parieto-Occipital_net, Salience, Sensorimotor_Lateral_net, Sensorimotor_Medial_net, Temporal_Pole_net, Ventral_Attention_net, Visual_net, Somato-cognitive-action_net
```

### Neuroimaging File Paths

Full paths to the following files are needed and should be supplied after the provided argument.

| File | Argument | Sample |
| -------- | ------- | ------- |
| T1 structural file | --P_T1w | full/path/path_T1.nii.gz |
| T2 structural file | --P_T2w | full/path/path_T2.nii.gz |
| Left_32k_midthickness.surf.gii | --P_L_mdthk_native | full/path/path_L_32k_midthickness.surf.gii |
| Right_32k_midthickness.surf.gii | --P_R_mdthk_native | full/path/path_R_32k_midthickness.surf.gii |
| Left_32k_white.surf.gii | --P_L_white_native | full/path/path_L_32k_white.surf.gii |
| Right_32k_white.surf.gii | --P_R_white_native | full/path/path_R_32k_white.surf.gii |
| Left_32k_pial.surf.gii | --P_L_pial_native | full/path/path_L_32k_pial.surf.gii |
| Right_32k_pial.surf.gii | --P_R_pial_native | full/path/path_R_32k_pial.surf.gii |
| Left_inflated_32k.surf.gii | --P_L_inflated | full/path/path_L_32k_inflated.surf.gii |
| Right_inflated_32k.surf.gii | --P_R_inflated | full/path/path_R_32k_inflated.surf.gii |
| func_dlabel.nii | --P_F_dlabel | full/path/path_LR_func_dlabel.nii |
| aparc_aseg_dlabel.nii | --P_A_dlabel | full/path/aparc_aseg_dlabel.nii |
| aparc_aseg_2009_dlabel.nii | --P_A_dlabel_2009 | full/path/aparc_aseg_2009_dlabel.nii |

### Input and Output Locations

For the scripts to find each other the full path to where the cloned Simnibs Cifti Tools Repo needs to be provided as well as where you would like the outputs to be stored.

| Category | Argument | Sample |
| -------- | ------- | ------- |
| Work directory | --work_location | /full/path/desired/location |
| Full_path_SCT_repo | --P_SCT_REPO | /full/path/simnibs_cifti_tools |

### Subject Labels

The provided subject labels are used to determine output locations as well as to ensure simulations are generated for unique subject id and visit id combinations.

| Category | Argument | Sample |
| -------- | ------- | ------- |
| Subject ID | --SID | fake01 |
| Visit ID | --VISIT | ses-1 |

### Note regarding intermediary outputs

The intermediary simulations are stored at the location specified during the --OUTPUT_FOLDER argument nested by subject ID and Visit like `output_folder/subjid/session`. By default this is set to start from the current working directory when the `settings_file_reader.sh` script gets executed. It is recommended to set this to a place that stays the same between simulations for the same subject and session to speed up the process.
Example: `--OUTPUT_FOLDER /scratch.global/baron063/simulation_outputs --SID fake01 --VISIT ses-1`
Example root simulation path: `/scratch.global/baron063/simulation_outputs/fake01/ses-1/`

## Settings Script

It is possible to run this pipeline through the command line however it is recommended to create a settings file script for reproducability as well as troubleshooting. Please see the documentation section regarding [settings script setup](./args_flags.md#settings-script-setup) where all key settings get set through flags and arguments.

### Provided template settings script

```bash
path_to_sct_repo=/projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/wip_k_branch/simnibs_cifti_tools

${path_to_sct_repo}/preprocessing/settings_file_reader.sh \
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
--P_SCT_REPO ${path_to_sct_repo} \
--work_location /full_path/desired_work_location/sub-fake01 \
--SID sub-fake01 \
--VISIT ses-fake01 \
```

## Running the Pipeline

To run the pipeline simply execute your settings script.
This can be done via `bash settings_file.sh` if you saved the script as `settings_file.sh`.

## Expected Outputs

Once a run is completed, all the files will be saved in the folder you defined as output folder with the addition of your defined subjectID and visitID.

For instance if `--SID sub-fake01 --VISIT ses-fake01 --work_location /full_path/desired_work_location/sub-fake01` was provided the output folder for the optimal targets would be `/full_path/desired_work_location/sub-fake01/sub-fake01_OTaS`). This folder will contain the following subfolders:

```markdown
├── /home/sub-fake01_OTaS  
    ├── intermediaries
        ├── dlabel_islands
        └── percent_preserved_Efield_within_network
    ├── optimal_targets
        └── Cingulo-Opercular        
            ├── Optimal_target_1_gy_##
            ├── Optimal_target_2_gy_##
            ├── Optimal_target_3_gy_##
            ├── sub-fake01_Cingulo-Opercular_net
            └── sub-fake01_L_dlpfc
        └── Ventral_Attention        
            ├── Optimal_target_1_gy_##
                └── coord_native.csv
                └── opt_coil_position_brainsight.txt
                └── opt_matrix.txt
                └── optimal_target_1_dscalar.png
                └── sub-fake01_ses-fake01_Efield_cifti_native.dscalar.nii
            ├── Optimal_target_2_gy_##
            ├── Optimal_target_3_gy_##
            ├── sub-fake01_Ventral_Attention_net
            ├── sub-fake01_L_dlpfc
            └── optimal_target_1_dscalar.png
            └── optimal_target_1_dscalar.scene
            └── optimal_target_1_dscalar.spec
            └── optimal_target_2_dscalar.png
            └── optimal_target_2_dscalar.scene
            └── optimal_target_2_dscalar.spec
            └── optimal_target_3_dscalar.png
            └── optimal_target_3_dscalar.scene
            └── optimal_target_3_dscalar.spec            
            └── sub-fake01_L_dlpfc_prctile_99_5_best_gy.csv
            └── sub-fake01_Ventral_Attention_L_dlpfc_prctile_99_5_best_gy.csv
            └── sub-fake01_Ventral_Attention_Ventral_Attention_net_prctile_99_5_performance.csv
            └── sub-fake01_Ventral_Attention_Ventral_Attention_net_prctile_99_5_best.csv
```

The final output of this pipeline is contained within the optimal target for the network of interest. In this directory there is an opt_coil_position_brainsight.txt file that can be directly uploaded into Brainsight for TMS stimulations.
