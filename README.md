## What's New?
**[04/03/2015]** 1000 Genomes Phase 3 reference panel for DISTMIX will be available soon.

**[02/06/2015]** a pre-compiled executable for DISTMIX (v0.2.0) built under Linux is available now! In this version, we added new option (--populationWeight) that enable users to pre-specify population weights based on their prior information on study cohorts. This option will be quite useful when the input data (GWAS summary statistics data) lacks allele frequency information. See DISTMIX input file second option.

**[01/03/2015]** updated a pre-compiled executable for DISTMIX (v0.1.0).

**[09/24/2014]** a pre-compiled executable for DISTMIX (v0.1.0) built under Linux is available now!

## Introduction

"DISTMIX is a very fast and novel software program for Directly Imputing summary STatistics (two-tailed Z-scores) for unmeasured SNPs from MIXed ethnicity cohorts using measured SNP summary data (including cohort allele frequencies) from the cohorts and external reference populations such as 1000 Genomes data. DISTMIX inherits the main advantage of [DIST](http://dleelab.github.io/dist/), i.e. speed, not requiring subject level genetic data access and applicability to pedigree data, while gaining the capability of accurate imputation of summary statistics from multi-ethnic GWAS/meta-analyses. Compared to commonly used genotype imputation methods, DISTMIX offers quite comparable imputation performance while dramatically reducing computation time and resource usage. DISTMIX software is written in C++ with open-source numerical libraries."

## Citing DISTMIX 

**_DISTMIX: Direct imputation of summary statistics for unmeasured SNPs from mixed ethnicity cohorts_**, Donghyung Lee; Tim B. Bigdeli; Vernell S. Williamson; Vladimir I. Vladimirov; Brien P. Riley; Ayman H. Fanous; Silviu-Alin Bacanu; *Bioinformatics* (2015) [doi:10.1093/bioinformatics/btv348](http://bioinformatics.oxfordjournals.org/content/early/2015/06/27/bioinformatics.btv348.full).

##Acknowledgement
**This work is supported by the National Institutes of Health with grants R25DA26119, R21MH100560, R21AA022717 and P50AA022537.**

<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/US-NIH-NIDA-Logo.svg/440px-US-NIH-NIDA-Logo.svg.png" height="100px">
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/US-NIH-NIMH-Logo.svg/280px-US-NIH-NIMH-Logo.svg.png" height="100px">
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/7/72/US-NIH-NIAAA-Logo.svg/440px-US-NIH-NIAAA-Logo.svg.png" height="100px">

##Download DISTMIX
The current release (Version 0.2.0) of DISTMIX is for a Linux user. The pre-compiled executables for other operating systems (e.g., Windows, MacOS) will be available soon. The latest source codes of DISTMIX are available upon request (dustorm_at_gmail_dot_com). 

|**Direct download link**|**Version**|**Release Date**|
|:---|:---|:---|
|[DISTMIX for a Linux user](https://drive.google.com/file/d/0B_9H56XID17ScTc3ZDFyT0NNNVU/view?usp=sharing)|v0.2.0|02/05/2015|

##Download Reference Panels
|**Direct download link**|**Number of Samples**|**Number of populations**|**NCBI build**|**Release Date**|**Note**|
|:---|:---|:---|:---|:---|:---|
|[1000 Genomes Phase1 Release3](https://drive.google.com/file/d/0B_9H56XID17SLWJaWjlYekxkVkU/view?usp=sharing)|1092|14|build 37 (hg19)|Nov. 23 2010|Includes chr1-chr22|

Here are the 1000 Genome population abbreviations used by DISTMIX. AFR is an abbreviation for African; AMR for admixed American; ASN for East Asian; EUR for European. 

|**Population Abbreviation**|**Number of Subjects**|**Super Population**|**Population Description**|
|:---|:---|:---|:---|
|ASW|61|AFR|African Ancestry in Southwest US|
|CEU|85|EUR|Utah residents (CEPH) with Northern and Western European ancestry|
|CHB|97|ASN|Han Chinese in Beijing, China|
|CHS|100|ASN|Southern Han Chinese|
|CLM|60|AMR|Colombian in Medellin, Colombia|
|FIN|93|EUR|Finnish in Finland|
|GBR|89|EUR|British in England and Scotlant|
|IBS|14|EUR|Iberian populations in Spain|
|JPT|89|ASN|Japanese in Tokyo, Japan|
|LWK|97|AFR|Luhya in Wenbuye, Kenya|
|MXL|66|AMR|Mexican Ancestry from Los Angeles, USA|
|PUR|55|AMR|Puerto Rican in Puerto Rico|
|TSI|98|EUR|Toscani in Italia|
|YRI|88|AFR|Yoruba in Ibadan, Nigeria|

##DISTMIX Input File Format

###When study allele frequency information is available
DISTMIX takes as input a plain text file with rows and columns denoting SNPs and variables, respectively. The first line of the input file should be column names/headers. Data entries on each line should be separated by white space. 
The file should contain seven columns: 1) rsid (SNP ID), 2) chr (chromosome number), 3) bp (base pair position), 4) a1 (reference allele), 5) a2 (alternative allele), 6) z (normally distributed GWAS/meta-analysis summary statistic, i.e. two-tailed Z-score) and  7) af1 (cohort reference allele frequency (RAF)). DISTMIX does not require the input data to be sorted in ascending order by chromosome number and base pair position or SNP ID. Here is a sample DISTMIX input file.


