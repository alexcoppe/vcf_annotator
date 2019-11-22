# vcf_annotator

A SCons script for VCFs annotation and filter.

## Launch the software

From the directory containing the **launch_annotator.scons** script launch it with all the required parameters. The only directory needed **must** be called *00_starting_vcfs* and it should have all the VCF to annotate.
Example:

```
scons -f launch_annotator.scons SNPSIFT_PATH=~/local/snpEff/ GNOMAD_ANNOTATION_FILE_PATH=~/annotations/gnomad.exomes.r2.0.2.sites.vcf.bgz DBSNP_ANNOTATION_FILE_PATH=~/annotations/All_20180423.vcf.gz DBNSFP_ANNOTATION_FILE_PATH=~/annotations/dbNSFP2.9.3_lite.txt.gz   FATHMM_RANKSCORE=0.3 GENOME_VERSION=GRCh37.75 SNPEFF_DATA_DIR=~/annotations AF_VALUE=0.05 AF=AF_NFE  CLINVAR_ANNOTATION_FILE_PATH=~/annotations/clinvar_20180603.vcf  DEBUG=T
```

## Steps done by the software

1. **SnpEff** annotation 

2. **gnomAD** annotation

3. **dbSNP** annotation

4. **dbNSFP** annotation

5. **Clinvar** annotation

5. **HIGH** and **MODERATE** filter

6. **PASS** filter

7. **AF** filter by alternate allele frequency

8. **FATHMM_rankscore** filter


## Needed parameters

- **SNPSIFT_PATH**: the directory containing the SnpSift.jar program

- **GNOMAD_ANNOTATION_FILE_PATH**: the path for the gnomad.exomes file (example: ~/annotations/gnomad.exomes.r2.0.2.sites.vcf.bgz)

- **DBSNP_ANNOTATION_FILE_PATH**: the path for the dbSNP file (example: ~/annotations/All_20180423.vcf.gz)

- **DBNSFP_ANNOTATION_FILE_PATH**: the path for the dbNSFP file (example: ~/annotations/dbNSFP2.9.3_lite.txt.gz)

- **CLINVAR_ANNOTATION_FILE_PATH**: the path for the ClinVar file (example: ~/annotations/clinvar_20180603.vcf)

- **FATHMM_RANKSCORE**: the FATHMM_rankscore obtained from dbNSF to filter (example: 0.75, must be between 0 and 1)

- **SNPEFF_DATA_DIR** the directory where SnpEff will download the annotation files (example: ~/annotations)

-  **AF_VALUE** the maximum value to be used from the alternative allele frequency from a given population (default: 0.05)

- **AF** the population to be used (default: AF_NFE, Non-Finnish European genotypes)

- **DEBUG**: T or F, show or do not show debug informations about the launched commands (default: F)
