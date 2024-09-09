# pn2.0-mlst-databases

These are databases for use with the PN2.0 caller.

## Databases

| scheme   | directory |
| ------   | --------- |
| _Campylobacter_ | [db/CAMPY](/db/CAMPY/) |
| _C. botulinum_  | [db/CBOT](/db/CBOT/) |
| _Cronobacter_   | [db/CRONO](/db/CRONO/) |
| _Listeria monocytogenes_ | [db/LISTERIA](/db/LISTERIA/) |
| _Salmonella enterica_    | [db/SALM](/db/SALM/) |
| Shiga toxin producing _E. coli_ | [db/STEC](/db/STEC/) |
| _Vibrio_        | [db/VIBR](/db/VIBR/) |

## Database structure

An MLST database has several standard files in a directory.

| filename | description |
| -------- | ----------- |
| alleles.fasta.gz | (optional) A compressed fasta file of all entries in the blast database |
| alleles_0.* | The blast database |
| aleleleinfo.txt_0 | A four-column file describing each allele in the database as described below |
| loci.tsv | A two column file describing each locus as described below |

### alleleinfo.txt_0

This file has four columns:

* allele, e.g., LMO_1_1
* locus, e.g., LMO_1
* length of allele in nucleotides, e.g., 123
* Is the start and stop required (1) or optional (0)? This is a boolean 1 or 0.

Example:

```text
SALM_1_1        SALM_1  714     1
SALM_1_2        SALM_1  714     1
SALM_2_1        SALM_2  228     1
SALM_25365_823  SALM_25365      501     0
SALM_25365_824  SALM_25365      501     0
SALM_25365_825  SALM_25365      501     0
```

### loci.tsv

This is a tab delimited file containing the locus ID and its respective core/accessory label.

Example:

```text
ID      allele_type
SALM_12272      core
SALM_13534      core
SALM_13975      core
SALM_9997       accessory
SALM_9998       accessory
SALM_9999       accessory
```
