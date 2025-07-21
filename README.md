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
  config_profile_description = 'Dans Phoenix HPC nextflow config'
  config_profile_contact = 'daniel.thomson@adelaide.edu.au'
  max_memory = 188.GB
  max_cpus = 64
  max_time = 72.h
  igenomes_base = '/home/a1205810/references/igenomes'
}

process {
  resourceLimits = [
        memory: 188.GB,
        cpus: 64,
        time: 48.h
    ]
   beforeScript = 'module load Singularity/3.10.5'
   executor = 'slurm'
   maxRetries = 2
   clusterOptions="-N 1 -p icelake,highmem"
}

singularity {
  enabled = true
  autoMounts = true
  cacheDir="/hpcfs/users/a1205810/"
  envWhitelist = 'SINGULARITY_BINDPATH'
}

executor {
    queueSize       = 50
    submitRateLimit = '10 sec'
}

profiles {
    debug {
        cleanup = false
    }
}

// Set custom cache directory
cache {
    dir = '/hpcfs/users/a1205810/containers/'
}
```
