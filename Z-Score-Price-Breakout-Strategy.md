
> Name

Z-Score-Price-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/d386cdae9d1531e353d59bc3190689b76e9d0c7d5148845027b460a73bffb970.png)

[trans]

### Overview
The Z-Score Price Breakout Strategy uses the standard score indicator of price to determine whether the current price is in an abnormal state, thereby generating trading signals. When the standard score of the price is higher or lower than a certain threshold, it indicates that the price has entered an abnormal state, and you can perform long or short operations at this time.
### Strategy Principles
The core indicator of this strategy is the standard score (Z-Score) of the price, and the calculation formula is as follows:
```
Z_score = (C - SMA(n)) / StdDev(C,n)
```

Among them, C is the closing price, SMA(n) is the simple moving average of n periods, and StdDev(C,n) is the standard deviation of the closing price of n periods.
The standard score reflects how much the current price deviates from the average price. When the price standard score is greater than a certain positive threshold (such as +2), it means that the current price is already 2 standard deviations higher than the average price, which is a relatively high level; when it is less than a certain negative threshold (such as -2), it means that the current price is already 2 standard deviations lower than the average price, which is a relatively low level.
This strategy first calculates the standard score of the price, and then sets a positive and negative threshold (such as 0 and 0). When the standard score is higher than the positive threshold, a buy signal is generated, and when the standard score is lower than the negative threshold, a sell signal is generated.
### Advantage Analysis
- Using price standard scores to determine price anomalies is a common and effective quantitative method.
- Long and short two-way transactions can be easily realized
- Flexible parameter settings, adjustable periods, thresholds, etc.
- Can be combined with other indicators to form a trading system
### Risk Analysis
- The standard score strategy is relatively extensive and prone to false signals.
- Appropriate parameters need to be set, such as period and threshold
- Stop loss strategies need to be considered to control risks
### Optimization direction
- Optimize cycle parameters and find the best cycle
- Optimize the positive and negative thresholds to reduce false signals
- Add filter conditions and combine with other indicators
- Add stop loss strategy
### Summarize
The standard score price breakout strategy determines whether the current price is in an abnormal state and trades based on the positive or negative price standard score. This strategy is simple and easy to implement and can be traded in both directions, but it also involves certain risks. Through parameter optimization and stop loss, this strategy can be strengthened and combined with other indicators to form a complete quantitative trading system.
||


### Overview  

The Z-Score price breakout strategy uses the z-score indicator of price to determine whether the current price is in an abnormal state, so as to generate trading signals. When the z-score of price is higher or lower than a threshold, it means the price has entered an abnormal state, at which point long or short positions can be taken.

### Strategy Principle  

The core indicator of this strategy is the z-score of price, calculated as follows: 

```
Z_score = (C - SMA(n)) / StdDev(C,n)
```

Where C is the closing price, SMA(n) is the simple moving average of n periods, and StdDev(C,n) is the standard deviation of closing price for n periods.  

The z-score reflects the degree of deviation of the current price from the average price. When the price z-score is greater than a certain positive threshold (e.g. +2), it means the current price is above the average price by 2 standard deviations, which is a relatively high level. When it is less than a certain negative threshold (e.g. -2), it means the current price is below the average price by 2 standard deviations, which is a relatively low level.

This strategy first calculates the z-score of price, then sets a positive and negative threshold (e.g. 0 and 0). When the z-score is higher than the positive threshold, it generates a buy signal. When lower than the negative threshold, it generates a sell signal.  

### Advantage Analysis   

- Using price z-score to judge price anomalies is a common and effective quantitative method  
- Easily achieve both long and short trading  
- Flexible parameter settings, adjustable cycle, threshold, etc.   
- Can be combined with other indicators to form a trading system  

### Risk Analysis

- The z-score strategy is crude and prone to false signals  
- Need to set appropriate parameters like cycle and threshold
- Need to consider stop loss strategies to control risk  

### Optimization Directions   

- Optimize cycle parameters to find the best cycle  
- Optimize positive and negative thresholds to reduce false signals 
- Add filter conditions, combine with other indicators  
- Add stop loss strategies  

### Summary   

The z-score price breakout strategy judges whether the current price is in an abnormal state, and trades according to the positive and negative of the price z-score. This strategy is simple and easy to implement, allows two-way trading, but also has some risks. By optimizing parameters, adding stop loss and combining with other indicators, this strategy can be enhanced to form a complete quantitative trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Period|
|v_input_2|false|Trigger|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-29 00:00:00
end: 2023-12-04 19:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 18/01/2017
// The author of this indicator is Veronique Valcu. The z-score (z) for a data 
// item x measures the distance (in standard deviations StdDev) and direction 
// of the item from its mean (U):
//     z = (x-StdDev) / U
// A value of zero indicates that the data item x is equal to the mean U, while 
// positive or negative values show that the data item is above (x>U) or below 
// (x Values of +2 and -2 show that the data item is two standard deviations 
// above or below the chosen mean, respectively, and over 95.5% of all data 
// items are contained within these two horizontal references (see Figure 1).
// We substitute x with the closing price C, the mean U with simple moving 
// average (SMA) of n periods (n), and StdDev with the standard deviation of 
// closing prices for n periods, the above formula becomes:
//     Z_score = (C - SMA(n)) / StdDev(C,n)
// The z-score indicator is not new, but its use can be seen as a supplement to 
// Bollinger bands. It offers a simple way to assess the position of the price 
// vis-a-vis its resistance and support levels expressed by the Bollinger Bands. 
// In addition, crossings of z-score averages may signal the start or the end of 
// a tradable trend. Traders may take a step further and look for stronger signals 
// by identifying common crossing points of z-score, its average, and average of average. 
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="Z-Score Strategy", shorttitle="Z-Score Strategy")
Period = input(20, minval=1)
Trigger = input(0)
reverse = input(false, title="Trade reverse")
hline(Trigger, color=purple, linestyle=line)
xStdDev = stdev(close, Period)
xMA = sma(close, Period)
nRes = (close - xMA) / xStdDev
pos = iff(nRes > Trigger, 1,
	   iff(nRes < Trigger, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(nRes, color=blue, title="Z-Score")
```

> Detail

https://www.fmz.com/strategy/434552

> Last Modified

2023-12-07 15:17:43
