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
| OrganismSettings.json | Description of custom settings per schema |

### alleleinfo.txt_0

This file has four columns:

* allele, e.g., SALM_1_1
* locus, e.g., SALM_1
* length of allele in nucleotides, e.g., 714
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

### organismSettings.json

Example:

```json
{
  "AllowInternalStopForAccept": "0",
  "AvgQuality": "30.0",
  "DcMegaBlastWordSize": "11, 12",
  "DcMegaBlastWordSizeDefault": "11",
  "ExpectedPresentLoci": "1235",
  "kmerLen": "35",
  "Length": "1600000",
  "MaxNrGapsForAccept": "100",
  "MinHomolForAccept": "70",
  "MinHomolForDetect": "70",
  "MinOccurrenceForAccept": "1",
  "NrAFPresent": "1235",
  "NrBAFPresent": "1235",
  "NrConsensus": "1235",
  "RequireStartStopCodonForAccept": "1",
  "SubmitNewAlleleComment": "[LabID] / [EntryID]"
}
```

## Hashing function

When the PN2.0 caller is run, this is the function for the hashing algorithm.
Is is based on the MD5 algorithm, but reduces the value to 56 bits.

```python
def hash_sequence(sequence: str) -> str:

    md5 = hashlib.md5(sequence.encode("utf-8"))
    max_bits_in_result = 56
    p = (1 << max_bits_in_result) - 1
    rest = int(md5.hexdigest(), 16)
    result = 0
    while rest != 0:
        result = result ^ (rest & p)
        rest = rest >> max_bits_in_result
    return str(result)
```
