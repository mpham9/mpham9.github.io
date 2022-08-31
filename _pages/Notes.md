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

Split text file
```R
file.split(fn, size = 50000, same.dir = FALSE, verbose = TRUE, suf = "part", win = TRUE)
```

---

# Python

Insert column into Pandas dataframe
```Python
df.insert(loc: 'int', column: 'str|number|hashable', value: 'scalar|serires|array-like', allow_duplicates: 'bool'=False)
df.insert(5,'Scenario','')
```

Extract table from PDF file
```Python
import tabula
df = tabula.read_pdf('filename.pdf',pages=2)
df.to_excel('filename_p2.xlsx')
```

Extract number using pattern
```Python
import re
filename = "filename.lp"
regex = '(?<=\\+\\s)[0-9\\.]+(?=\\sConVio_N1_BuildLimit)'
match_list = []
with open(filename, "r") as file:
    for line in file:
        for match in re.finditer(regex, line):
            match_text = match.group()
            match_list.append(match_text)
            print(line)           
len([float(i) for i in match_list if float(i) != 0])
sum([float(i) for i in match_list])
```
