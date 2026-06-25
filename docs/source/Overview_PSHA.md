<script>window.MathJax = {"tex": {"inlineMath": [["$", "$"], ["\\(", "\\)"]], "processEscapes": true}, "options": {"ignoreHtmlClass": "tex2jax_ignore|mathjax_ignore|document", "processHtmlClass": "tex2jax_process|mathjax_process|math|output_area"}}</script>
<script defer="defer" src="https://cdn.jsdelivr.net/npm/mathjax@4/tex-mml-chtml.js"></script>

# Overview of Probabilistic Seismic Hazard Analysis (PSHA)
_Aulia Khalqillah, S.Si., M.Si._

Tsunami and Disaster Mitigation Research Center (TDMRC)

Universitas Syiah Kuala, Banda Aceh, Indonesia

auliakhalqillah@usk.ac.id,

&copy; 2026

## What is Probabilistic Seismic Hazard Analysis (PSHA)?

Probabilistic Seismic Hazard Analysis (PSHA) is the method to quantify the ground motion intensity in terms of Peak Ground Accelartion (PGA), Peak Ground Velocity (PGV), and Peak Ground Displacement (PGD) for a site of interest through probabilistically. The site can be a local scale (a city), regional scale (a province, multiple provinces) or global scale (a country, multiple countries in the same continent). The simplicity way to describes this is, what is the probability of exceedance (PoE) at a site of interest for a specific intensity measure level?

## The main procedure to conduct PSHA

In the comprehensive analysis, the PSHA is conducted through four steps.

![](ilustrasi_proses.png)
*Figure 1: The graph is ilustrated by Baker et.al 2021*

1. **Seismic sources definition**; active faults, subduction interfaces/intraslab, and background sources (area or gridded).

2. **Source chracterization**

    Each seismic source consider magnitude ranges and depth ranges  (minimum and maximum) with a certain magnitude and depth bins repectively, and also occurrence rates (related to the probability). This process can be estimated by using Magnitude-Frequency Distribution (MFD) or Characteristic MFD for a certain case, such as an active shallow crust fault. 

3. **Calculating the intensity level**
    
    All these components are calculated by using Ground Motion Prediction Equations (GMPEs) and applied the weigth through the logic tree for each GMPEs and seismic source models due to the uncertainty condition. The GMPEs are calculated based on the site location condition in terms of shear wave velocity up to 30 meters depth (Vs30), magnitude (M), distance (R) from the sources to the site of interest, and others detail parameters. 

