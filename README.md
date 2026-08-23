# Mind the Gap: Interagency Measurement Uncertainty in California Dairy Methane Inventories

**Overview**
This repository contains a reproducible, open-source Python pipeline designed to audit and quantify the structural uncertainty between California's two primary agricultural methane tracking datasets: the California Air Resources Board (CARB) CADD dataset and the California Department of Food and Agriculture (CDFA) licensed dairy registry.

By moving beyond simple arithmetic point-estimates, this project utilizes Monte Carlo bootstrapping and emissions error propagation to quantify the true atmospheric and economic liability of un-accounted dairy facilities in California.

**Note**: Because the bioinformatics pipelines I engineered during my graduate school and postdoctoral tenure are currently maintained on secure university servers pending publication, I built this repository to explicitly demonstrate how my data science stack translates directly from microbial genomics to climate policy auditing.

**Repository Structure**
data/: Contains the baseline CADD and CDFA facility counts (2012-2022).
notebooks/: Contains the primary Jupyter Notebook (dairy_uncertainty_audit.ipynb) detailing the data ingestion, statistical modeling, and economic analysis.
figures/: Generated figures.

**Methodology**
This analysis evaluates climate data integrity through four distinct computational steps:

Directional Filtering: Isolating county-years where CDFA facility counts exceed CADD counts, identifying genuine regulatory blind spots rather than systematic overcounts.
Empirical Bootstrapping: Utilizing a 10,000-iteration Monte Carlo simulation to sample missing herd sizes directly from known regional distributions, replacing deterministic point-estimates with 95% Confidence Intervals.
Emissions Error Propagation: Applying published variance in California dairy enteric and manure emissions to the bootstrapped herd data to generate a probabilistic distribution of unaccounted MTCO2e.
Political Economy & Shadow Pricing: Quantifying the unpriced financial liability of this data gap by applying multiple carbon pricing scenarios, including the California Cap-and-Trade market proxy, the Federal Social Cost of Carbon (SCC), and the Equity-Weighted SCC.

**Tech Stack**
*Data Wrangling*: pandas, numpy.   
*Statistical Modeling*: scipy.stats (Lin's Concordance Correlation Coefficient, Monte Carlo simulations). 
Geospatial Analysis: geopandas. 
Visualization: matplotlib. 

**Author & Conflict of Interest Statement**
Katharine Dickson, Ph.D.  
Conflict of Interest Statement: The author currently serves as the Agricultural Methane Policy Team Lead at Climate Action California. This repository was developed as an independent computational policy audit.
