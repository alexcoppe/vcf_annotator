# vcf_annotator

A SCons script for annotation of VCFs.

## Launch the software

From the directory containing the **launch_annotator.scons** script launch it with all the parameters needed.
Example:

```
scons -f launch_annotator.scons SNPSIFT_PATH=~/local/snpEff/ GNOMAD_ANNOTATION_FILE_PATH=~/annotations/gnomad.exomes.r2.0.2.sites.vcf.bgz DBSNP_ANNOTATION_FILE_PATH=~/annotations/All_20180423.vcf.gz DBNSFP_ANNOTATION_FILE_PATH=~/annotations/dbNSFP2.9.3_lite.txt.gz   FATHMM_RANKSCORE=0.3 GENOME_VERSION=GRCh37.75 SNPEFF_DATA_DIR=~/annotations  DEBUG=T
```

## Parameters

- **SNPSIFT_PATH**: the directory containing the SnpSift.jar program

- **GNOMAD_ANNOTATION_FILE_PATH**: the path for the gnomad.exomes file (example: ~/annotations/gnomad.exomes.r2.0.2.sites.vcf.bgz)

- **DBSNP_ANNOTATION_FILE_PATH**: the path for the dbSNP file (example: ~/annotations/All_20180423.vcf.gz)

- **DBNSFP_ANNOTATION_FILE_PATH**: the path for the dbNSFP file (example: ~/annotations/dbNSFP2.9.3_lite.txt.gz)

- **FATHMM_RANKSCORE**: the FATHMM_rankscore obtained from dbNSF to filter (example: 0.75, must be between 0 and 1)

- **SNPEFF_DATA_DIR** the directory where SnpEff will download the annotation files (example: ~/annotations)

- **DEBUG**: T or F, show or do not show debug informations about the launched commands



## Steps done

1. **SnpEff** annotation 

2. **gnomAD** annotation

3. **dbSNP** annotation

4. **dbNSFP** annotation

5. **HIGH** and **MODERATE** filter

6. **FATHMM_rankscore** filter
