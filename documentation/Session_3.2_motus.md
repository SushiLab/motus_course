# Introduction to mOTUs
mOTUs uses 10 of the 40 universal marker genes to taxonomically profile metagenomes, to quantify metabolically active members in metatranscriptomics and to quantify differences between strain populations using single nucleotide variation (SNV) profiles.

---

Today we will show how to use the tool for the first and second of these tasks, profiling metagenomes and metatranscriptomes.

### Running a single sample
The most basic command is ***profile***, which runs the entire mOTUs pipeline with default parameters.
```bash
profile -f <forward reads> -r <reverse reads> -o <output file> -t <no. threads>
```
We will have to put this command into a job submission script as described in the earlier session and then leave it to run in the queueing system.

### Running individual steps
Whilst this is running, let's take a look at the individual steps of the pipeline:

![motus_profile](/images/motus_profile.png)

#### map_tax
This command uses the program *BWA* to align the reads against the mOTUs database. The output is a *SAM* or *BAM* file (*Sequence* or *Binary Alignment/Map*), which is a standard format used by the *SAMtools* set of utilities.

### mOTUs output

### Running multiple samples

### Merging output
