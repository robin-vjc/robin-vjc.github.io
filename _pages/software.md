---
title: "Software"
layout: single
excerpt: "Software Tools for Optimization, mainly written in Python."
sitemap: false
permalink: /software/
---

All software tools are provided without any guarantee nor liability.

## nsopy

A python package for non-smooth optimization. Github repo [here](https://github.com/robin-vjc/nsopy).

* Installation: ```pip install nsopy```
* Examples
  * [basic usage](https://github.com/robin-vjc/nsopy/blob/master/notebooks/AnalyticalExample.ipynb)
  * [computing approximate solutions to structured MILPs](https://github.com/robin-vjc/nsopy/blob/master/notebooks/ApplicationToDuality.ipynb)


## Parsers
#### SMPS File Reader

* [SMPS reader for Python.](https://github.com/robin-vjc/smps)

[SMPS](http://myweb.dal.ca/gassmann/smps2.htm) is a file format for distributing stochastic multistage models. 
It is an extension of the [MPS file format](https://en.wikipedia.org/wiki/MPS_(format)), which is used to store 
optimization models. 
{: .text-justify}

There is a [parser written in FORTRAN](http://myweb.dal.ca/gassmann/inputs.htm), but I was unable to make it work in my 
Python environment. [Pyomo](http://www.pyomo.org/) has some code to write SMPS files, but not to parse them (see also 
[my request](https://groups.google.com/forum/#!searchin/pyomo-forum/smps/pyomo-forum/jfRD7BK4Mt4/GQqbpAzaBAAJ) on their forum). 
I decided to write a parser script from scratch. It can be used to parse most models from archives such as 
[SIPLIB](http://www2.isye.gatech.edu/~sahmed/siplib/), [POST](http://users.iems.northwestern.edu/~jrbirge/html/dholmes/post.html)
 and [Andy Felt's collection](http://www4.uwsp.edu/math/afelt/slptestset/download.html).
{: .text-justify}
 
Standards are set in the SMPS documentation, but models archives do not always follow them. Also, the parser does not
currently support BLOCK-INDEP mode. If you have troubles parsing some of these files, do not hesitate to contact me.
{: .text-justify}


#### MineLib Reader

* [minelib-read.py]({{site.url}}/publications/minelib_read.txt)

[MineLib](http://mansci-web.uai.cl/minelib/) is a library of optimization model instances related to open-pit 
mine sequencing. [Here](http://emoreno.uai.cl/publicaciones/PREPRINTS/preprint-AOR12-Minelib.pdf) is a description 
of the file format, while [here](http://mansci-web.uai.cl/minelib/Datasets.xhtml) are the datasets.
{: .text-justify}

This Python script does the parsing. It requires the `gurobipy` package.
