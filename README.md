# Mind the Gap: Interagency Measurement Uncertainty in California Dairy Methane Inventories

**Overview**  
This repository contains a reproducible, open-source Python pipeline designed to audit and quantify the structural uncertainty between California's two primary agricultural methane tracking datasets: the California Air Resources Board (CARB) CADD dataset and the California Department of Food and Agriculture (CDFA) licensed dairy registry.

By moving beyond simple arithmetic point-estimates, this project utilizes Monte Carlo bootstrapping and emissions error propagation to quantify the atmospheric and economic liability of enteric methane emissions from lactating cows at unaccounted dairy facilities in California between 2012 and 2022.

This work builds directly on an original concordance analysis by Dr. Daniel Chandler ([Climate Action California](https://climateactionca.org/)), submitted as an appendix to [CAC's response](https://ww2.arb.ca.gov/form/public-comments/submissions/60256) to CARB's 2026 [Information Solicitation to Inform Implementation of the Dairy and Livestock Provisions of Senate Bill 1383](https://ww2.arb.ca.gov/public-comments/information-solicitation-inform-dairy-and-livestock-sb1383).

**Repository Structure** 

- *data/raw/*: CADD facility and herd-size data (2012–2023), California county boundary shapefile. (CDFA licensed-dairy data, obtained by Dr. Chandler via a 2024 Public Records Act request, is not included here — see Data Access below.)
- *notebooks/*: MindTheGap.ipynb, the full analysis pipeline — data ingestion, statistical modeling, geospatial mapping, and economic analysis.
- *figures/*: Chloropleth map of California counties and lactating cow methane uncertainty data.

**Data Access**

CADD v2.0.0 is publicly downloadable from CARB's website. The CDFA licensed dairy registry data used here was obtained via a Public Records Act request by Dr. Chandler supplied by CDFA by means of a public records request he made in on October 18, 2024 (data received October 2, 2025); it is used here with his permission.

Additional acknowledgments are due to Jonathan Cole of CAC for translating data from the PDFs initially provided by CDFA into CSV form.

**Methodology**

This analysis proceeds in four steps:

- *Directional Filtering* — isolating county-years where CDFA facility counts exceed CADD counts, which identifies genuine regulatory blind spots rather than simple overcounts.
- *Empirical Bootstrapping* — a 10,000-iteration Monte Carlo simulation sampling missing herd sizes directly from known regional distributions, replacing a deterministic point estimate with a full probability distribution.
- *Emissions Error Propagation* — applying published variance in California dairy enteric emissions (Marklein et al. 2021, *Earth System Science Data* 13: 1151-1166, "[Facility-scale inventory of dairy methane emissions in California: implications for mitigation](https://doi.org/10.5194/essd-13-1151-2021)") to the bootstrapped herd data to generate a probabilistic distribution of unaccounted MTCO2e.
- *Economic Translation* — quantifying the unpriced financial exposure of this uncertainty under three carbon pricing scenarios: California's Cap-and-Invest market price, the federal Social Cost of Carbon, and an equity-weighted SCC.

**Setup**

```
pip install -r requirements.txt
```

Update BASE_PATH in the first code cell of MindTheGap.ipynb to point to your local data/raw/ directory, then run all cells in order.

**Tech Stack**  

- *Data Wrangling*: pandas, numpy.   
- *Statistical Modeling*: scipy.stats (Lin's Concordance Correlation Coefficient, Monte Carlo simulations).  
- *Geospatial Analysis*: geopandas.  
- *Visualization*: matplotlib. 

**Author & Conflict of Interest Statement**

Katharine Dickson, Ph.D.  

*Conflict of Interest Statement: The author currently serves as an Agricultural Methane Policy Team Co-Lead at Climate Action California. This repository was developed as an independent computational policy audit.*
