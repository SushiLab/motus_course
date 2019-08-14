# mOTUsv2 Database Extension (20 min)

The mOTUsv2 database is composed from a large number of published genomes and metagenomic assemblies. One additional feature of mOTUsv2 is that ability to add your own genomes/MAGs/SAGs to improve the profiling of specific microbiomes.

In order to add new genomes to the mOTUsv2 database you need to provide one or multiple genomes that:

- are taxonomically annotated using NCBI ids:
```bash
  DKWZ00000000	2 Bacteria	976 Bacteroidetes	200643 Bacteroidia	171549 Bacteroidales	171551 Porphyromonadaceae	NA unclassified Porphyromonadaceae	2049046 Porphyromonadaceae bacterium
  
  DIDX00000000	2 Bacteria	976 Bacteroidetes	117747 Sphingobacteriia	200666 Sphingobacteriales	84566 Sphingobacteriaceae	28453 Sphingobacterium	NA unknown Sphingobacterium
```
- contain at least 6 of the 10 marker genes


**This will be a demo/explanation of the extender. Running the extender is relatively quick but installation and rebuilding of the mOTUsv2 database would take more then the 20 minutes we have in this session.**


## Installation

The extender tool is an addon tool that has to be downloaded and installed:

```bash
#download extender archive
wget https://motu-tool.org/data/extend_mOTUs_DBv2.tar.gz
#decompress
tar -xzvf extend_mOTUs_DBv2.tar.gz
cd extend_mOTUs_DBv2
#create a conda enviroment with dependencies 
conda env create -f env/update_mOTUs_v2.yaml
cd ..
source activate update_mOTUs_v2
#Motus should be installed without conda
git clone https://github.com/motu-tool/mOTUs_v2.git
cd mOTUs_v2
python setup.py
python test.py
cd ..
MOTUS_DIR=`pwd`/mOTUs_v2/
```

## Required Files

The extender comes with a set of genomes that can be added as a test case.

Each genome needs to be present as fasta file:

[DJUC00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DJUC00000000)
```
>ENA|DJUC01000001|DJUC01000001.1 TPA: Lactococcus lactis isolate UBA6292 UBA6292_contig_1463, whole genome shotgun sequence.
TTCAGCCATTAAGTGAATAAAGAGTTTGGAAGGGTAGCGAAGAGGCTAAACGCGGCGGAC
TGTAAATCCGCTCCTTCGGGTTCGGGGGTTCGAATCCCTCCCCTTCCATAGAAAACGGGC
ATCGTATAAAGGTAGTACAAAGGTCTCCAAAACCTTTAGTGTGGGTTCAATTCCTGCTGC
CCGTGTTTCATTATGGCGGATGTGGTGAAGTGGTTAACACACCGGCTTGTGGCGCCGGCA
CTCGCGAGTTCGATCCTCGTCATCCGCCTTTTTAATGGGGTATAGCCAAGCGGTAAGGCA
AGGGACTTTGACTCCCTCATGCGTTGGTTCGAATCCAGCTACCCCAGTTGTTATGTTTCG
CCGAAGTGGCGGAATAGGCAGACGCGCCAGACTCAAAATCTGGTTCCTTCACGGGAGTGC
CGGTTCGACCCCGGCCTTCGGCATAACATAAAGAGCTAACATGCCTATTGTTAGCTTTTT
...
```
[DBLN00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DBLN00000000)

```
>ENA|DBLN01000001|DBLN01000001.1 TPA: Alphaproteobacteria bacterium UBA723 UBA723_contig_2110, whole genome shotgun sequence.
GTCTCAGATCCGTCAGGACATGCCGTCGAGATCGGCGATAACCTGGCCGGGATGATCGGC
CGGCGTCACTTCGTCATATGCCACGGCGACTTTGCCGTCAGGTCCGATCAACACAGATTT
GCGCGGGGATCGCGTGCTGTCCGGTTCGGACACGCCGAAGGCGATAGAAACGGCGCCTTT
CTCGTCGCTGAGCAGGTCGTAGGGAAACGAGAATTTATCGCGAAACGCGCCGTTGTCCGC
CGGGCCGTCATAACTGATGCCGACGATTGAGGCGTTACGTTCTTCGAAGTCTTGGATTCG
ATCACGGAACCCATTGCCTTCGATGGTTCAGCCGGGCGTATCGGCTTTGGGATACCACCA
GAGAAGGACATAGCGCCCGGCGAAATCGTCTTTCTTCACCGTCTTTCCATCCTGGTTCGG
...
```

[DJPR00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DJPR00000000)

...

[DCXR00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DCXR00000000)

...

[DKWZ00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DKWZ00000000)

...

[DKSV00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DKSV00000000)

...

[DIDX00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DIDX00000000)

...

[DGGF00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DGGF00000000)

...

[DLHH00000000](https://www.ncbi.nlm.nih.gov/genome/?term=DLHH00000000)

...

Each genome needs to have a taxonomic assignation:

```
DBLN00000000	2 Bacteria	1224 Proteobacteria	28211 Alphaproteobacteria	204441 Rhodospirillales	41295 Rhodospirillaceae	NA unknown Rhodospirillaceae	NA unknown Rhodospirillaceae
DCXR00000000	2 Bacteria	NA NA	NA NA	NA NA	NA NA	NA NA	NA Candidatus Microthrix sp. UBA2131
DGGF00000000	2 Bacteria	976 Bacteroidetes	117743 Flavobacteriia	200644 Flavobacteriales	49546 Flavobacteriaceae	59732 Chryseobacterium	253 Chryseobacterium indologenes
DIDX00000000	2 Bacteria	976 Bacteroidetes	117747 Sphingobacteriia	200666 Sphingobacteriales	84566 Sphingobacteriaceae	28453 Sphingobacterium	NA unknown Sphingobacterium
DJPR00000000	2 Bacteria	1239 Firmicutes	186801 Clostridia	186802 Clostridiales	541000 Ruminococcaceae	1263 Ruminococcus	NA unknown Ruminococcus
DJUC00000000	2 Bacteria	1239 Firmicutes	91061 Bacilli	186826 Lactobacillales	1300 Streptococcaceae	1357 Lactococcus	1358 Lactococcus lactis
DKSV00000000	2 Bacteria	1224 Proteobacteria	1236 Gammaproteobacteria	91347 Enterobacteriales	543 Enterobacteriaceae	547 Enterobacter	158836 Enterobacter hormaechei
DKWZ00000000	2 Bacteria	976 Bacteroidetes	200643 Bacteroidia	171549 Bacteroidales	171551 Porphyromonadaceae	NA unclassified Porphyromonadaceae	2049046 Porphyromonadaceae bacterium
DLHH00000000	2 Bacteria	976 Bacteroidetes	768503 Cytophagia	768507 Cytophagales	89373 Cytophagaceae	319458 Leadbetterella	NA unknown Leadbetterella
```
