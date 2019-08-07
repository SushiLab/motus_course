# Introduction to mOTUs
mOTUs uses 10 of the 40 universal marker genes to taxonomically profile metagenomes, to quantify metabolically active members in metatranscriptomics and to quantify differences between strain populations using single nucleotide variation (SNV) profiles.

---

Today we will show how to use the tool for the first and second of these tasks, profiling metagenomes and metatranscriptomes.

### Running a single sample
The most basic command is ***profile***, which runs the entire mOTUs pipeline with default parameters.
```bash
motus profile -f <forward reads> -r <reverse reads> -o <output file> -t <no. threads>
```
We will have to put this command into a job submission script as described in the earlier session and then leave it to run in the queueing system.

### Running individual steps
Whilst this is running, let's take a look at the individual steps of the pipeline:

![motus_profile](/images/motus_profile.png)

#### map_tax
This command uses the program *BWA* to align the reads against the mOTUs database. The output is a *SAM* or *BAM* file (*Sequence* or *Binary Alignment/Map*), which is a standard format used by the *SAMtools* set of utilities.
```bash
motus map_tax -f <forward reads> -r <reverse reads> -o <output file> -b -t <no. threads>
```

#### calc_mgc
The intermediate step calculates the number of reads aligned to each marker gene cluster, weighted by gene length.
```bash
motus calc_mgc -n <sample name> -i <bam file> -o <output file>
```
The output format consists of two columns: the name of the marker gene cluster and the count.

#### calc_motu
The final step controls the output format of the final abundance table.
```bash
motus calc_motu -n <sample name> -i <mgc file> -o <output file>
```

### mOTUs output
The standard output format consists of two columns: the mOTU name and the relative abundance of the mOTU in the sample. Note that the table lists all possible mOTUs, i.e.: it includes zeros.
```bash
#consensus_taxonomy     M01.1-V1-stool-metaG
Kandleria vitulina [ref_mOTU_v2_0001]   0.0000000000
Methyloversatilis universalis [ref_mOTU_v2_0002]        0.0000000000
Megasphaera genomosp. [ref_mOTU_v2_0003]        0.0000000000
Streptococcus anginosus [ref_mOTU_v2_0004]      0.0000000000
Streptococcus anginosus [ref_mOTU_v2_0005]      0.0000000000
```

### Merging output
