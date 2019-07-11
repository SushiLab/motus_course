# Using Euler

Euler is the ETH supercomputer. There are two main differences between using euler compared to your own computer.

1. You don't run jobs directly but you submit them to the LSF. The LSF will find a free node and run the job for you.
2. Software is not visible to you by default but has to be loaded first using the module system.


## Module System

Euler comes with a large number of [software](https://scicomp.ethz.ch/wiki/Category:Application) modules preinstalled. That software is by default 'invisible' to you and has to be loaded before you can use it.


**Hands on**

```bash
# login to euler using mobaXterm.
ssh euler
# Use your biolcourse-XX password for login

# type:
module list
# no module is loaded besides the module system
module avail
# shows available modules

# type:
R --help
# R is not loaded on euler
module load r
R --help
# R is loaded now and can be used
module list
# Loaded R loaded other modules too.
```

Keep in mind that you need to reload your modules after the next login to euler.

## LSF - submitting jobs

Euler is a cluster built from hundreds of compute nodes and few submit nodes. You will log in to one of the submit nodes, prepare your data there and then submit the CPU heavy computation to a compute node.  
