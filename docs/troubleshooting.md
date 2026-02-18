# Troubleshooting

## User needs to change their target after running this pipeline

This section will help explain what to do if the user has already ran this pipeline and obtained optimal targets but wants to change their `--brain_target` or redefine their inclusion criteria for which coordinates are to be simulated and considered for optimal targeting.

To restart the process while maintaining the `FEM` that was previously generated all you need to do is update your `settings_file` script or your `config` file with the updated `--brain_target` or the `--user_provided_table` and `--user_inclusion_column`. It is most important to keep the `--OUTPUT_FOLDER` argument the same between runs to preserve the previously generated `FEM` as this is subject specific and doesn't change depending on the specified `--brain_target`. For more details regarding these arguments see [Users Guide](./args_flags.md).

### Sample config file where the user provides an inclusion/exclusion table

The below sample is assuming you already have a config file and are only adding in the user_provided_table and user_inclusion_column arguments.

```bash
.
.
.
user_provided_table=/full/path/inclusion/table.csv
user_inclusion_column=ROI
```

## Most common issue 2
