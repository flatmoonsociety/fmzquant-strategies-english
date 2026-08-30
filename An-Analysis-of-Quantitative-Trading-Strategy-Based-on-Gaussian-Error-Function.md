
> Name

An-Analysis-of-Quantitative-Trading-Strategy-Based-on-Gaussian-Error-Function
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/03d31a687b8f504d8fa704616cbc8d498325e2491c90a69e9226d23ba3e4a6f0.png)

[trans]
## Overview
This strategy is a quantitative trading strategy based on the Gaussian error function to calculate the P-Signal indicator of price changes. It uses the P-Signal indicator to determine price trends and turning points to determine the timing of entry and exit.
## Strategy Principle
The core indicator of this strategy is P-Signal. The calculation formula of P-Signal is as follows:
```
fPSignal(ser, int) => 
    nStDev = stdev(ser, int)
    nSma = sma(ser, int)
    fErf(nStDev > 0 ? nSma/nStDev/sqrt(2) : 1.0)
```

Here ser represents the price sequence, and int represents the parameter nPoints, that is, how many K lines are looked at. The formula consists of three parts:
1. nStDev is the standard deviation of prices;
2. nSma is the simple moving average of price;
3. fErf is the Gaussian error function.
The meaning of the entire formula is to divide the moving average of the price by the standard deviation of the price, then divide it by sqrt(2) for standardization, and then map it to the (-1, 1) interval through the Gaussian error function. That is, if the price fluctuation is greater than the average, P-Signal is close to 1; if the price fluctuation is less than the average, P-Signal is close to -1.
The strategy uses the value of P-Signal and its changing sign to determine entry and exit:
```
strategy.entry("long", strategy.long, 1, when = nPSignal < 0 and ndPSignal > 0)  

strategy.close("long", when = nPSignal > 0 and ndPSignal < 0)
```

Go long when P-Signal is less than 0 and the change is positive; close the position when P-Signal is greater than 0 and the change is negative.
## Strategic Advantages
This strategy has the following advantages:
1. Fit the price distribution using a Gaussian error function. The Gaussian error function can fit the normal distribution well, which is consistent with the distribution characteristics of most financial time series.
2. Automatically adjust parameters using the standard deviation of prices. This enables a wider range of strategy parameters and is more robust to market changes.
3. The P-Signal indicator combines the advantages of trend and reversal trade. It considers both price fluctuation trends and price reversal points, which is helpful for capturing trend trading and reversal trading opportunities.
## Risk Analysis
This strategy also has some risks, mainly reflected in:
1. High-frequency trading risks. This strategy is a typical high-frequency trading strategy, which will generate more transactions and bear higher transaction costs and slippage risks.
2. Poor performance in volatile market conditions. The P-Signal indicator will generate a large number of false signals in markets where prices have no obvious trends and patterns.
3. Parameter optimization is difficult. The relationship between multiple parameters in the formula is complex, making parameter optimization difficult.
In order to reduce these risks, you can consider adding filtering conditions and reducing transaction frequency; optimizing parameter combinations and transaction cost settings; running in on the real market to select appropriate varieties.
## Optimization direction
There is room for further optimization of this strategy. The main directions are:
1. Add filter conditions to avoid false signals. For example, combine other indicators, do AND or OR conditions, and filter out part of the noise.
2. Optimize parameter combination. Adjust the size of nPoints in different varieties and periods to improve strategy stability.
3. Consider dynamic parameters. Let the nPoints parameter be adaptively adjusted according to the degree of market volatility, which may improve the robustness of the strategy.
4. Incorporate machine learning methods. Use AI algorithms to optimize parameters, filter conditions, and timing of multiple varieties.
## Summarize
Overall, the core idea of ​​this strategy is novel, using a Gaussian function to fit the price distribution and automatically adjust the parameter range. However, as a high-frequency trading strategy, further testing and optimization are needed, especially in terms of risk control and parameter adjustment, in order to achieve stable profits in real trading.
||

## Overview

This strategy is a quantitative trading strategy based on P-Signal indicator calculated by Gaussian error function to measure price changes. It uses P-Signal to determine price trend and turning points for entries and exits.  

## Strategy Logic

The core indicator of this strategy is P-Signal. The calculation formula of P-Signal is: 

```
fPSignal(ser, int) =>
    nStDev = stdev(ser, int) 
    nSma = sma(ser, int)
    fErf(nStDev > 0 ? nSma/nStDev/sqrt(2) : 1.0)
```

Here ser represents the price series, int represents the parameter nPoints, which is the number of bars to look back. This formula consists of three parts:

1. nStDev is the standard deviation of price;  
2. nSma is the simple moving average of price;
3. fErf is the Gaussian error function.

