# Simnibs Cifti Tools Overview 

Simnibs cifti tools is an end-to-end standardized toolbox for coil localization informed by individualized functional targets. It is built on top of Simnibs, a tool to simulate electric field propagation in the brain using finite element models (FEM) (Saturnino et al. 2019) as well a pipeline for preprocessing fMRI data [ABCD-HCP], (https://github.com/DCAN-Labs/abcd-hcp-pipeline).

Simnibs-cifti-tools uses the outputs of the ABCD-HCP preprocessed MRI files and a set of coordinates of interest as the target to stimulate.The generated outputs, a FEM, the optimal coil position and orientation, the Electric field projected on the cortex as volume and as a surface, both in native and atlas space are stored in a standardized format. Using this structure enables the pipeline to run multiple jobs in a computer cluster.

The outputs of this pipeline are optimized coil placements for the desired brain region specified at startup and can be directly uploaded into Brainsight's TMS neuronavigation system [Brainsight](https://brainbox-neuro.com/products/brainsight-tms-navigation). In addition to this there are additional visualization outputs generated to aid in decision making when determining which of the top 3 targets to use.

The toolbox is developed according to the [NMIND initiative](https://www.nmind.org/) coding and documentation practices and is intended to be released as a public repository to facilitate reliable and scalable data analysis as well as planning neuronavigated TMS interventions at the individual level.

## Pipeline Description

This pipeline operates in 3 main stages. These stages are all linked together through slurm commands and are tied as dependencies to run in sequential order.

### Stage 1: FEM Generation

In this stage of the pipeline a Finite Element Model (FEM) gets generated based on user provided T1, and T2 MR images. The FEM generation is performed through [headreco](https://simnibs.github.io/simnibs/build/html/documentation/command_line/headreco.html) since we utilize a Simnibs 3 container to do so. This process takes roughly an hour and a half.

### Stage 2: Simulation Generation

Based on the determined candidate coordinates list, simulations are performed in parallel through slurm batch jobs utilizing the parallel module split into groups of 3 so as to minimize resource requests and optimize slurm priority queue. This process varies in length of time from 1 hour to 15 hours depending on the amount of coordinates being simulated as well as the priority given to the submitted simulations by your slurm submitter.

### Stage 3: Optimal Targeting

After all of the potential optimal targets have been simulated a Matlab script determines the optimal targets to stimulate for each network inside of the user provided specified regions of interest. By default the top 3 targets are provided per functional brain network. This process takes between 10 minutes and 20 hours depending on the amount of simulations that were run during stage 2 of this pipeline.

## Notes

For more information regarding setup see [Installation](./Installation.md).
For more information regarding potential settings see [Users Guide](./args_flags.md).