---
layout: page
title: "My notes"
permalink: /notes/
published: false
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

Create lower or upper triangular matrix
```R
m = matrix(1:20,4,5)
# make lower triangular matrix
m[upper.tri(m)] = 0
# make upper triangular matrix
m[lower.tri(m)] = 0
```

Load data
```R
df = read.csv("filename.csv",fileEncoding = 'UTF-8-BOM')
```
```R
library(openxlsx)
df  = read.xlsx(filename,sheet=1)
```

Parallel computing
```R
library(foreach)
library(doParallel)
library(parallel)
numCores = detectCores()
cl = makeCluster(numCores-2)
registerDoParallel(cl)
res = foreach (i = 1:n, .packages = c("stringr","dplyr"), .combine = rbind) %dopar% {
  c(a,b,c,d)
}
stopCluster(cl)
```

Measure runtime
```R
start_time = Sys.time()
end_time = Sys.time()
exec_time = end_time - start_time
```


---


