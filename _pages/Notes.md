---
layout: page
title: "My notes"
permalink: /notes/
---

# Anaconda setup

Create/delete environments
```
conda create --name ENVNAME python=3.8
conda activate ENVNAME
conda deactivate
conda remove --name ENVNAME --all
```

Add the channel "conda-forge" to the top of the channel list, making it the highest priority:
```
conda config --add channels conda-forge
```

Activate strict channel priority. This will ensure that all the dependencies come from the conda-forge channel unless they exist only on defaults.
```
conda config --set channel_priority strict
```

Install packages
```
conda install jupyter notebook
conda install conda-forge::PKGNAME
conda install spyder
```

---

# R

Install packages if not available
```R
pkg="dplyr"; if (!require(pkg,character.only=TRUE)) install.packages(pkg)
library(pkg,character.only=TRUE)
```
Matrix to vector
```R
# sort by column
vector = c(matrix)

# sort by row
vector = c(t(matrix))
```
---


