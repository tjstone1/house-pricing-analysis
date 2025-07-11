# house-pricing-analysis

## Overview

This project analyses property price data to understand key factors influencing market values. Starting with data scraping from online property listings, the process covers cleaning, feature engineering, and statistical modelling to build an interpretable predictive model.

## Data Sourcing

Data was sourced from savills.co.uk, a reputable UK property listing website. Data collection was conducted in accordance with their terms of service and therefore the dataset will not be publicly shared.

## Project Steps

1. **Data Collection**  
   Property data was scraped from public listings, gathering features such as price, area size, number of bedrooms, bathrooms, receptions, council tax bands, and energy performance ratings. The data was collected using Google Puppeteer.

![Segment of Puppeteer script](/images/scraper.png)

2. **Data Cleaning & Preparation**  
   The raw data was cleaned by handling missing values, recoding categorical variables (e.g., energy ratings), and converting key variables to numeric formats suitable for analysis.

3. **Modelling**  
   Stepwise regression was employed using log-transformed prices to stabilise variance. Interaction terms were included to capture combined effects of features like bathrooms, bedrooms, and receptions. Model selection was based on minimising AIC.

4. **Diagnostics & Validation**  
   Residual analysis and tests for heteroscedasticity (Breusch-Pagan test) were conducted.

5. **Prediction**  
   The final model was used to predict property prices on new data, showing reasonable accuracy. This was not included in the final report as the sample size was too small to make any insights.

## Key Findings

- Property size, bathroom count, and council tax band are significant predictors of price.
- Interactions between bedrooms, bathrooms, and reception rooms meaningfully influence valuation.
- Energy performance shows limited direct impact in the model.
- The model explains approximately 72% of the variation in log-prices.

## Conclusion

This analysis highlights the complexity of property valuation, where multiple features and their interactions shape market prices. Future work could extend to non-linear models and incorporate location-specific effects for enhanced precision.

---

_Project developed using R and includes steps from data scraping to advanced regression modelling._
