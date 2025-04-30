## Repo for the backtest of my Sustainable Finance project

### Methodology: 
Given the composition of our universe - which contains a lot of Chinese listed equities, we faced
limitations with traditional back-testing tools.   
We initially attempted to use IndexOne but only 11 of our 33 tickers were supported (despite using their symbol mapping). We then used Bloomberg; however, due to licensing restrictions most education focused indices weren’t available.  
We ended up using the Yahoo Finance public API along with the yfinance library. This allowed us to
download historical price data for all our 33 tickers, along with their corresponding currencies.  
To prepare the data, we first retrieved each stock’s daily adjusted close prices and merged them into a
single CSV file. Since many of our stocks trade in non-USD currencies, we also pulled daily FX rates and
multiplied each stock’s local currency price by its FX rate to get a final, USD price.   
Portfolio weights were initially drafted in Excel and then imported to align with the tickers available in our dataset.  

We converted daily prices into monthly returns by extracting each month's final price, calculating
the percentage change, and multiplying these returns by the rebalanced weights. The same monthly return
logic was applied to our benchmark.  
Finally, we combined the monthly returns of both the portfolio and the benchmark into a single CSV that we used for our analysis. Using that data, we calculated some performance metrics and plotted some graphs. The Sharpe ratio was calculated by taking our portfolio’s annualised return subtracting a 2 % annual risk-free rate (short-term U.S. Treasury bills), and dividing the result by the annualised volatility.  
To verify our calculations, we cross-checked our annual returns against Bloomberg for the same period and verified they matched to the nearest 0.01.  


#### Getting and preparing the data:
1. Fetching stock historical data (Yfinance) -> combining all the close price for each ticker into one csv  
2. Fetching each ticker's currency(Yfinance)
3. Download our benchmark's historical close price as a csv from MSCI
4. Reindex dates to make sure they are matching -> multiply each close price(from the combined CSV) by the conversion rate  
**Result**: one combined CSV with all close prices in USD

#### Data Analysis: 
1. Load the data -> Define and normalize weights(initially drafted by solver with ESG score as one of the constraints)
2. Compute monthly returns(for both benchmark and portfolio) taking into consideration monthly weights rebalancing(to account for tickers that IPO'd later than the backtest start)
3. Make some initial graphs with Matplotlib to explore data
-> save the two monthly returns dataframes to csv for plotting more graphs outside of Matplotlib

| Folder         | Description                                                                  | Link                 |
|----------------|------------------------------------------------------------------------------|----------------------|
| 📁 Charts       | Charts used in the final report                                              | [Charts](./Charts)     |
| 📁 Analysis     | Monthly rebalancing, return computation, Sharpe ratio, drawdown, etc.        | [analysis](./analysis)   |
| 📁 Data         | Raw and processed data used for visualizations and analysis                  | [data](./data)       |
| 📁 Prep         | Data preparation: downloading, merging, and FX conversion                    | [prep](./prep)       |
| 📊 Excel   | Initial universe screening, ESG score attribution, weight optimizer (Solver), return analysis    | [excel](./Sustainable%20Finance%20Universe%20Research.xlsx) |

