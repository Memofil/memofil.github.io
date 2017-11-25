---
layout: default
title:  "Essentiels - Python "
date:   2017-10-04 00:09:36 +0200
categories: Python 
tags: Python 
---

# Essentiels - Python

## Importer des librairies via `sys.path`


```
- PythonApp
    - package_1
    - tools
      - graphics
  - package_2
    -  ui

``` 
En ajoutant au `sys.path` la racine du projet, on peut alors importer les packages depuis n'importe quel sous-dossier du projet : 

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sun Nov  5 18:18:23 2017
file : ui.py
"""
import os
import sys
import re
pathToFile = os.path.dirname(os.path.realpath(__file__))
projectPath = "PythonApp/"
base = re.split(projectPath, pathToFile)[0] + projectPath
sys.path.append(base)
import package_1.tools.graphics as graphics

```



### Sources : 

* [Les imports en Python](http://sametmax.com/les-imports-en-python/){:target="_blank"}
