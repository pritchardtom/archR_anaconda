```
module load anaconda/2020.07
source activate
conda create -n arch_r r-base
```

```
conda activate arch_r
```

```
R
install.packages("devtools")
install.packages("BiocManager")
devtools::install_github("GreenleafLab/ArchR", ref="master", repos = BiocManager::repositories())
library(ArchR)
ArchR::installExtraPackages()
```
