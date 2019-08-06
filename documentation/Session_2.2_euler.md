

# Login to Cluster + mOTUSv2 Installation (60min)


The `mOTUsv2` tool uses a set of 10 marker genes to profile metagenomic and metatranscriptomic sequencing datasets.

`mOTUSv2` is capable of running on different operating systems, uses relatively low memory and can be executed on machines with only a few CPUs. However, in order to process all `mOTUSv2` jobs in parallel, we will fall back to use a dedicated compute cluster for today's tutorial.

We will first log in to the cluster and install the mOTUSv2 tool.


-------------------------------

## Connection to the cluster (10min)

Euler is the ETH supercomputer with a large number of compute nodes. During the course you will use Euler to run `mOTUsv2`. To login to euler you open ```mobaXterm```, start a new session and type:

```bash
ssh euler
```
You will be asked if you trust this connection (type yes) and will then be asked for the password (same as for the VM).

Proceed to your work directory (replace biolcourse-XX with your our username):

```bash
cd /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-XX/
```

This is the same folder as you see it on your Windows Desktop and will serve as data folder for all your computations.



**ALL FOLLOWING COMMANDS HAVE TO BE EXECUTED ON EULER AND NOT ON WINDOWS**


-------------------------------

## Quick Linux Introduction (15min)


Being able to use the Linux terminal is an integral part of most bioinformatic workflows. In order to use `mOTUSv2` on Linux we have to know some basic commands:


```bash
# print current directory
pwd
# e.g. /cluster/home/biolcourse-XX/

# change to new directory
cd /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-XX/
pwd
# now you are in /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-XX/

# list all files and folders inside the current directory
ls

# list all files and folders inside a specific directory
ls /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/test/

# go one directory up
cd ..
# now you are in /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/

# inspect a file
less /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/test/test.motus
# Use the cursor to navigate, use space to go one page down, use q to leave the program
```


Mastering the terminal is an incredible useful skill for most bioinformatic workflows. We show you only the minimum number commands that are needed for this tutorial. There're great [tutorials](http://swcarpentry.github.io/shell-novice/) if you would like to continue working with the terminal.




-------------------------------

## mOTUSv2 Installation (30min)

Type `pwd` and make sure that you are in your working directory (`/nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-XX/`).

```bash
# print current directory
pwd
# /cluster/home/biolcourse-XX/
cd /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-XX/
pwd
# /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-XX/
```

We will follow the installation instructions from the [mOTUSv2](https://motu-tool.org/) website. At home you can reuse the installation instructions and tutorials from this website.

The `mOTUSv2` software is written in `python3` and requires the `bwa` aligner and `samtools` as prerequisites. All prerequisites are already installed on euler but need to be loaded:

```bash
# load bwa, samtools and python
module load vcp
module load samtools
module load python/3.6.0
```

Next we install the mOTUSv2 software:


```bash
# Running the setup.py command will take ~1 minute
git clone https://github.com/motu-tool/mOTUs_v2.git
cd mOTUs_v2
python setup.py
export PATH=`pwd`:$PATH
python test.py
cd ..
```

`mOTUSv2` is correctly installed if the last line reads like:

`Check resulting profile: correct`.


-------------------------------

## After each login

**You will need to run these commands after each login. This is due to the nature of how software is handled on euler.**

```bash
# Replace the XX with your username/number
cd /nfs/nas22.ethz.ch/fs2201/biol_isg_course_1/Workshop_Bern/biolcourse-XX/
cd mOTUs_v2
export PATH=`pwd`:$PATH
cd ..
module load vcp
module load samtools
module load python/3.6.0
cd bbmap
export PATH=`pwd`:$PATH
cd ..
```