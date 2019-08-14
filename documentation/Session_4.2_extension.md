# mOTUsv2 Database Extension (20 min)

The mOTUsv2 database is composed from a large number of published genomes and metagenomic assemblies. One additional feature of mOTUsv2 is that ability to add your own genomes/MAGs/SAGs to improve the profiling of specific microbiomes.

In order to add new genomes to the mOTUsv2 database you need to provide one or multiple genomes that:

- are taxinomically annotated using NCBI ids:
```bash
  DKWZ00000000	2 Bacteria	976 Bacteroidetes	200643 Bacteroidia	171549 Bacteroidales	171551 Porphyromonadaceae	NA unclassified Porphyromonadaceae	2049046 Porphyromonadaceae bacterium
  
  DIDX00000000	2 Bacteria	976 Bacteroidetes	117747 Sphingobacteriia	200666 Sphingobacteriales	84566 Sphingobacteriaceae	28453 Sphingobacterium	NA unknown Sphingobacterium
```
- contain at least 6 of the 10 marker genes


**This will be a demo/explanation of the extender. Running the extender is relatively quick but rebuilding the mOTUsv2 database
takes > 15 minutes.**


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
