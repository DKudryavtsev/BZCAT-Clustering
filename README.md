# BZCAT Clustering

## 1. About the project

This is a repository for the cluster analysis of the blazars from the BZCAT catalog (Massaro et al., 2015, Ap&SS, 357, 75). The aim is to divide the objects into groups with more or less similar properties to further analyze the differences between them and possibly obtain some insighths into the nature of this type of active galactic nuclei (AGNs). 

The feature space for the clustering has been choosen with a simple approach: "all" available independent features. As well, the dependent ones are used if they are of the same nature, in this case the first PCA component of them is the feature. 

It is worth noting that blazars is quite a homogenious class of AGNs, which has been some kind of a challenge for the project. The other problem is a deficiency of data: out of the 3561 blazars from the catalog, only 800 objects had all the "clustering features" measured. To fill the missing data the probabilistic PCA approach have been used. I analyze both the "short" version of the catalog and the total result with the PPCA-imputed values, comparing the results. 

The general clustering workflow therefore is as follows:
* probabilistic PCA to guess the missing values;
* classical PCA to reduce dependent values into one primary component
* general dimensionality reduction using PCA or t-SNE (the results of both are compared)
* clustering: k-means or Gaussian mixture 

Actually, I use 'PCA + k-means' as a first approach and then refine this result with the 't-SNE + Gaussian mix' so that t-SNE parameters are choosen having in mind the "baseline" model.

Some other algorithms have also been tested to look for the best metrics, but they are not included in the final noteooks for clarity.

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

The raw data are not provided here. The processed datasets are:
* [BZCAT_combined.csv](./data/BZCAT_combined.csv): the dataset after the raw data combination;
* [BZCAT_all_features.csv](./data/BZCAT_all_features.csv): the dataset after feature preparation;
* [BZCAT_clusters.csv](./data/BZCAT_clusters.csv): final dataset with cluster labels;
* [seds_residents.csv](./data/seds_residents.csv): SEDs from the SED Builder resident catalogs (the file is needed to run feature_engeneering.ipynb)

Some data have not been used in the clustering itself because of their scarcity, but they can be used in further analysis.


## 3. Project stages and files

* The [./scrapers/](./scrapers/) folder contains the scripts used to get the data from the PanSTARRS, WISE, GALEX, NED, and SDSS catalogs. A script for the Selenium web driver has been also developed to mine the data on spectral energy distributions, "hiding behind the buttons" on the SED Builder web page. Thanks to Selenium, I can now winkle it out. :)

* [./data_comb.ipynb](./data_comb.ipynb) A notebook that combines the data. I do not provide the raw data on GitHub, so this is only for demonstration.

* [./feature_engeneering.ipynb](./feature_engeneering.ipynb) A general preprocessing with some transformations made and new features created. Most of them are of astronomical kind, and some are further used in the clustering feature space while the others are only for possible further analysis purposes. Some "pure clustering" features are also created (the "hardnesses" at the end).

* [./main_model.ipynb](./main_model.ipynb) This is the core of the project with the ML algorithms working, metrics, and preliminary analysis. I have cleaned it as much as I can from the leftovers of the working process, trying to leave only the essence of the result.

* [sweetviz_report.ipynb](./sweetviz_report.ipynb) makes a [Sweetviz](https://pypi.org/project/sweetviz/) HTML report used for faster data reviewing and cleansing. 

## 5. Running the project

To run the project by yourself, you will need the [Jupiter Notebook](https://jupyter.org/) installed along with Python and some of its libraries (see [requirements.txt](./requirements.txt)). The notebooks should be runned in the following order:
1. feature_engeneering.ipynb
2. main_model.ipynb

## 4. The results

A further analysis is currently being made and a paper is being prepared where we are going to present the results and conclusions.
