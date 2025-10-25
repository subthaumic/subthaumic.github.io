---
layout: "page"
title: "List of Software"
permalink: "/projects/ep-math-data/list-of-software/"
archived: true
archive_source: "STRUCTURES Wiki"
archive_captured: "Oct 2025"
primary_editor: "Dspitz"
primary_edit_count: "14"
total_edits: "21"
first_editor: "Bleher"
first_edit: "2019-05-05T12:58:20Z"
last_editor: "Dspitz"
last_edit: "2019-05-21T15:06:25Z"
---
> This article was originally written by Daniel Spitz for the STRUCTURES Wiki (captured October 2025).


In recent years, a whole landscape of software emerged that deals with computational topology tasks in different fashions. On this page, we provide starting points for the selection of software suited for the problem of interest.

Packages described here include the following: 
- CGAL (https://www.cgal.org/)
- JavaPlex (https://github.com/appliedtopology/javaplex), [Tutorial](https://wiki.structures.mathi.uni-heidelberg.de/index.php?title=JavaPlex_Tutorial)
- GUDHI (http://gudhi.gforge.inria.fr/), [Tutorial](https://wiki.structures.mathi.uni-heidelberg.de/index.php?title=GUDHI_Tutorial)
- Ripser (https://github.com/Ripser)
- PHAT (https://github.com/blazs/phat)
- Dionysus (http://www.mrzv.org/software/dionysus)
- R-Package TDA (https://cran.r-project.org/web/packages/TDA/index.html)
- Perseus (http://www.sas.upenn.edu/~vnanda/perseus/index.html)
- Rivet (http://rivet.online/)

This collection has been created without any claim of comprehensiveness. Whoever is aware of interesting topological data analysis software packages not listed here may contact the authors by mail at structures-hiwi@mathi.uni-heidelberg.de.

## Overview
The following table summarizes information from Otter et al  and Wikipedia. Nomenclature within the following table follows Otter et al .
**Software** | **CGAL** | **JavaPlex** | **GUDHI** | **Ripser** | **PHAT** | **Dionysus** | **R-Package TDA** | **Perseus** | **Rivet**
Language | C++ | Java, Matlab | C++ | C++ | C++, Python bindings | C++, Python bindings | R | C++ | stand-alone
Filtrations computed | alpha | VR, W, W_v | VR, alpha, W, lower star of  cubical complex | VR | - | VR, alpha, Čech | VR, alpha, sublevels of  function on grid | VR, lower star of  cubical complex | VR
Persistent homology computation | no | yes | yes | yes | yes | yes | yes | yes | yes
Homology | - | simplicial,  cellular | simplicial | simplicial | simplicial, cubical | simplicial | simplicial | simplicial, cubical | simplicial
Coefficient field | - | [math]\mathbb{Q}[/math], [math]\mathbb{F}_p[/math] | [math]\mathbb{F}_p[/math] | [math]\mathbb{F}_p[/math] | [math]\mathbb{F}_2[/math] | [math]\mathbb{F}_2[/math] (standard, zigzag),  [math]\mathbb{F}_p[/math] (dual) | [math]\mathbb{F}_2[/math]? | [math]\mathbb{F}_2[/math] | [math]\mathbb{F}_2[/math]?
Remarks | Provides a lot of versatile geometry algorithms | Routines for two-dimensional persistence computations

## Details
### CGAL
The basic design of CGAL is described in Fabri et al 2000. 

The software's webpage can be found here: https://www.cgal.org/.

### JavaPlex
The basic design of JavaPlex is described in Adams et al 2014. 

We provide an introductory tutorial to Javaplex on a different [page](https://wiki.structures.mathi.uni-heidelberg.de/index.php?title=JavaPlex_Tutorial). 

The software's webpage can be found here: https://www.cgal.org/.

### GUDHI
The basic design of GUDHI is described in Maria et al 2014. 

We provide an introductory tutorial to using GUDHI on a different [page](https://wiki.structures.mathi.uni-heidelberg.de/index.php?title=GUDHI_Tutorial). 

The software's webpage including tons of useful example codes can be found here: http://gudhi.gforge.inria.fr/.

### Ripser
The software's webpage can be found here: https://github.com/Ripser.

### PHAT
The basic design of the Persistent Homology Algorithms Toolbox (PHAT) is described in Bauer et al 2017.

The software's webpage can be found here: https://github.com/blazs/phat.

### Dionysus
The software's webpage can be found here: http://www.mrzv.org/software/dionysus.

### R-Package TDA
The Package TDA provides an R interface for the algorithms of the C++ libraries GUDHI, Dionysus and PHAT. 

For an extensive reference manual and further information the reader may consult https://cran.r-project.org/web/packages/TDA/index.html.

### Perseus
The efficient Morse-theoretic algorithm to compute persistent homology implemented in Perseus has been descibed first in Mischaikow and Nanda 2013. 

For details on the software we refer to http://www.sas.upenn.edu/~vnanda/perseus/index.html.

### Rivet
The software Rivet is described in . The software's webpage can be found here: http://rivet.online/.

## References
