# Overview of Probabilistic Seismic Hazard Analysis (PSHA)
Aulia Khalqillah, S.Si., M.Si.
Tsunami and Disaster Mitigation Research Center (TDMRC)
Universitas Syiah Kuala, Banda Aceh, Indonesia
_auliakhalqillah@usk.ac.id_

&copy;2026

## Topics

1. What is Probabilistic Seismic Hazard Analysis (PSHA)?
2. Introduction to the main parameters of PSHA
3. The main procedure to conduct PSHA
4. How to conduct the PSHA using OpenQuake program?

## What is Probabilistic Seismic Hazard Analysis (PSHA)?

Probabilistic Seismic Hazard Analysis (PSHA) is the method to quantify the ground motion intensity in terms of Peak Ground Accelartion (PGA), Peak Ground Velocity (PGV), and Peak Ground Displacement (PGD) for a site of interest through probabilistically. The site can be a local scale (a city), regional scale (a province, multiple provinces) or global scale (a country, multiple countries in the same continent).

## Introduction to the main parameters of PSHA

In general, the PSHA aims to answer the question of _how much is the annual frequency of exceedance ($\lambda$) for given a probability of exceedance (PoE) that will exceed for a greater than or equal to ground motion intensity level ($x$) and time window ($t$)_ as written in equation (1) where $IMT$ is intensity measure type (PGA, PGV, or PGD) and $t$ refer to the exposure period (building life expectancy in years). The $\lambda$ is equivalent to the inverse of return period (RP).


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

## The main procedure to conduct PSHA

In the comprehensive analysis, the PSHA is conducted through four steps. 

1. Seismic sources definition (active faults, subduction interfaces, and background sources).

2. Source chracterization

    Each seismic source consider magnitude ranges and depth ranges  (minimum and maximum) with a certain magnitude and depth bins repectively, and also occurrence rates (related to the probability). This process is estimated by using Magnitude-Frequency Distribution (MFD). 

3. Calculating the intensity level
    
    All these components are calculated by using Ground Motion Prediction Equations (GMPEs) and applied the weigth through the logic tree for each GMPEs and seismic source models due to the uncertainty condition. The GMPEs are calculated based on the site location condition in terms of shear wave velocity upt to 30 meters depth (Vs30), magnitude (M), distance (R) from the sources to the site of interest, and others detail parameters. 

4. Calculating the probabilistic

    Finally, it will provide a hazard curve for each site of interest that depicts the relationship between annual frequency of exceedance (or probability of exceedance) and intensity measure level. The probabilistic calculation is calculated by using the following equation,

   $$\lambda [IMT \ge x] = \Sigma_{source_i} v_i \int_{M_0}^{M_{max}} \int_{R|M} P[IMT \ge x | M,R] f_M(m) f_{R|M} (r|m) dr dm$$

    where the

    - $v_i$ is is the annual rate of occurrence of earthquakes on seismic source $i$. In further analysis, the annual rate of occurrence for the subduction can be calculated by using Gutenberg-Richter's relationship $log_{10} v = a - bM$ from the earthquake catalog distribution. The $b$ value is estimated by using linear regression. Meanwhile, for the active shallow crust, this parameter is calculated by using its slip-rate through the geological data approach.

    - $P[IMT \ge x | M,R]$ is the probability of ground motion intensity level greater than and equal to a certain value of $x$ as function of magnitude (M) and distance (R).

        $ P[IMT \ge x | M, R] = 1 - \phi (\frac {\ln x - \overline {\ln IMT}}{\sigma_{\ln PGA}})$

        where the $\overline {\ln IMT}$ is the mean/median of ground motion intensity level from the GMPE and $\sigma_{\ln PGA}$ is its standard deviation

    - $f_M(m)$ is the probability density function of earthquake magnitude

       $$f_M(m) = \frac {b \ln (10) 10^{-b(m - m_{min})}}{1 - 10^{-b(m_{max} - m_{min})}}$$

        for $m_{min} < m < m_{max}$ and $b$ is b-value

    - $f_{R|M} (r|m)$ is the probability density function of distance from the earthquake source to the site of interest. This can be calculated based on the geometry of seismic sources will be modeled (area source, simple fault source, or complex fault source). Further information can be accessed to the [OpenQuake Engine Testing Procedures](https://cloud-storage.globalquakemodel.org/public/wix-new-website/pdf-collections-wix/publications/OQ%20Testing%20Procedures.pdf).

## How to conduct the PSHA using OpenQuake program?

**Requirements**

1. OpenQuake software (seet table below to download). In this tutorial, OpenQuake version of 3.21.0 will be used.

    |Operating Systems|Link|
    |--|--|
    |Installation for Windows | Installation Process - https://docs.openquake.org/oq-engine/master/manual/getting-started/installation-instructions/windows.html|
    ||Download page - https://downloads.openquake.org/pkgs/windows/oq-engine/|
    |Installation for Mac OS | https://docs.openquake.org/oq-engine/master/manual/getting-started/installation-instructions/macos.html|
    |Installation for Ubuntu (Linux) | https://docs.openquake.org/oq-engine/master/manual/getting-started/installation-instructions/index.html|

2. Quantum GIS software (for mapping) - https://qgis.org/resources/installation-guide/ - In this tutorial will be used version of 3.28.3

    After the QGIS has been installed, please install the OpenQuake Integrated Risk Modelling Toolkit (https://plugins.qgis.org/plugins/svir/) through the QGIS's plugin menu.

3. Visual Studio Code (for text editor) - latest version - https://code.visualstudio.com/download

**Mode Calculation**

We will demonstrate the classical calculation of PSHA by using OpenQuake engine. The general and fundamental theory have been explained in above.

**Subtopics**

1. Introduction to the configuration file (job.ini)
2. Setup seismic source model file (nrml-Natural hazards' Risk Markup Language format in xml extention file)
3. Setup logic tree file for seismic source model (xml file)
4. Setup logic tree file for GMPE (xml file)

## References

1. [Thenhaus, P. C., Campbell, K. W., Chen, W. F., & Scawthorn, C. (2003). Seismic hazard analysis. Earthquake engineering handbook, 8, 1-50.](https://www.researchgate.net/profile/Kenneth-Campbell/publication/329682244_Seismic_hazard_analysis/links/5c194fe7a6fdccfc70586a7e/Seismic-hazard-analysis.pdf)

2. [Baker, J., Bradley, B., & Stafford, P. (2021). Seismic hazard and risk analysis.](https://books.google.com/books?hl=en&lr=&id=preiEAAAQBAJ&oi=fnd&pg=PP1&dq=seismic+hazard&ots=aTGZe-WnqZ&sig=pRCcvPnpkbByxIacplfZqeZ8SKU)

3. [Pagani, M., Monelli, D., Weatherill, G. A. and Garcia, J. (2014). Testing procedures adopted in the development of the hazard component of the OpenQuake-engine. Global Earthquake Model (GEM) Technical Report 2014-09, doi: 10.13117/GEM.OPENQUAKE.TR2014.09, 73 pages.](https://cloud-storage.globalquakemodel.org/public/wix-new-website/pdf-collections-wix/publications/OQ%20Testing%20Procedures.pdf)

4. [Pagani, M., Monelli, D., Weatherill, G. A. and Garcia, J. (2014). The OpenQuake-engine Book: Hazard. Global Earthquake Model (GEM) Technical Report 2014-08, doi: 10.13117/-GEM.OPENQUAKE.TR2014.08, 67 pages.](https://cloud-storage.globalquakemodel.org/public/wix-new-website/pdf-collections-wix/publications/OQ%20Hazard%20Science%201.0.pdf)