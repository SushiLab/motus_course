
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



# Quality Control (15 min)
