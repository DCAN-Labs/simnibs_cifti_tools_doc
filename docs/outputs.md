# Outputs

## Stage 1: Setup

## Stage 2: Simulations

## Stage 3: Optimal Targeting

## Output Folder Structure Old

Once a run is completed, all the files will be saved in the folder you defined as output folder (in this example is `/home/example1/Pilottest`). This folder will contain the following subfolders:

```markdown
├── /home/example1  
    ├── Pilottest
        └── SubjectID        
            └── session
                ├── coord_x_y_z
                   └── derivatives
                       └── Atlas
                       └── Native                   
                   ├── Efield
                       └── Cifti
                           └── Atlas
                           └── Native 
                       ├── Surface
                           └── Atlas
                           └── Native                   
                       └── Volume
                           └── Atlas
                           └── Native                  
                   ├── sim
                       └── fsavg_overlays
                       ├── mni_volumes                
                       ├── subject_overlays            
                       └── subject_volumes              
                   └── opt                 
                └── FEM
```

## Exploring Outputs Old


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
