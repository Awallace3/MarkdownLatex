# MarkdownLatex
Provides a template for making markdown files for nice latex output.

# Build Latex Documents
- Require refs.bib and default.csl files (can get from [example1](.example))
```bash
pandoc -V geometry:margin=1in -C --bibliography=refs.bib --listings --csl=default.csl -s h.md -o h.pdf --pdf-engine=xelatex 
```
- need h.md to have header below (see example1 [here](./example1/h.md))
```md
---
title: Computational Chemistry Example
date: 2023-04-21
author: Austin M. Wallace
reference-section-title: "References"
link-citations: true
link-bibliography: true
header-includes:
  - \usepackage{cancel}
  - \usepackage{fancyvrb}
  - \usepackage{listings}
  - \usepackage{amsmath}
  - \usepackage[version=4]{mhchem}
  - \usepackage{xcolor}
  - \usepackage{chemmacros}
  - \chemsetup{formula=mhchem,modules=newman}

  - \lstset{breaklines=true}
  - \lstset{language=[Motorola68k]Assembler}
  - \lstset{basicstyle=\small\ttfamily}
  - \lstset{extendedchars=true}
  - \lstset{tabsize=2}
  - \lstset{columns=fixed}
  - \lstset{showstringspaces=false}
  - \lstset{frame=trbl}
  - \lstset{frameround=tttt}
  - \lstset{framesep=4pt}
  - \lstset{numbers=left}
  - \lstset{numberstyle=\tiny\ttfamily}
  - \lstset{postbreak=\raisebox{0ex}[0ex][0ex]{\ensuremath{\color{red}\hookrightarrow\space}}}
  - \lstset{keywordstyle=\color[rgb]{0.13,0.29,0.53}\bfseries}
  - \lstset{stringstyle=\color[rgb]{0.31,0.60,0.02}}
  - \lstset{commentstyle=\color[rgb]{0.56,0.35,0.01}\itshape}
---

```
