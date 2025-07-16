# Modelling House Prices

## Overview

This project analyses property prices in Oxfordshire and Cambridgeshire, assuming their market dynamics are broadly comparable, to understand key factors influencing market values. Starting with data scraping from online property listings, the process covers cleaning, feature engineering, and statistical modelling to build an interpretable predictive model.
## Data Sourcing

Property listing data was scraped from **savills.co.uk** using **Google Puppeteer**.  Savills was chosen because it was the only site I could find whose Terms of Service (ToS) did not prohibit scraping, ensuring the data collection process was compliant and ethical. However, due to ToS restrictions, the raw dataset itself cannot be shared.

## Project Steps

1. **Data Collection**  
   Scraped property listings with details including price, size, bedrooms, bathrooms, receptions, council tax band, EPC rating, and tenure.

![Segment of Puppeteer script](/images/scraper.png)
*Screenshot: A portion of the Puppeteer script used to extract EPC rating, tenure, and council tax band from listings.

2. **Data Cleaning & Preparation**  (in Google Colab)
   - Removed incomplete records and placeholder entries.  
   - Standardised **area measurements**.  
   - Converted **tenure** into a boolean (`1 = Freehold`, `0 = Other`), as most properties were freehold (181/191).  
   - Converted **property type** into a boolean (`1 = House`, `0 = Other`), as most were houses (177/191).  
   - Encoded **EPC rating** and **council tax band** as **ordered numeric values** to preserve their natural hierarchy and reduce dimensionality.

3. **Modelling**  
   - Built a **log-linear regression model** and performed **stepwise selection** to identify significant predictors and interactions.  
   - Considered interaction terms such as bathrooms × receptions and bedrooms × bathrooms to capture combined effects.  
   - Selected the final model using AIC minimization.

4. **Diagnostics & Validation**  
   - Checked assumptions with **Breusch–Pagan test** (heteroscedasticity), **VIF** (multicollinearity), and residual diagnostic plots.  
   - Evaluated the final model on a hold‑out test set using:  
      - **RMSE** (Root Mean Squared Error),  
      - **MAPE** (Mean Absolute Percentage Error),  
      - **R²** (coefficient of determination).

## Key Findings

- **Bedrooms**  
  *Significant positive main effect.*  
  More bedrooms are strongly associated with higher property prices, even after controlling for other factors.

- **Council Tax Band (`tax_numeric`)**  
  *Highly significant positive effect.*  
  Properties in higher council tax bands tend to have higher prices, reflecting their greater value and location desirability.

- **Receptions**  
  *No significant main effect*, but:  
  - *Negative interaction with bedrooms:* the combined effect of having both more bedrooms and more receptions is smaller than the sum of their individual effects.  
  - *Positive interaction with area size:* reception rooms add more value in larger properties.

- **Bathrooms**  
  *No significant main effect*, but:  
  - *Positive interaction with receptions:* additional bathrooms are more valuable in properties with more reception rooms.

- **Area (`areaValue`)**  
*No significant main effect*, but:  
  - *Positive interaction with receptions:* larger properties with more reception rooms achieve higher prices.

- **EPC Rating (`epc_numeric`)**  
  Not statistically significant in this model.

## Conclusion
This analysis shows that property valuations are driven by multiple features and their interactions, rather than single factors in isolation. Future improvements could explore non-linear models and integrate location-specific variables to achieve even greater predictive accuracy.

---

_Project developed using R and includes steps from data scraping to advanced regression modelling._
