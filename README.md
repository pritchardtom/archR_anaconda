# ArchR - Sunbird Instructions

These instructions will help users install and use the R package [ArchR](https://www.archrproject.com/) and its dependencies.

## Installation

The best way to install `ArchR` on Sunbird is to do it yourself using an Anaconda environment.  Please follow the instructions provided below to do this, and contact me if you experience any issues.

### Create the Anaconda Environment and install R

```
module load anaconda/2020.07
source activate
conda create -n arch_r r-base
```

This will create a new Anaconda environment called `arch_r` and install the `R` programming language into it, along with any dependencies that `R` requires in order to run.

Once Anaconda has found all the packages it will need to download, confirm the creation of the environment and wait for it to install.  When the installation has completed, enter the following command to start using your new Anaconda environment:

```
conda activate arch_r
```

You should see your command prompt change from something like this:

```
[a.username@sl2 ~]$
```

To something like this:

```
(arch_r) [a.username@sl2 ~]$
```

This means you are now inside your Anaconda environment and we can start installing `ArchR`.  

### Install `ArchR` and Dependencies

- First we enter the `R` command line interpreter from inside our Anaconda environment by entering: `R` and hitting enter.
- We can now install the dependencies:

```
install.packages("devtools")
install.packages("BiocManager")
devtools::install_github("GreenleafLab/ArchR", ref="master", repos = BiocManager::repositories())
library(ArchR)
ArchR::installExtraPackages()
```

- Everything should now be installed correctly and you can start to use `ArchR`.

## How to Use `ArchR` on Sunbird

- Any computationally-intensive job should be submitted to the `compute` nodes using a SLURM submission script, as per our documentation [here](https://portal.supercomputing.wales/index.php/index/submitting-jobs/).

- Once you have selected the resources you require for your job, you will need to include the following code in your script:

```
module load anaconda/2020.07
source activate
conda activate arch_r
```

- This will load and activate the environment with `ArchR` installed, and you can add further commands to start processing files and so on.
