# rMATS turbo v4.1.2 WDL workflow for AnVIL

This is the rMATS turbo workflow in [Workflow Description Language
(WDL)](https://openwdl.org/) written to run on the
[AnVIL](https://anvil.terra.bio/) cloud platform. Bam files are taken
as input.

## Dependencies

This workflow is written to run on the AnVIL platform powered by
[Terra](https://app.terra.bio/). In order to run locally, `cromwell`
and `womtool` must be
[installed](https://github.com/broadinstitute/cromwell/releases). Run
the workflow locally using:

```
java -jar cromwell-xx.jar run rmatsTurbo.wdl -i xx.json
```

## Example

### Generate input file (`xx.json`)

Prepare the test data, and write them into the `xx.json` file. The
file can be generated with suggested formatting using `womtool`, e.g.,

```
java -jar womtool-xx.jar inputs rmatsTurbo.wdl > test.json
```

The output `.json` file shows all the defined parameters (required and
optional), the data type and default value if optional.

```
{
  "rMATS_turbo.mil": "Int (optional, default = 50)",
  "rMATS_turbo.variable_readLength": "Boolean (optional, default = false)",
  "rMATS_turbo.paired_stats": "Boolean (optional, default = false)",
  "rMATS_turbo.novelSS": "Boolean (optional, default = false)",
  "rMATS_turbo.nthread": "Int (optional, default = 1)",
  "rMATS_turbo.statoff": "Boolean (optional, default = false)",
  "rMATS_turbo.readLength": "Int",
  "rMATS_turbo.lib_type": "String (optional, default = \"fr-unstranded\")",
  "rMATS_turbo.pairedORsingle": "String (optional, default = \"paired\")",
  "rMATS_turbo.tmp_dir": "String",
  "rMATS_turbo.gtf": "File",
  "rMATS_turbo.anchorLength": "Int? (optional)",
  "rMATS_turbo.bam_g2": "Array[File]",
  "rMATS_turbo.tstat": "Int (optional, default = 1)",
  "rMATS_turbo.mel": "Int (optional, default = 500)",
  "rMATS_turbo.task_type": "String (optional, default = \"both\")",
  "rMATS_turbo.bam_g1": "Array[File]",
  "rMATS_turbo.out_dir": "String",
  "rMATS_turbo.cstat": "Float (optional, default = 0.0001)"
}

```

Then open the `.json` file in editor, keep the keys unchanged, and
fill in the values each key is expecting. `(optional)` parameters can
be omitted and default values will be used. Parameter documentation
can be checked in the `rmatsTurbo.wdl` under the `parameter_meta`
sections.

```
{
  "rMATS_turbo.bam_g1": ["../testdata/231ESRP.25K.rep-1.bam", "../testdata/231ESRP.25K.rep-2.bam"],
  "rMATS_turbo.bam_g2": ["../testdata/231EV.25K.rep-1.bam", "../testdata/231EV.25K.rep-2.bam"],
  "rMATS_turbo.gtf": "../testdata/gtf/Homo_sapiens.Ensembl.GRCh37.75.gtf",
  "rMATS_turbo.pairedORsingle": "paired",
  "rMATS_turbo.readLength": 50,
  "rMATS_turbo.nthread": 4,
  "rMATS_turbo.tmp_dir": "rmats_tmp",
  "rMATS_turbo.out_dir": "rmats_out"
}
```

### Run the wdl workflow

Run the wdl workflow locally:

```
java -jar cromwell-xx.jar run rmatTurbo.wdl -i test_bam_default.json
```

OR submit the `xx.json` file to AnVIL under the [`INPUTS`] tab of
`rmats_turbo_bam` workflow. Users can write the `Attribute` column
using `json` format or click on `upload json` on the upper-right
corner of `INPUTS` section. **NOTE** that the `/path/to/test_data`
should be modified to be data path on AnVIL cloud.

Save the editting, and click on `RUN ANALYSIS`. The job will be
submitted with a link of job manager to check for task status. Using
the above `.json` as input, the outputs are compressed into a `.tar`
file in the output directory:

```
rmats_out.tar
```