```
rsid        chr  bp         a1  a2  z          af1

rs1000109   9    117908733  C   T  -0.714464   0.384

rs10001109  4    44904653   C   T   0.721919   0.198

rs1000112   22   28273339   C   G  -0.583666   0.042 

rs10001127  4    130547376  T   C   0.069329   0.210 

rs1000113   5    150240076  T   C  -1.447288   0.189
```

###When study allele frequency information is not available
Genome-wide association studies/meta-analyses typically do not provide study allele frequency information due to privacy issues. However, information about ethnic proportion of the study samples is usually available from the publications. By using the prior ethnic information, users can run DISTMIX to impute association summary data lacking allele frequency information. In this case, DISTMIX does not require study allele frequency information (the column ‘af1’) in the input file, but additionally DISTMIX needs one more input text file (population weight file) specifying ethnic proportion of the study samples. Here is a sample DISTMIX input file with 5 SNPs, which should be used when allele frequency information is not available. Actually, this is the DIST input format. 

```
rsid        chr  bp         a1  a2   z   

rs1000109   9    117908733  C   T   -0.714464

rs10001109  4    44904653   C   T    0.721919 

rs1000112   22   28273339   C   G   -0.583666

rs10001127  4    130547376  T   C    0.069329

rs1000113   5    150240076  T   C   -1.447288
```

**Note:** If the input summary data comes a different genome assembly (e.g. NCBI build 36 (hg18)) than NCBI build 37 (hg19), it needs to be converted by the user to NCBI build 37 (hg19) using a software, called [liftover](https://genome.ucsc.edu/cgi-bin/hgLiftOver), from UCSC.


Here is a sample DISTMIX population weight file, which is needed when cohort allele frequency information is not available. 

```
pop	wgt   

ASW	0.1

GBR	0.3

FIN 0.2

CEU	0.25

IBS	0.15
```

The first line of the population weight file should be column names/headers. The file should contain two columns: 1) pop (population abbreviation) and 2) wgt (population proportion). The columns of data should be separated by white space. The weight file name should be specified with the ‘--populationWeight’ option.


##DISTMIX Output File Format

The DISTMIX output file has eleven columns: 1) rsid (SNP ID), 2) chr (chromosome number), 3) bp (base pair position), 4) a1 (reference allele), 5) a2 (alternative allele), 6) waf1 (estimated/observed cohort study RAF), 7) af1 (the reference panel RAF), 8) z (Z-score), 9) info (DISTMIX imputation information score), 10)  pval (p-value) and 11) type (SNP type). The first line of the output file is column names/headers. The sixth column, waf1, contains observed cohort RAFs (i.e. when the SNP is measured) or RAFs estimated as a mixture of ethnicity RAFs from the reference panel (when the SNP is unmeasured). The last column, type, contains 0, 1 or 2. 0 means the corresponding SNP is unmeasured (thus, imputed) one but has been genotyped in the reference panel; 1 means the corresponding SNP is measured one and has been genotyped in the reference panel; 2 means the corresponding SNP is measured one but has not been genotyped in the reference panel. Here is a sample DISTMIX output file, with 5 SNPs:

