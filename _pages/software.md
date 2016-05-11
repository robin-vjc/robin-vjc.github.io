---
title: "Software"
layout: single
excerpt: "Some Software Tools."
sitemap: false
permalink: /software/
---

All the software tools below are provided without any guarantee.

## SMPS Files Reader (Python)

* [smps-read.py](https://github.com/robin-vjc/fastDD/blob/master/applications/stochasticMIP/smps_read.py)

[SMPS](http://myweb.dal.ca/gassmann/smps2.htm) is a file format for distributing stochastic multistage models. 
It is an extension of the [MPS file format](https://en.wikipedia.org/wiki/MPS_(format)), which is used to store 
optimization models. 

There is a [parser written in FORTRAN](http://myweb.dal.ca/gassmann/inputs.htm), but I was unable to make it work in my 
Python environment. [Pyomo](http://www.pyomo.org/) has some code to write SMPS files, but not to parse them (see also 
[my request](https://groups.google.com/forum/#!searchin/pyomo-forum/smps/pyomo-forum/jfRD7BK4Mt4/GQqbpAzaBAAJ) on their forum). 
I decided to write a parser script from scratch. It can be used to parse most models from archives such as 
[SIPLIB](http://www2.isye.gatech.edu/~sahmed/siplib/), [POST](http://users.iems.northwestern.edu/~jrbirge/html/dholmes/post.html)
 and [Andy Felt's collection](http://www4.uwsp.edu/math/afelt/slptestset/download.html).
 
Standards are set in the SMPS documentation, but models archives do not always follow them. Also, the parser does not
currently support BLOCK-INDEP mode. If you have troubles 
parsing some of these files, do not hesitate to contact me.



## MineLib Parser (Python)


## Robust Scheduler for STNs

## fastDD (Distributed methods for Stochastic Models, and graphical models)