4. **Calculating the probability**

    Finally, it will provide a hazard curve for each site of interest that depicts the relationship between annual frequency of exceedance (or probability of exceedance) and intensity measure level. The probabilistic calculation is calculated by using the following equation,
    
    $$\lambda [IMT \ge x] = \Sigma_{source_i}^{n_{source}} \lambda_i(M \ge M_{min}) \int_{M_0}^{M_{max}} \int_{R|M} P[IMT \ge x | M,R] f(M) f(R|M) dr dm$$

    where the

    - $\lambda_i(M \ge M_{min})$ is is the annual rate of occurrence of earthquakes on seismic source $i$. In further analysis, the annual rate of occurrence for the subduction can be calculated by using Gutenberg-Richter's relationship $\lambda_i(M \ge M_{min}) = 10^{a - bM}$ from the earthquake catalog distribution. The $b$ value is estimated by using linear regression. Meanwhile, for the active shallow crust, this parameter is calculated by using its slip-rate through the geological data approach and calculate the annual rate of occurrence by using characteristic earthquake model since the fault has the characteristic earthquake model, which is more sensitive to occur for higher magnitude earthquake rather than lower (small) earthquake. The characteristic earthquake model can be estimated by using YoungsCoppersmith1985 approach.

    - $P[IMT \ge x | M,R]$ is the probability of ground motion intensity level greater than and equal to a certain value of $x$ as function of magnitude (M) and distance (R).

        $$P[IMT \ge x | M, R] = 1 - \phi (\frac {\ln x - \overline {\ln IMT}}{\sigma_{\ln PGA}})$$

        where the $\overline {\ln IMT}$ is the mean/median of ground motion intensity level from the GMPE and $\sigma_{\ln PGA}$ is its standard deviation

    - $f(M)$ is the probability density function of earthquake magnitude

       $$f(M) = \frac {b \ln (10) 10^{-b(M - M_{min})}}{1 - 10^{-b(M_{max} - M_{min})}}$$

        for $M_{min} < M < M_{max}$ and $b$ is b-value

    - $f(R|M) $ is the probability density function of distance from the earthquake source to the site of interest. This can be calculated based on the geometry of seismic sources will be modeled (area source, simple fault source, or complex fault source). Further information can be accessed to the [OpenQuake Engine Testing Procedures](https://cloud-storage.globalquakemodel.org/public/wix-new-website/pdf-collections-wix/publications/OQ%20Testing%20Procedures.pdf).

All these processes will generate a hazard maps for a certain return period and hazard curve

![](example_hazard_curve_2.png)

## Introduction to the main parameters of PSHA

In general, the PSHA aims to answer the question of **what is the annual frequency of exceedance ($\lambda$) for given a probability of exceedance (PoE) that will exceed for a greater than or equal to ground motion intensity level ($x$) and time window ($t$)** as written in equation (1) where $IMT$ is intensity measure type (PGA, PGV, or PGD) and $t$ refer to the exposure period (building life expectancy in years). The $\lambda$ is equivalent to the inverse of return period (RP).


$$\lambda[IMT \ge x] = - \frac {ln (1-PoE)}{t} = \frac {1}{RP} \tag {1}$$

Hence, the return period is

$$RP = \frac {1}{\lambda[IMT \ge x]} \tag {2}$$

In the simple manner, the equation (1) describes the occurrence rate of a single event (e.g. earthquake) will occur within duration of time (return period in years) in any years.

For instance, if the PoE of a certain intensity level that exceed 0.5 g event is $2\%$ or equivalent to the $0.02$ and the building life expectancy is $50$ years, then the $\lambda$ is

$$\lambda[IMT \ge x] = - \frac {ln (1-PoE)}{t} = - \frac {ln (1-0.02)}{50}$$
$$\lambda[IMT \ge x] = - \frac {ln (1-0.02)}{50} = - \frac {ln(0.98)}{50} = - \frac {-0.02}{50} = 0.0004$$

and the return period is

$$RP = \frac {1}{\lambda[IMT \ge x]} = \frac {1}{0.0004} = 2500$$

These values tell us about:

- The earthquake with the intensity level greater than or equal to certain value $x$ where the probability of exceedance of $2\%$ for building life expectancy of 50 years has the occurrence rate of $0.0004$ times per year. It means that this earthquake occurs once every 2500 years in average. However, it does not mean that this earthquake will occur every 2500 year.

## Conducting the PSHA using OpenQuake

**Requirements**

1. OpenQuake software (seet table below to download).

    |Operating Systems|Link|
    |--|--|
    |Installation for Windows | Installation Process - [Link](https://docs.openquake.org/oq-engine/master/manual/getting-started/installation-instructions/windows.html)|
    ||Download page - [Link](https://downloads.openquake.org/pkgs/windows/oq-engine/)|
    |Installation for Mac OS | [Link](https://docs.openquake.org/oq-engine/master/manual/getting-started/installation-instructions/macos.html)|
    |Installation for Ubuntu (Linux) | [Link](https://docs.openquake.org/oq-engine/master/manual/getting-started/installation-instructions/index.html)|

2. Quantum GIS software (for mapping) - https://qgis.org/resources/installation-guide/ - In this tutorial will be used version of 3.28.3

    After the QGIS has been installed, please install the OpenQuake Integrated Risk Modelling Toolkit (https://plugins.qgis.org/plugins/svir/) through the QGIS's plugin menu.

3. Visual Studio Code (for text editor) - latest version - https://code.visualstudio.com/download

**Mode Calculation**

OpenQuake Engine provide several hazard calculation, they are:

- Scenario: the basic calculation of ground intensity level at a site of interest given a seismic source model, magnitude, source-to-site distance, and local site parameter (Vs30)

- Classical PSHA: calculating the probability of exceedance at a site of interest given a number of seismic sources models, magnitude ranges, distance ranges, depth ranges, and some fault mechanism, where the intensity could occure at least once in a given time span.

- Event-Based PSHA: calculating the probability of exceedance at a site of interest through a simulation seismicity using stochastic approach (e.g., random sampling using Monte Carlo). The simulation seismicity will generate stochastic event set (synthetic earthquake catalog) based on range of magnitude, distance, depth, and fault mechanisms and also time span.

## References

1. [Thenhaus, P. C., Campbell, K. W., Chen, W. F., & Scawthorn, C. (2003). Seismic hazard analysis. Earthquake engineering handbook, 8, 1-50.](https://www.researchgate.net/profile/Kenneth-Campbell/publication/329682244_Seismic_hazard_analysis/links/5c194fe7a6fdccfc70586a7e/Seismic-hazard-analysis.pdf)

2. [Baker, J., Bradley, B., & Stafford, P. (2021). Seismic hazard and risk analysis.](https://books.google.com/books?hl=en&lr=&id=preiEAAAQBAJ&oi=fnd&pg=PP1&dq=seismic+hazard&ots=aTGZe-WnqZ&sig=pRCcvPnpkbByxIacplfZqeZ8SKU)

3. [Pagani, M., Monelli, D., Weatherill, G. A. and Garcia, J. (2014). Testing procedures adopted in the development of the hazard component of the OpenQuake-engine. Global Earthquake Model (GEM) Technical Report 2014-09, doi: 10.13117/GEM.OPENQUAKE.TR2014.09, 73 pages.](https://cloud-storage.globalquakemodel.org/public/wix-new-website/pdf-collections-wix/publications/OQ%20Testing%20Procedures.pdf)

4. [Pagani, M., Monelli, D., Weatherill, G. A. and Garcia, J. (2014). The OpenQuake-engine Book: Hazard. Global Earthquake Model (GEM) Technical Report 2014-08, doi: 10.13117/-GEM.OPENQUAKE.TR2014.08, 67 pages.](https://cloud-storage.globalquakemodel.org/public/wix-new-website/pdf-collections-wix/publications/OQ%20Hazard%20Science%201.0.pdf)