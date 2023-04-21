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

# Build Latex Document

```bash
pandoc -V geometry:margin=1in -C --bibliography=refs.bib --listings --csl=default.csl -s h.md -o h.pdf --pdf-engine=xelatex 
```

# Example Table

| Basis Set | Basis Functions Count |
| --------- | --------------------- |
| 6-31G\*   | 19                    |
| cc-pVTZ   | 58                    |

Table: Basis set sizes

# Using Latex Equations

$$
N! = \int_0^\infty e^{Ng(x)}dx =
 \int_0^\infty e^{N \ln{\left(N \right)} - 1 - \frac{\left(x - N\right)^{2}}{2 N^{2}} }dx
$$

The exponential terms that do not contain an x can be separated out and pulled out to the front.

$$
N! = e^{N (\ln{\left(N \right)} - 1)}\int_0^\infty  e^{\frac{\left(x - N\right)^{2}}{2 N^{2}} }dx
$$

# Coding Examples


<!-- target: 1c2-->

```python
import sympy as sp

x = sp.Symbol("x")
N = sp.Symbol("N", positive=True)
# N = sp.Symbol("N")
gx = sp.exp(-(x-N)**2/(2*N))
out = sp.integrate(gx, (x, 0, sp.oo))
print(sp.latex(out))

N = sp.oo
erfc_eval = (2 - sp.erfc(sp.sqrt(2)*sp.sqrt(N)/2))/2
print(erfc_eval)
```

<!-- name: 1c2-- -->

```
\frac{\sqrt{2} \sqrt{\pi} \sqrt{N} \left(2 - \operatorname{erfc}{\left(\frac{\sqrt{2} \sqrt{N}}{2} \right)}\right)}{2}
1
```

This ultimately yields...

$$
N! = e^{N \ln{\left(N \right)} - N} \frac{\sqrt{2\pi N} \left(2 - \operatorname{erfc}{\left(\frac{\sqrt{2} \sqrt{N}}{2} \right)}\right)}{2}
$$

Since N is very large, the erfc portion of the equation effectively becomes 1,
allowing us to remove the portion through an approximation.

$$
N! \approx e^{N \ln{\left(N \right)} - N} \sqrt{2\pi N}
$$

Taking the natural log of this produces...

$$
\ln N! = ln(e^{N \ln{\left(N \right) - N}}\sqrt{2\pi N}) = ln(e^{N \ln{\left(N \right) - N}}) + \ln\sqrt{2\pi N} = N \ln{\left(N \right) - N}  + \ln\sqrt{2\pi N}
$$

# Images

![The water entropy vs. temperature plot shows large jumps in entropy between
the major phase transitions of solid to liquid and liquid to gas.
](images/water.png){width=500px}

# Latex Sections

$$
\newcommand{\newmanalkene}[6][0]{
    \def \alkeneangle {-#1}
    \pgfmathsetmacro{\Cdist}{.3*cos(#1*3)^2}        %   rear atom position
    \def \bondlengthfront {1.25}                %   front atom's bond length
    \def \bondlengthback {.95}                  %   back atom's bond length
    \begin{tikzpicture}
        \coordinate (C1) at (0,0);
        \draw[draw=none] (C1) -- ++(0+\alkeneangle:\Cdist) coordinate (C2);     %   sposta l'atomo posteriore, vedi Cdist
            %
        \coordinate (C1-1) at (90:\bondlengthfront);
        \coordinate (C1-2) at (210:\bondlengthfront);
        \coordinate (C1-3) at (330:\bondlengthfront);
            %
        \draw[draw=none] (C2) -- ++(+90+\alkeneangle:\bondlengthback) coordinate (C2-1) ;
        \draw[draw=none] (C2) -- ++(-90+\alkeneangle:\bondlengthback) coordinate (C2-2) ;
            %
        \draw (C2)  -- (C2-1);
        \draw[double, double distance=2pt] (C2)  -- (C2-2);
        \draw[fill=white] (C1) circle (.6);
            %
        \draw
            (C1) -- (C1-1)
            (C1) -- (C1-2)
            (C1) -- (C1-3);
            %
        \node[inner sep=0,anchor=-90] at (C1-1) {#2} ;
        \node[inner sep=0,anchor=30] at (C1-2) {#3} ;
        \node[inner sep=0,anchor=150] at (C1-3) {#4} ;
        \node[inner sep=0,anchor=-90+\alkeneangle] at (C2-1) {#5} ;
        \node[inner sep=0,anchor=90+\alkeneangle] at (C2-2) {#6} ;
            %
        \draw
            (C1) circle (.6);
    \end{tikzpicture}
}
\newmanalkene[0]{\ce{CH3}}{H}{H}{\ce{CH3}}{O}
\newmanalkene[120]{\ce{CH3}}{H}{H}{\ce{CH3}}{O}
\newmanalkene[180]{\ce{CH3}}{H}{H}{\ce{CH3}}{O}
$$

# Citations

| Rotational Constants | Frequency (cm$^{-1}$) |
| -------------------- | --------------------- |
| A                    | 27.8761               |
| B                    | 14.5074               |
| C                    | 9.2877                |

: Water rotational constants [@hall1967pure]
