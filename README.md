# Phoenix-HPC-nextflow-config
Dans base nextflow.config for running nextflow processes on the Phoenix HPC
- optimised for nextflow / nf-core 
- nextflow will read this if it is kept in the run directory, or can be specified with -c 
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

nextflow.config
```
params {
  config_profile_description = 'Dans Phoenix HPC nextflow config Aug2025'
  config_profile_contact = 'daniel.thomson@adelaide.edu.au'
  max_memory = 188.GB
  max_cpus = 64
  max_time = 72.h
  igenomes_base = '/home/$USER/references/igenomes'
}

process {
   beforeScript = 'module load Singularity/3.10.5'
   beforeScript = 'module load Nextflow/25.04.3'
   executor = 'slurm'
   maxRetries = 2
}

singularity {
  enabled = true
  autoMounts = true
  cacheDir="/hpcfs/users/$USER/"
  envWhitelist = 'SINGULARITY_BINDPATH'
}

executor {
    queueSize       = 20
    submitRateLimit = '10 sec'
}

profiles {
    debug {
        cleanup = false
    }
}

// Set custom cache directory
cache {
    dir = '/hpcfs/users/$USER/containers/'
}
```
