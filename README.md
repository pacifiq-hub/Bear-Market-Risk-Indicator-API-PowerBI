# Bear-Market-Risk-Indicator-PowerBI

It's March 2020, the COVID-19 pandemic strikes the whole world, and we are soon all locked down at home. Good times to find a new hobby, in particular one you can do from your laptop at home! That's how I started developping a strong interest for finance and investment theory. I particularly recomment the writtings of Warren Buffet, Benjamin Graham, Phil Fisher or Peter Lynch that are timeless and so insightful. This project I am covering here though is a reproduction (one may say a copy) of a fascinating indicator, the _Bear Market Risk Indicator_ that [Peter C Oppenheimer](https://www.goldmansachs.com/media-relations/in-the-news/current/oppenheimer-oped-folder/bio-oppenheimer.pdf), Chief Investment Officer at Goldman Sachs, created and detailed in his book [The Long Good Buy](https://www.goodreads.com/en/book/show/49049246). The book is detailed enough that one can find the pieces needed to reconstruct that indicator. As its name indicates, that indicator tracks the risks at one point in time to experience a bear market (i.e., a period of time when stock prices are declining and market sentiment is pessimistic) based on several macro-economical factors such as inflation, private sector financial balance or the yield curve. Power BI is used (actually Power Pivot, which is based on the same technology but that is free with an Excel license) to track this indicator and get data from the different APIs.

## ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) Data needed 

As explained by Peter Oppenheimer in his book, the BMRI ('Bear Market Risk indicator') is calculated out of 6 different metrics:
1. **Unemployment rate**
2. **Inflation rate**
3. **S&P 500 Shiller PE ratio**: this metric was created by [Robert J. Shiller](http://www.econ.yale.edu/~shiller/), professor at the Yale Department of Economics, and provides a sense of the current valuation of the S&P 500. The ratio is a valuation measure that uses real earnings per share (EPS) over a 10-year period to smooth out fluctuations in corporate profits that occur over different periods of a business cycle. Its detractors contend that it is not very useful since it is inherently backward-looking, rather than forward-looking. That leads to our next indicator that balance out this limitation
4. **The inverted yield curve**: which shows that long-term interest rates are less than short-term interest rates. With an inverted yield curve, the yield decreases the farther away the maturity date is. Sometimes referred to as a negative yield curve, the inverted curve has proven in the past to be a reliable indicator of a recession. Because it is based on investors sentiment, this indicator is qualitative rather than quantitative.
5. **ISM PMI Index**: The ISM manufacturing index, also known as the purchasing managers' index (PMI), is a monthly indicator of U.S. economic activity based on a survey of purchasing managers at more than 300 manufacturing firms. It is considered to be a key indicator of the state of the U.S. economy. Formally called the Manufacturing ISM Report on Business, the survey is conducted by the Institute for Supply Management (ISM).

I'd like to pause here before presenting the sixth and last indicator. So far, we've picked standard indicators that are famous proxies to recession risks. Now the last one is my favorite because it's not a common one, it was highlighted by Jan Hatzius, Chief Economist at Goldman Sachs, and the legend says it helped him predict the 2008 subprime recession. 

6. **Private sector balance sheet**: this indicator tracks the amount of savings of the private sector, which includes private households as well as businesses together. A surplus balance means U.S. households and businesses together are net savers, building their financial asset position. In other words, savings by households exceed the amount borrowed and invested by businesses. There is a net inflow of money into the private sector. This indicator is the hardest to calculate and track but the most important in my view for the BMRI. 

## ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) APIs! 

| Metric  | API Provider | Updates | Other instructions |
| ------------- | ------------- | ------------- | ------------- |
| Unemployment rate | US. bureau of labor statistics: https://www.bls.gov/  | https://www.bls.gov/schedule/2020/08_sched.htm | **Series of interest**: LNS14000000 <br> **Series title:**(Seas) Unemployment Rate <br> **Labor force status**: Unemployment rate <br> **To find this serie**: go to https://www.bls.gov/cps/data.htm > Top picks > "" Unemployment Level - LNS14000000"" <br> **Comments**: no need to add registration key, calculations or Annual average"
| Inflation rate | US. bureau of labor statistics: https://www.bls.gov/  | https://www.bls.gov/schedule/2020/08_sched.htm |**Series of interest**: CUUR0000AA0 <br> **Series title**: CPI for All Urban Consumers (CPI-U) <br> **To find this serie**: go to https://www.bls.gov/cps/data.htm > Top picks > "CPI for All Urban Consumers (CPI-U) 1967=100 (Unadjusted) - CUUR0000AA0" <br> **Comments**: no need to add registration key, calculations or Annual average
| S&P 500 Shiller PE Ratio  | Quandl (was free until march 2023), Trading Economics or Guru Focus provide it with a subscription fee | Monthly, ~beg. Of the month | **URL**: https://www.quandl.com/data/MULTPL/SHILLER_PE_RATIO_MONTH-Shiller-PE-Ratio-by-Month  <br>  **From the data product**: S&P 500 Ratios <br> **Series title**: Shiller PE Ratio by Month
| ISM PMI Index  | Quandl (was free until march 2023), Trading Economics or MacroVar provide it with a subscription fee | Monthly, ~beg. Of the month | **URL**:  https://www.quandl.com/data/ISM/MAN_PMI-PMI-Composite-Index <br>  **From the data product**: Institute for Supply Management <br> **Series title**: PMI Composite Index
| US Tresury yields  | Bureau of Economic Affairs: https://www.bea.gov/open-data | https://www.bea.gov/news/schedule | **URL**: https://www.quandl.com/data/USTREASURY/YIELD-Treasury-Yield-Curve-Rates <br> **From the data product**: US Treasury <br> **Series title**: Treasury Yield Curve Rates
| Real GDP | Bureau of Economic Affairs <br> **BEA**: https://apps.bea.gov/ <br> **API documentation PDF**: https://apps.bea.gov/api  | Quaterly, ~last day of next quarter's 1st month | **Check NIPA tables**: https://apps.bea.gov/api/data/?&UserID=C36A268E-C628-4F21-9624-C69BD55C081B&method=GetParameterValues&DataSetName=NIPA&ParameterName=TableName&ResultFormat=xml <br> **Table used**: T10106 <br> **Name of table used**: Real Gross Domestic Product, Chained Dollars
| Saving & Investment | Bureau of Economic Affairs <br> **BEA**: https://apps.bea.gov/ <br> **API documentation PDF**: https://apps.bea.gov/api  | Quaterly, ~last day of next quarter's 1st month | **Check NIPA tables**: https://apps.bea.gov/api/data/?&UserID=C36A268E-C628-4F21-9624-C69BD55C081B&method=GetParameterValues&DataSetName=NIPA&ParameterName=TableName&ResultFormat=xml <br> **Table used**: T50100 <br> **Name of table used**: Saving & investment by sector
| 6Q Forward interest rate | **Federal Reserve**: https://www.federalreserve.gov/  <br> **Nominal Yield Curve Detail Page**: https://www.federalreserve.gov/data/nominal-yield-curve.htm | https://www.federalreserve.gov/data/yield-curve-tables/feds200628_1.html | **Where to find the data**: https://www.federalreserve.gov/data/nominal-yield-curve.htm <br> **Name of the table**: Nominal Yield Curve <br> The forward 6 Quarter instantaneous rate is calculated with the GSM Rates as detailed by the paper published by the FED: https://www.federalreserve.gov/econres/feds/files/2018055pap.pdf TableName&ResultFormat=xml <br> **Table used**: T50100 <br> **Name of table used**: Saving & investment by sector

**Note to the reader after 2023:** It was still possible back in 2020 to find all data for free. Now that NASDAQ and S&P bought many of the smaller data providers, I find it harder to get the data for free. It is still possible to scrap some web pages to get partial historical information, but that won't get the full historical overview of these indicators. Bigger institutions such as the BEA, FED or BLS belonging to the government will continue to provide this data for free, their API are very easy to use and well documented. 

## ![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) BMRI

Once all data is pulled from these different APIs, we create the resulting tables that store the information needed. The data model leading to the calculation of the BRMI is the following:

![image](https://github.com/pacifiq-hub/Bear-Market-Risk-Indicator-API-PowerBI/assets/46910395/48558cb4-d76c-4960-96bb-2a23bbaf689a)

**BMRI calculation**: The last step of our project is to calculate the BMRI. Our data going back to 1961 for the six indicators, we simply calculate the percentile for each indicator all the way back to 1961. We then average out the 6 percentile values to get the BMRI percentile value. 

This how it looks in the backend: 

![image](https://github.com/pacifiq-hub/Bear-Market-Risk-Indicator-API-PowerBI/assets/46910395/7bb163e7-c979-4f4b-9b45-fe452c4f0a87)

**And the final graph:**

![image](https://github.com/pacifiq-hub/Bear-Market-Risk-Indicator-API-PowerBI/assets/46910395/1f3117d5-c837-48e6-a377-d92fbf5f4e8e)

**How to read this graph:**
- The higher the percentile value of the BMRI, the higher the chances of a recession
- Peter Oppenheimer offered threshold values that separate our graph into 3 areas: Green is safe and healthy to invest, Grey is neutral and Red is risky with a market that comes to saturation.
- you will notice that the last 4 values of the graph are dotted, and separated from the rest of the graph. This is because the the BEA only provide data on the 6th indicator 2 quarters late, vs. all other indicators are provided on a monthly basis. I decided to still capture a percentile value based on the first 5 indicators, and called it a forecast while waiting for the actual value of the BMRI 

## ![#1589F0](https://placehold.co/15x15/1589F0/1589F0.png) Conclusions

![BMRI through history](https://github.com/pacifiq-hub/Bear-Market-Risk-Indicator-API-PowerBI/assets/46910395/f4eb8d46-38b3-4544-b28e-bdc560fb1049)

I consider this tool to be a fantastic addition to the investor toolkit, providing a higher level of confidence investing when all macro-economical factors are "green". It tremendously helped guide my investment strategy in the aftermath of the pandemic crisis. 

I made the Power Pivot file available for anyone to download from this repository and use, and welcome any suggestions to improve it. You will only need an Microsoft Excel license and the power pivot add-in enabled to refresh the data, and play with the filters. 

**Note to the reader after 2023:** ISM PMI as well as Shiller S&P 500 ratio APIs are not free anymore, and a subcription will be needed to get these. APIs in the power pivot file should be modified to redirect to the new provider. 


## ![#1589F0](https://placehold.co/15x15/1589F0/1589F0.png) Future research

The private sector financial balance indicator value lags the other indicators due to the time it takes the BEA to consolidate and publish their GDP reports. I read in some documents that Goldman Sachs uses proxies that approximate the value of this indicator until the actual value is published. It makes their forecast more accurate than mine that removes it entirely until publication. Finding an efficient proxy would be a great addition to this project! 



for more details on the bibliography, [check the final technical report](https://github.com/pacifiq-hub/Mode-Transportation-Choices-Clustering-Logit/blob/main/technical%20report.pdf).

#  
