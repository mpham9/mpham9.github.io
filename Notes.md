---
layout: page
title: "Notes"
permalink: /Notes/
---

**Anaconda setup**

{% highlight python %}
conda create --name ENVNAME python=3.8
conda activate ENVNAME
conda deactivate
conda remove --name ENVNAME --all

conda install jupyter notebook
conda install conda-forge::PKGNAME
conda install spyder

conda config --add channels conda-forge
conda config --set channel_priority strict
{% endhighlight %}
