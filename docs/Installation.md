# Installation

1. Obtain a container or singularity image for Simnibs 3
2. Clone Simnibs Cifti Tools from [Github repository](https://github.com/DCAN-Labs/simnibs_cifti_tools)

## System Requirements

- Python 3.6
  - nibabel
  - numpy
  - subprocess
- Matlab
- Workbench Command
- SLURM
- Bash
- Singularity

### Recommended conda environment

Link for the virtual conda environment that we use for Python dependencies below:
```bash
filler way to download and set-up the environment
```

## Simnibs Container

TODO: Upload the `.sif` directly to share the .sif file.

Steps to do so
1. Create GitHub repo
2. Go to Releases
3. Upload `.sif` file

People then download via:
```bash
wget https://fullgithublink.com/releases/download/v1/myimage.sif
```

If the above doesn't work it will need to be converted into a proper docker file then uploaded to dockerhub. 
1. Convert SIF back to Docker
2. Push to Docker Hub (creating a free account or using an existing one)

Alternatively this `.sif` file can be added to an S3 bucket or hosted 

## Simnibs Cifti Tools Github Repository

Clone the Simnibs Cifti Tools GitHub Repo to your local system.

```bash
git clone https://github.com/DCAN-Labs/simnibs_cifti_tools.git
```

## Disclaimer

This software was built and developed on MSI and relies heavily on the resources available by this HCP environment. All system requirements are satisfied if you use this pipeline while on MSI.

# Set up for MSI user 

1. There is a current working version that was cloned from the [Github repository](https://github.com/DCAN-Labs/simnibs_cifti_tools) located at: `/projects/standard/miran045/shared/code/internal/pipelines/simnibs_cifti_tools/production_branch/simnibs_cifti_tools`
2. This installation relies on a containerized Simnibs version 3 existing at `/projects/standard/faird/shared/code/internal/pipelines/container_simnibs/sing_test_simnibs_alone_debian.sif` plus the existing matlab installation version.

