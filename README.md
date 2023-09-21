# BZCAT Clustering

## 1. About the project

This is a repository for the cluster analysis of the blazars from the Roma-BZCAT catalog (Massaro et al., 2015, Ap&SS, 357, 75). The aim is to divide the objects into groups with more or less similar properties to further analyze the differences between them and possibly obtain some insighths into the nature of this type of active galactic nuclei (AGNs). 

The feature space for the clustering has been choosen with a simple general approach: all possible features related to the physics of the objects. We'll discuss the selection of characteristics for the model dataset in the paper currently prepared. 

It is worth noting that blazars is quite a homogenious class of AGNs, which has been some kind of a challenge for the project. The other problem is a deficiency of data: out of the 3561 blazars from the catalog, only about 800 objects had all the model dataset characteristics measured. To fill the missing data, the probabilistic PCA (pPCA) approach have been used. We analyze both the "short" version of the catalog and the total result with the pPCA-imputed values, comparing the results (about 90% consistency). 

The general clustering workflow is as follows:
* probabilistic PCA to guess the missing values;
* PCA dimensionality reduction 
* k-means clustering

Some other algorithms have also been tested to look for the best metrics, but they are not included in the final noteooks for clarity.

The project has been reported at the conference ["Modern instruments and methods in astronomy"](https://crimea-2023.crao.ru/), the proceedings is going to be published in Acta Astrophysica Taurica. We have been also preparing a paper with more detailed description of the dataset, clustering, and results.

## 2. The data

The dataset has been combined from the following sources:
* original [Roma-BZCAT catalog](https://heasarc.gsfc.nasa.gov/W3Browse/all/romabzcat.html)
* [BLcat catalog](https://www.sao.ru/blcat/) 
* [CATS database](https://www.sao.ru/cats/)
* [Sloan Digital Sky Survey](http://skyserver.sdss.org/dr18/)
* [Pan-STARRS data](https://outerspace.stsci.edu/display/PANSTARRS/)
* [GALEX mission](http://www.galex.caltech.edu/about/overview.html) from the [Mikulsky Archive for Space Telescopes](https://archive.stsci.edu/) via the [Astroquery](https://astroquery.readthedocs.io/) library
* [WISE](https://www.nasa.gov/mission_pages/WISE/mission/index.html) and [2MASS](https://irsa.ipac.caltech.edu/Missions/2mass.html) missions from the [NASA/IPAC Infrared Science Archive](https://irsa.ipac.caltech.edu/frontpage/)
* Data on interstellar extinctions from the [NED database](https://ned.ipac.caltech.edu/extinction_calculator)
* Spectral energy distributions (SEDs) from [SED Builder](https://tools.ssdc.asi.it/SED/)

We currently don't provide the data in this repository, the final dataset is now being prepared for publication.


## 3. Project stages and files

* The [./scrapers/](./scrapers/) folder contains the scripts used to get the data from the PanSTARRS, WISE, GALEX, NED, and SDSS catalogs. A script for the Selenium web driver has been also developed to mine the data on spectral energy distributions, "hiding behind the buttons" on the SED Builder web page. Thanks to Selenium, we can now winkle it out. :)

* [./data_comb.ipynb](./data_comb.ipynb) A notebook that combines the data. 

* [./feature_engeneering.ipynb](./feature_engeneering.ipynb) A general preprocessing with some transformations made and new features created. Most of them are of astronomical kind, and some are further used in the clustering feature space while the others are only for the sake of possible further analysis.

* [./main_model.ipynb](./main_model.ipynb) This is the core of the project with the clustering, metrics, and preliminary analysis. We have cleaned it as much as we can from the leftovers of the working process, trying to leave only the essence of the result.

* [sweetviz_report.ipynb](./sweetviz_report.ipynb) makes a [Sweetviz](https://pypi.org/project/sweetviz/) HTML report used for faster data reviewing and cleansing.
