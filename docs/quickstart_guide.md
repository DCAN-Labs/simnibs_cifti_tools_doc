# Quickstart Guide

The goal of this section is to help users get started using this tool as quickly as possible focusing on the bare essentials.

## Required Input Files

The mandatory input files include a T1, T2, inflated, the Native 32k resolution pial, white, and midthickness surfaces for both left and right hemispheres, and three Dlabel files. For guidance regarding imaging inputs see [Imaging files](./dependancies.md). 


## Required Arguments

In order for this tool to run paths to each of the required input files need to be provided as shown in the below table.

### Input Arguments

| File | Argument |
| T1 structural file | --P_T1w |
| T2 structural file | --P_T2w |
| Left_32k_midthickness.surf.gii | --P_L_mdthk_native |
| Right_32k_midthickness.surf.gii | --P_R_mdthk_native |
| Left_32k_white.surf.gii | --P_L_white_native |
| Right_32k_white.surf.gii | --P_R_white_native |
| Left_32k_pial.surf.gii | --P_L_pial_native |
| Right_32k_pial.surf.gii | --P_R_pial_native |
| Left_inflated_32k.surf.gii | --P_L_inflated |
| Right_inflated_32k.surf.gii | --P_R_inflated |
| func_dlabel.nii | --P_F_dlabel |
| aparc_aseg_dlabel.nii | --P_A_dlabel |
| aparc_aseg_2009_dlabel.nii | --P_A_dlabel_2009 |

The required subject settings are subject and session identifier. 

### Subject Arguments

| Category | Argument |
| Subject ID | --SID |
| Visit ID | --VISIT |

For the scripts to find each other the full path to where the cloned Simnibs Cifti Tools Repo needs to be provided. 

| Category | Argument |
| Full_path_SCT_repo | --P_SCT_REPO |

The mandatory configuration settings include your brain target, threshold, and where to store outputs

| Category | Argument |
| Brain target | --brain_target |
| Threshold | --threshold |
| Work directory | --work_location |

## Settings Script

TODO this section next.

## Running the Pipeline

## Expected Outputs

Short description

### Taken from another section and being stored here 
1. There is a current working version that was cloned from the [Github repository](https://github.com/DCAN-Labs/simnibs_cifti_tools) located at: `/projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/production_branch/simnibs_cifti_tools`
2. This installation relies on a containerized Simnibs version 3 existing at `/projects/standard/faird/shared/code/internal/pipelines/container_simnibs/sing_test_simnibs_alone_debian.sif` plus the existing matlab installation version\
3. Ensure you know the full path to the left and right hemisphere surfaces in **32k native space resolution** for the following surfaces for your desired subject:
    1. Midthickness
    2. Pial
    3. White

<!-- -->

4. Ensure you have the full paths to the T1w & T2w of the desired subject in native resolution.
5. Have available the full paths to the functional dlabel file you would like to use as well as the subjects **aparc aseg dlabel files**.
6. Make your own subject specific settings file script following the example seen at [Sample settings file](./basic_example/default_settings_file.sh)
7. For an example on using the code for the Efield Generator, follow the instructions at [Running an example](https://simnibs-cifti-tools-rtd2.readthedocs.io/en/latest/Efield_generator/#running-an-example)

*To resample higher resolution surfaces down to 32k resolution see [FAQ](https://simnibs-cifti-tools-rtd2.readthedocs.io/en/latest/FAQ/)* *To generate subject specific aparc aseg dlabel files see [FAQ](https://simnibs-cifti-tools-rtd2.readthedocs.io/en/latest/FAQ/)*
