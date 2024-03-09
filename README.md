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




## ![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) Discrete Choice Model 




## ![#1589F0](https://placehold.co/15x15/1589F0/1589F0.png) Conclusions




## ![#1589F0](https://placehold.co/15x15/1589F0/1589F0.png) Future research



for more details on the bibliography, [check the final technical report](https://github.com/pacifiq-hub/Mode-Transportation-Choices-Clustering-Logit/blob/main/technical%20report.pdf).

#  