The meaning of the whole formula is to take the moving average of price divided by the standard deviation of price, then divided by sqrt(2) for standardization, and finally mapped to (-1, 1) range by the Gaussian error function. That is, if the price fluctuation is greater than the average, P-Signal is close to 1; if the price fluctuation is less than the average, P-Signal is close to -1.

The strategy uses the value of P-Signal and the sign of its change to determine entries and exits:  

``` 
strategy.entry("long", strategy.long, 1, when = nPSignal < 0 and ndPSignal > 0)

strategy.close("long", when = nPSignal > 0 and ndPSignal < 0)  
```

It goes long when P-Signal is less than 0 and change to positive. It closes position when P-Signal is greater than 0 and change to negative.

## Advantages

The advantages of this strategy include:

1. Using Gaussian error function to fit price distribution. Gaussian error function can fit normal distribution very well, which is in line with most financial time series distributions.
2. Automatically adjusting parameters by standard deviation of price. This makes the strategy more robust across different market conditions.  
3. P-Signal combines the advantages of trend following and mean reversion. It considers both price fluctuation trend and reversal points, which helps capturing opportunities in both trend trading and reversal trading.

## Risks

There are also some risks with this strategy:  

1. High frequency trading risk. As a typical high frequency trading strategy, it may generate more trades, thus bearing higher transaction costs and slippage risks.
2. Underperformance in ranging markets. P-Signal may produce many false signals when price has no clear trend or pattern. 
3. Difficult parameter optimization. Complex relationship between multiple parameters makes parameter optimization challenging.

To reduce those risks, some measures can be taken into consideration: adding filters to reduce trade frequency; optimizing parameter combination and transaction costs setting; live testing and choosing suitable products.  

## Enhancement

There is room for further enhancement:

1. Adding filters to avoid false signals, eg. AND/OR with other indicators to filter out some noise.  
2. Optimizing parameter combination. Adjusting the size of nPoints across different products and timeframes to improve stability.
3. Considering dynamic parameters. Adaptively adjusting nPoints according to market volatility may improve robustness.  
4. Incorporating machine learning methods. Using AI algorithms on parameters, filters and cross-product timing optimization.

## Conclusion

In conclusion, the core idea of this strategy is innovative, fitting price distribution with Gaussian function and automatically adjusting parameters. But as a high frequency trading strategy, it requires further testing and optimization on risk control and parameter tuning before stable profitability in live trading, especially as a high frequency trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|(?Parameters of observation.)Number of Bars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-12 00:00:00
end: 2024-01-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// **********************************************************************************************************
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// P-Signal Strategy © Kharevsky
// @version=4
// **********************************************************************************************************
strategy("P-Signal Strategy", precision = 3)
// Parameters and const of P-Signal.
nPoints = input(title = "Number of Bars", type = input.integer, defval = 9, minval = 4, maxval = 100, group = "Parameters of observation.")
int nIntr = nPoints - 1
// Horner's method for the error (Gauss) & P-Signal functions.
fErf(x) =>
    nT = 1.0/(1.0 + 0.5*abs(x))
    nAns = 1.0 - nT*exp(-x*x - 1.26551223 + 
     nT*( 1.00002368 + nT*( 0.37409196 + nT*( 0.09678418 + 
     nT*(-0.18628806 + nT*( 0.27886807 + nT*(-1.13520398 + 
     nT*( 1.48851587 + nT*(-0.82215223 + nT*( 0.17087277 ))))))))))
    x >= 0 ? nAns : -nAns
fPSignal(ser, int) => 
    nStDev = stdev(ser, int)
    nSma = sma(ser, int)
    fErf(nStDev > 0 ? nSma/nStDev/sqrt(2) : 1.0)
// Strat.
float nPSignal = sma(fPSignal(change(ohlc4), nIntr), nIntr)
float ndPSignal = sign(nPSignal[0] - nPSignal[1])
strategy.entry("long", strategy.long, 1, when = nPSignal < 0 and ndPSignal > 0)
strategy.close("long", when = nPSignal > 0 and ndPSignal < 0)
// Plotting. 
hline(+1.0, color = color.new(color.orange,70), linestyle = hline.style_dotted)
hline(-1.0, color = color.new(color.orange,70), linestyle = hline.style_dotted)
plot(nPSignal, color = color.blue, style = plot.style_line)
plot(strategy.position_size, color = color.white, style = plot.style_cross)
// Alerts.
if(strategy.position_size[0] > strategy.position_size[1])
    alert("P-Signal strategy opened the long position: " + syminfo.tickerid + " " + timeframe.period, alert.freq_once_per_bar)
if(strategy.position_size[0] < strategy.position_size[1])
    alert("P-Signal strategy closed the long position: " + syminfo.tickerid + " " + timeframe.period, alert.freq_once_per_bar)
// The end.
```

> Detail

https://www.fmz.com/strategy/439348

> Last Modified

2024-01-19 14:28:03
