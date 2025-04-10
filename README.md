# Phoenix-HPC-nextflow-config
Dans base nextflow.config for running nextflow processes on the Phoenix HPC
- optimised for nf-core
- works with Epi2me workflows
- nextflow will read this if it is kept in the run directory or the ~/ directory
- For specific nextflow pipelines and processes extra argument '-c' can point to those

e.g.
```

process {
  }
  withName: GTDBTK_CLASSIFYWF {
    memory = '200G'
  }
}

```
