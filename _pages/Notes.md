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
conda env remove -n corrupted_env
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

List installed packages in an environment
```
conda list
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

Extract number using pattern
```R
library(NCmisc)
library(stringr)
res = list()
j = 1
df = readLines("filename.lp")
for(i in 1:length(df)){
  if(str_detect(df[i],"(?<=\\+\\s)[0-9\\.]+(?=\\sConVio_N1_BuildLimit)")){
    print(df[i])
    print(str_extract_all(df[i],"(?<=\\+\\s)([0-9\\.]+)(?=\\sConVio_N1_BuildLimit)")[[1]])
    res1[[j]] = str_extract_all(df[i],"(?<=\\+\\s)([0-9\\.]+)(?=\\sConVio_N1_BuildLimit)")[[1]]
    j = j+1
  }
}
```

Convert HEIC file to pdf
```R
library("magick")
n = dir()
for (i in 1:length(n)){
  tmp = image_read(n[i])
  image_write(tmp,paste0(i,".pdf"),format="pdf")
}
```

Reshape data wide and long
```R
library(tidyr)
# wide to long
df = df %>% gather(key="Generator",value="Value", col_list[3:10])
# long to wide
df = df %>% gather(Property, Value)
```

Read excel data as datetime
```R
library(datetimeutils)
df$Datetime = convert_date(df$Datetime,type="Excel",fraction=TRUE)
```
