# Mind the Gap: Interagency Measurement Uncertainty in California Dairy Methane Inventories

**Overview**  
This repository contains a reproducible, open-source Python pipeline designed to audit and quantify the structural uncertainty between California's two primary agricultural methane tracking datasets: the California Air Resources Board (CARB) CADD dataset and the California Department of Food and Agriculture (CDFA) licensed dairy registry.

By moving beyond simple arithmetic point-estimates, this project utilizes Monte Carlo bootstrapping and emissions error propagation to quantify the true atmospheric and economic liability of unaccounted dairy facilities in California.

This work builds directly on an original concordance analysis by Dr. Daniel Chandler (Climate Action California), submitted as an appendix to CAC's response to CARB's 2026 Information Solicitation on SB 1383 dairy and livestock provisions.

**Repository Structure** 

- *data/raw/*: CADD facility and herd-size data (2012–2023), California county boundary shapefile. (CDFA licensed-dairy data, obtained by Dr. Chandler via a 2024 Public Records Act request, is not included here — see Data Access below.)
- *notebooks/*: MindTheGap.ipynb, the full analysis pipeline — data ingestion, statistical modeling, geospatial mapping, and economic analysis.
- *figures/*: Chloropleth map of California counties and lactating cow methane uncertainty data.

**Data Access**

CADD v2.0.0 is publicly downloadable from CARB's website. The CDFA licensed dairy registry data used here was obtained via a Public Records Act request by Dr. Daniel Chandler and is not independently redistributable; readers seeking to reproduce this analysis should submit their own PRA request to CDFA or contact the author. Once you receive the CSV, place it in the **data/raw/** directory with the other data files prior to running the analysis.

**Methodology**

This analysis proceeds in four steps:

- *Directional Filtering* — isolating county-years where CDFA facility counts exceed CADD counts, which identifies genuine regulatory blind spots rather than simple overcounts.
- *Empirical Bootstrapping* — a 10,000-iteration Monte Carlo simulation sampling missing herd sizes directly from known regional distributions, replacing a deterministic point estimate with a full probability distribution.
- *Emissions Error Propagation* — applying published variance in California dairy enteric emissions (Marklein et al., 2021) to the bootstrapped herd data to generate a probabilistic distribution of unaccounted MTCO2e.
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

*Conflict of Interest Statement: The author currently serves as the Agricultural Methane Policy Team Lead at Climate Action California. This repository was developed as an independent computational policy audit.*
