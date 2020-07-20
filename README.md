# vcf_annotator

A SCons script for [Leukemia](https://www.medicalnewstoday.com/articles/142595#types) VCFs annotation and filter.

## Launch the software

From the directory containing the **launch_annotator.scons** script launch it with all the required parameters. The only directory needed **must** be called *00_starting_vcfs* and it should have all the VCF to annotate.
Example:

```
scons -f launch_annotator.scons SNPSIFT_PATH=~/local/snpEff/ GNOMAD_ANNOTATION_FILE_PATH=~/annotations/gnomad.exomes.r2.0.2.sites.vcf.bgz DBSNP_ANNOTATION_FILE_PATH=~/annotations/All_20180423.vcf.gz DBNSFP_ANNOTATION_FILE_PATH=~/annotations/dbNSFP2.9.3_lite.txt.gz FATHMM_RANKSCORE=0.3 GENOME_VERSION=GRCh37.75 AF_VALUE=0.05 AF=AF_NFE  CLINVAR_ANNOTATION_FILE_PATH=~/annotations/clinvar_20180603.vcf JUNK_GENES_FILE_PATH=~/annotations/junk_genes.txt LEUKEMIA_GENES=~/annotations/leukemia_genes.txt COSMIC_FILE_PATH=~/annotations/CosmicCodingMuts.vcf.gz NX=2 RNA_TISSUE_CONSENSUS=~/annotations/rna_tissue_consensus.tsv.zip DEBUG=T
```

## Steps done by the software

1. Add **GT** to VCFs produced by Strelka2. Diretory of results: **01_strelka2_gt**

2. **SnpEff** annotation. Directory of results: **02_snpeff**

3. **gnomAD** annotation. Directory of results: **03_gnomad**

4. **dbSNP** annotation. Directory of results: **04_dbsnp**

5. **dbNSFP** annotation. Diretroy of results: **05_dbnsfp** 

6. **Clinvar** annotation. Directory of results: **06_clinvar**

7. **HIGH** and **MODERATE** filter. Directory of results: **07_high_moderate**

8. **PASS** filter. Directory of results: **08_pass*

9. **AF** filter by alternate allele frequency: Directory of results: **09_population_af**

10. No **Junk** filter out junk genes: Directory of results: **10_no_junk**

11. No **SNPs** filter out SNPs using [COSMIC](https://cancer.sanger.ac.uk/cosmic) VCF file of all coding mutations in the current release. Directory of results: **11_no_snps**

12. **Leukemia genes** keep only genes associated to leukemia or cancer. It includes the genes from [Cancer Gene Census](https://cancer.sanger.ac.uk/census#cl_search) and [Leukemia Gene Literature Database](http://soft.bioinfo-minzhao.org/lgl/). Directory of results: **12_leukemia**

13. Filter out germline variants from VarScan2. It uses the VarScan2 VCF produced by [vs_format_converter.py](https://github.com/PoisonAlien/varscan_accessories) and the [remove_germline_variants_from_varscan.py](https://github.com/alexcoppe/iSeqs2) script from [iSeqs2](https://github.com/alexcoppe/iSeqs2) 

14. Build **tab separated** files from VCFs found in the **12_leukemia** directory. Directory of results: **13_tables**

15. **Gene Expression Filter**, filter out variants based on the level of expression in B, NK, T, bone marrow , dendritic, granulocytes and monocytes normal cells. Data from [rna_tissue_consensus.tsv.zip](https://www.proteinatlas.org/about/download) file Uobtained from [Human Protein Atlas](https://www.proteinatlas.org/about). Directory of results: **14_filtered_by_gene_expression**

16. Build **tab separated** files from VCFs found in the **14_filtered_by_gene_expression** directory

17. Filter tab separated files by **FATHMM_rankscore**. Directory of results: **16_filtered_by_fathmm_tables**


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

- **JUNK_GENES_FILE_PATH** a file containing the list of junk genes. One gene for each line

- **LEUKEMIA_GENES** a file containing the list of genes associated to leukemia or cancer in general. One gene for each line

- **COSMIC_FILE_PATH** the path to the CosmicCodingMuts.vcf.gz file downloaded from [COSMIC](https://cancer.sanger.ac.uk/cosmic) (example: ~/annotations/CosmicCodingMuts.vcf.gz)

- **RNA_TISSUE_CONSENSUS** the path to the rna_tissue_consensus.tsv.zip file downloaded from [The Human Protein Atlas](https://www.proteinatlas.org) (example: ~/annotations/rna_tissue_consensus.tsv.zip)

- **NX** the number to be used for filtering from [The Human Protein Atlas](https://www.proteinatlas.org) (example: 2)

- **DEBUG** T or F, show or do not show debug informations about the launched commands (default: F)
