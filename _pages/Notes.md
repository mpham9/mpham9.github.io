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

Try catch
```R
t = TRUE
t = tryCatch(
  {
  ...
  }, error = function(e) FALSE)
```

---

# Paper

Probability of a spike on a given day 9% in VIC, 5% in NSW

https://doi.org/10.1515/snde-2012-0001
https://doi.org/10.1111/1540-6261.00463
https://doi.org/10.1016/j.jbankfin.2007.04.011

https://doi.org/10.1016/j.eneco.2008.04.006
https://doi.org/10.1016/j.eneco.2021.105260

the probability of spike occurrence increases when temperature deviates substantially from mean temperature levels.
https://doi.org/10.1016/j.eneco.2008.05.007

https://doi.org/10.1016/j.energy.2022.123417
https://doi.org/10.1111/j.1540-6261.1997.tb02721.x
https://doi.org/10.1080/10168730000000017
https://doi.org/10.1016/j.enpol.2014.10.016

simple OLS hedge, conditional hedges, minimum variance hedge ratio, traditional naive hedge, GARCH hedges,
https://doi.org/10.1080/00036840210138365


https://doi.org/10.1016/j.eneco.2008.08.003

bid behavior, vesting and bilateral contracts, generation reserve, gaming attitudes
https://doi.org/10.2307/2234783

https://ieeexplore.ieee.org/abstract/document/779387

https://doi.org/10.1016/j.eneco.2013.02.006

electricity portfolio optimization
https://ieeexplore.ieee.org/abstract/document/5712193

cross hedge
https://doi.org/10.1016/S0140-9883(00)00071-2

https://doi.org/10.1016/j.eneco.2021.105101