```
rsid        chr  bp     a1  a2  waf1     af1         z           info        pval      type

rs74970982  1    61442  G   A   0.93133  0.951444    0.00678502  0.252236    0.994586  0

rs62637820  1    61920  A   G   0.06324  0.062992   -0.0502051   0.490445    0.959959  0

rs76735897  1    61987  G   A   0.40114  0.440945   -0.0614578   0.528252    0.950995  0

rs77573425  1    61989  C   G   0.46001  0.458005   -0.0552563   1           0.955934  1

rs28599927  1    62271  G   A   .        .          -0.0314447   1           0.974915  2
```

##Options

|**Option**|**Short Flag**|**Parameter**|**Default**|**Description**|
|:---|:---|:---|:---|:---|
|--version|-v|none|none|Prints version information.|
|--help|-h|none|none|Outputs a full description of all DISTMIX options.|
|--reference|-r|filename|none|The filename of the reference panel data.|
|--referenceIndex|-i|filename|none|The filename of the reference panel index data.|
|--output|-o|filename|out.distmix|The filename of DISTMIX output|
|--chromosome|-c|positive integer between 1 and 22 or string such as "1p” or “2q"|none|The chromosome number (or the chromosome number and arm, e.g., 1q, 22p).|
|--windowSize|-n|decimal|1.0|The size of the DIST prediction window (Mb).|
|--wingSize|-m|decimal|0.5|The size of the area (wing) flanking the left and right of the DISTMIX prediction window (Mb).|
|--populationWeight|-w|filename|none|The filename of the population weight data.|

**Note:** DISTMIX imputes unmeasured SNP statistics within the prediction window based on measured SNP statistics within the extended window (i.e. the prediction window with flanking regions (wings) on both sides)

##Getting Started with Examples

The users are required to download a tgz-compressed directory containing a pre-compiled DISTMIX executable (distmix), sample input files (sample.input.chr22.wthAf1.txt and sample.input.chr22.txt) and a sample population weight file (sample.pop.wgt.txt) from the **Download DISTMIX** section above. A tgz-compressed directory with 1000 Genomes reference panel data sets also should be downloaded from the **Download Reference Panels** section above. The directories can be uncompressed using **tar** with the **-zxvf** options. Let’s assume that the DISTMIX executable (distmix), sample input files and the sample weight file are stored in the same directory. Assume that the reference panel data file and its index file named as "1kg.ref.gz" and "1kg.ref.index.gz" respectively are stored in a directory /path/to/reference/. 

**Scenario 1:** We want to impute unmeasured SNPs on chromosome 22 in the sample input file (sample.input.chr22.wthAf1.txt) containing study allele frequencies and store all imputation results in a text file named as "sample_output_chr22".

```shell
>> ./distmix -c 22 sample.input.chr22.wthAf1.txt -o sample.output.chr22 -r /path/to/reference/1kg.ref.gz -i /path/to/reference/1kg.ref.index.gz
```

Here, we didn't set the size of the prediction window and wing by using options "--windowSize" and "--wingSize", so DISTMIX will use the default size (1 Mb for the DISTMIX prediction window and 0.5 Mb for the wing).

**Scenario 2:** Here, we want to set *the size of the DISTMIX prediction window (--windowSize or -n)* to be 0.6 Mb and *the size of the wing flanking both sides of the prediction window (--wingSize or -m)* to be 0.2 Mb. For this scenario, we can use the following command.

```shell
>> ./distmix -c 22 sample.input.chr22.wthAf1.txt -o sample.output.chr22 -r /path/to/reference/1kg.ref.gz -i /path/to/reference/1kg.ref.index.gz -n 0.6 -m 0.2
```

**Scenario 3:** We want to impute unmeasured SNPs on chromosome arm 22q in the sample input file (sample.input.chr22.txt) lacking study allele frequencies and store all imputation results in a text file named as "sample_output_chr22q". Since the input data does not include allele frequency information, DISTMIX requires a population weight file (sample.pop.wgt.txt) providing proportion information about ethnicities in the study cohort. Usually, this prior information is available from the study publication. For this scenario, we can use the following command.

```shell
>> ./distmix -c 22q sample.input.chr22.txt -o sample.output.chr22q -r /path/to/reference/1kg.ref.gz -i /path/to/reference/1kg.ref.index.gz -w sample.pop.wgt.txt
```
