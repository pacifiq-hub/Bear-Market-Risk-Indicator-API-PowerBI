# Bear-Market-Risk-Indicator-PowerBI

It's March 2020, the COVID-19 pandemic strikes the whole world, and we are soon all locked down at home. Good times to find a new hobby, in particular one you can do from your laptop at home! That's how I started developping a strong interest for finance and investment theory. I particularly recomment the writtings of Warren Buffet, Benjamin Graham, Phil Fisher or Peter Lynch that are timeless and so insightful. This project I am covering here though is a reproduction (one may say a copy) of a fascinating indicator, the _Bear Market Risk Indicator_ that [Peter C Oppenheimer](https://www.goldmansachs.com/media-relations/in-the-news/current/oppenheimer-oped-folder/bio-oppenheimer.pdf), Chief Investment Officer at Goldman Sachs, created and detailed in his book [The Long Good Buy](https://www.goodreads.com/en/book/show/49049246). The book is detailed enough that one can find the pieces needed to reconstruct that indicator. As its name indicates, that indicator tracks the risks at one point in time to experience a bear market (i.e., a period of time when stock prices are declining and market sentiment is pessimistic) based on several macro-economical factors such as inflation, private sector financial balance or the yield curve. Power BI is used (actually Power Pivot, which is based on the same technology but that is free with an Excel license) to track this indicator and get data from the different APIs.

## ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) Data needed 

As explained by Peter Oppenheimer in his book, the BMRI ('Bear Market Risk indicator') is calculated out of 6 different metrics:
1. **Unemployment rate**
2. **Inflation rate**
3. **S&P 500 Shiller PE ratio**: this metric was created by [Robert J. Shiller](http://www.econ.yale.edu/~shiller/), professor at the Yale Department of Economics, and provides a sense of the current valuation of the S&P 500. The ratio is a valuation measure that uses real earnings per share (EPS) over a 10-year period to smooth out fluctuations in corporate profits that occur over different periods of a business cycle. Its detractors contend that it is not very useful since it is inherently backward-looking, rather than forward-looking. That leads to our next indicator that balance out this limitation
4. **The inverted yield curve**: which shows that long-term interest rates are less than short-term interest rates. With an inverted yield curve, the yield decreases the farther away the maturity date is. Sometimes referred to as a negative yield curve, the inverted curve has proven in the past to be a reliable indicator of a recession. Because it is based on investors sentiment, this indicator is qualitative rather than quantitative.
5. **ISM PMI Index**: The ISM manufacturing index, also known as the purchasing managers' index (PMI), is a monthly indicator of U.S. economic activity based on a survey of purchasing managers at more than 300 manufacturing firms. It is considered to be a key indicator of the state of the U.S. economy. Formally called the Manufacturing ISM Report on Business, the survey is conducted by the Institute for Supply Management (ISM).

I'd like to pause here before presenting the sixt and last indicator. So far, we've picked standard indicators that are famous proxies to recession risks. Now the last one is my favorite because it's not a common one, it was highlighted by Jan Hatzius, Chief Economist at Goldman Sachs, and the legend says it helped me predict the 2008 subprime recession. 

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


## ![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) BMRI




## ![#1589F0](https://placehold.co/15x15/1589F0/1589F0.png) Conclusions




## ![#1589F0](https://placehold.co/15x15/1589F0/1589F0.png) Future research



for more details on the bibliography, [check the final technical report](https://github.com/pacifiq-hub/Mode-Transportation-Choices-Clustering-Logit/blob/main/technical%20report.pdf).

#  
