
# Data (5 min)

For this course we will use public datasets from [Heintz-Buschart, A. et al. Integrated multi-omics of the human gut microbiome in a case study of familial type 1 diabetes](https://www.nature.com/articles/nmicrobiol2016180).

This study comprises in total 89 sequencing datasets of which 53 come from metagenomic and 36 come from metatranscriptomic sequencing.

Forward and reverse read files for all samples can be found here: `/nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/data`.

```bash
ls /nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/data

  M01.1-V1-stool-metaG
  M01.2-V3-stool-metaG
  M01.4-V2-stool-metaT
  M02.1-V3-stool-metaT
  ...

ls /nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/data/M01.1-V1-stool-metaG/*
  
  M01.1-V1-stool-metaG/M01.1-V1-stool-metaG.1.fq.gz # forward read file
  M01.1-V1-stool-metaG/M01.1-V1-stool-metaG.2.fq.gz # reverse read file
```

You will perform the first steps of analysis (QC and mOTUsv2) on **one** dataset that is linked to your own folder (e.g. `/nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-35` for the user with username `biolcourse-35`).

The user `biolcourse-35` has 2 files in the folder:


```bash

ls /nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-35

  M01.1-V1-stool-metaG.1.fq.gz # forward read file
  M01.1-V1-stool-metaG.2.fq.gz # reverse read file
  
```

Everyone will have a different sample to work on. That is why we refer to read files the following:

```

for user biolcourse-35

<forward raw reads> --> /nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-35/M01.1-V1-stool-metaG.1.fq.gz
<reverse raw reads> --> /nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-35/M01.1-V1-stool-metaG.2.fq.gz

or for user biolcourse-34

<forward raw reads> --> /nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-35/M02.1-V3-stool-metaT.1.fq.gz
<reverse raw reads> --> /nfs/nas22/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-35/M02.1-V3-stool-metaT.2.fq.gz

```


# Quality Control (15 min)

The sequence files that you download from your sequencing center usually come with only basic quality control performed. E.g. The sequencing center knows when a run failed and will not deliver those results. Consequently the quality control of raw sequencing data is your first task before starting any downstream analysis. 

There is a large number of tools that perform Read QC. But most tools try to perform three crucial steps:

1. **Remove Adapters** - Before sequencing you add adapters to insert in order for it to bind to the flowcell. The sequencer sometines reads into those adapters --> Need to remove beginning/end of the sequence that contains adapter sequences
2. **Contamination** - Your metagenomic sample contains host DNA (e.g. Human) or artifical spike-ins (e.g. Phi X) which is then being sequenced --> Remove full sequences that come from host contamination.
3. **Base Quality** - The most common error in Illumina sequencing is the introduction of wrong bases (mutations not indels) into the resulting sequence. This problem is especially prominent towards the end of the sequences. --> Remove the low quality tail of sequences based on quality scores. 

We will run a pipeline that combines all three steps and creates qc'ed read files that we can use as input for mOTUsv2.


*There're many options on how to tweak the performance of the QC step. We use a similar pipeline in our lab and we're confident that it produces solid results. For your own data you will need to look into the pipeline and find parameters that suit your analysis best.*



