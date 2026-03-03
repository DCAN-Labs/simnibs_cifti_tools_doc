# Modularized Tools

There are several features in the Simnibs Cifti Tools GitHub repository that are modularized and can be run independently of the whole pipeline if desired.

## Resample fMRIPrep native surfaces to 32k resolution

Script location: `simnibs_cifti_tools/preprocessing/resample_native_surfaces.sh`
Inputs:

* Needs the path to where the fMRIprep surfaces are
* Also needs this file *hemi-{L,R}_space-fsLR_desc-msmsulc_sphere.surf.gii to be at the same path pointed to
* Path to the Template files directory. Can be downloaded from [templateflow/tpl-fsLR](https://github.com/templateflow/tpl-fsLR)

Outputs: to the same path

* States which files have been made in the terminal
* Saves a log of this as resample_log.txt in the directory where you run the resample_native_surfaces.sh script.

Example:

```bash
/projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/production_branch/simnibs_cifti_tools/preprocessing/resample_native_surfaces.sh /scratch.global/baron063/shared/recode/testing /projects/standard/miran045/shared/code/external/templateflow/tpl-fsLR
```

## Convert annot files (aparc dlabel.nii generation)

Script location: `simnibs_cifti_tools/preprocessing/make_annot_dlabel.sh`
Inputs:

* ids #Everything after sub-
* output_dir #Recommended place is where the other fmriprep_anat_derivitives_dir is
* s3_bucket # the location where sourcedata/freesurfer for the subject is
* session

Outputs:

* where the aparc dlabels have been made and are being stored
* States which files have been made in the terminal. Also saved as make_annot_dlabel_log.txt in the directory where you run make_annot_dlabel.sh

Example:

```bash
/projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/production_branch/simnibs_cifti_tools/preprocessing/make_annot_dlabel.sh TCBXX /scratch.global/baron063/shared/recode/testing s3://recode-rawdata/derivatives/fmriprep/sub-TCBXX/sourcedata/freesurfer/sub-TCBXX/ ses-Y
```

## Aux Tools

description of Aux Tools 

```
def check_if_fem_exist(output_folder):
“””
This function checks if the output_folder is an existing directory or not, if the FEM exists, and if the Mesh File exists. If the output folder doesn't exist, it creates a new directory for the output_folder. Based on the existence of the FEM and Mesh file, the function produces a boolean for each variable. If the FEM and or Mesh file doesn't exist, the function returns a false boolean for each variable. 
Arguments:
	output_folder: path to the output folder to store the results and FEM, if it doesn't exist, it will be created. 
Returns: 
	bool_fem_dir: a binary variable, having two possible values called “true” and “false.” If the FEM exists, the value is true. If the FEM doesn't exist, the value is false. 
	bool_fem_file: a binary variable, having two possible values called “true” and “false.” If the Mesh file exists, the value is true. If the mesh file doesn't exist, the value is false.

“”””
return bool_fem_dir and bool_fem_file
```
```
def get_ids(path_mri_processed_data):
“””
From the provided path to processed MRI data, the function creates variables indicating the subject ID and visit. 
Arguments:
	path_mri_processed_data: path to processed MRI data
Returns: 
	subjectID: name of the subject
	visit: session name
“”””
return subjectID, visit
```
```
def mni2native(subjectID,XYZ_atlas,full_path_to_simnibs_container,path_to_fem,path_to_this_code,output_folder):
“””
This function takes the XYZ coordinates in atlas space,  saves it in a csv file and uses it to convert the coordinates into native space using each participant's FEM. The function creates the output folder for the given coordinate in Native space. 
Arguments:
	subjectID: name of subject
	XYZ_atlas:  coordinate of vertex in atlas space in X Y Z format 
	full_path_to_simnibs_container: full path to the simnibs container 
	path_to_fem: structure of path to access each participants FEM 
	path_to_this_code:
	output_folder: path to the output folder to store the results
Returns: 
	XYZ_native: coordinate of vertex in native space in X Y Z format 
“”””
return XYZ_native
```

```
def get_coord_from_csv_file(csv_file):
“””
This function takes a csv file and formats it into an array. 
Arguments:
	csv_file: The CSV (Comma-Separated Values) file format contains structured information that is separated. This file stores a desired coordinate. 
Returns: 
	XYZ_array: Arrays are used to store multiple values in one single variable. This 
array stores the coordinate of vertex in native space

“”””
return XYZ_array
```
```
def write_coord_to_csv_file(coordinate_csv_file_name,XYZ_array):
“””
This function takes the coordinate array and writes it into a csv file. This csv is in the format needed for simnibs. 
Arguments:
	coordinate_csv_file_name: creates a csv file named after the desired 
	coordinate containing the coordinate in a format that is accepted by simnibs. 
	XYZ_array: Arrays are used to store multiple values in one single variable. This 
	array stores the coordinate of vertex in native space
“”””
```

## Cifti to Volume (Atlas and Native)
- Description : Map the content of a cifti file (dscalars, pscalars, dlabels) into a volume file (yes, no white matter) in both atlas space and in native space. White matter would be filled with NaN's. (check if nifti accept NaN's)
This convertion includes cortical and subcortical structures
- Input
    - Mandatory
      - Cifti file , File that contain the values to be mapped into the volume. 
      - Cortical ribbons (pial and white matter, left and right)
      - Subject Volume reference (can be native or atlas, but same as used in the cifti file used as input)
    - Optional
      - Atlas to native transformation matrix
- Outputs : Output volume in same space 

## Volume to Cifti (Atlas and Native)

- Description
- Input
- Output

## Read coordinates from file

## Cifti to table of coordinates with label (i.e. Network label) (Base for Brain_to_coordinate_text)

## Extract brain structures (from aseg, dlabel, to cifti and/or volume)
