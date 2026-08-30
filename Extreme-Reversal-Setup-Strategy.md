
> Name

Extreme-Reversal-Setup-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/f38926e6708c10606eee53f45fe1b81c26d929a797f0002d227669ca7ec32653.png)
[trans]
## Overview
The reversal extreme setup strategy is a strategy that takes advantage of extreme K-line reversals. It will judge based on the entity size and average value of the latest K line. When the entity size is greater than the average value and a reversal occurs, a trading signal will be generated.
## Strategy Principle
This strategy mainly determines the physical size of the current K line and the overall K line size.
It will record the physical size of the latest K line (the difference between the opening price and the closing price) and the overall K line size (the difference between the highest price and the lowest price).
Then use the average true range averaging method (RMA) to calculate the average entity size and K line size of the last 20 K lines.
When the latest K line rises and the real body size is greater than the average real body size, and the overall K line size is also greater than 2 times the average K line size, a long signal is generated.
On the contrary, when the latest K line falls and the entity size also meets the above conditions, a short signal is generated.
That is to say, when the extreme K line reverses, the average value is used to judge and generate trading signals.
## Advantage Analysis
The main advantages of this strategy are:
1. Taking advantage of extreme K-line characteristics, it is easy to form a reversal
2. Compare the extreme values of the entity size and the overall K-line size to find outliers
3. Use RMA to calculate dynamic average and adapt to market changes
4. Combined with the reversal pattern, the signal is more reliable
## Risk Analysis
There are also some risks with this strategy:
1. The extreme K line may not reverse and may continue to run
2. Improper parameter settings may lead to over sensitivity or slowness
3. Needs sufficient market fluctuations as support and is not suitable for market consolidation
4. Frequent trading signals may be generated, increasing transaction costs and slippage risks.
In order to reduce risks, you can adjust parameters appropriately or add stop loss to control losses.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Increase the filtering of trading volume to avoid false breakthroughs
2. Use volatility indicators to optimize dynamic settings of parameters
3. Combine with trend indicators to avoid reverse long and short positions
4. Add a machine learning model to determine the probability of K-line reversal
5. Add a stop loss mechanism
## Summarize
The reversal extreme setting strategy generates trading signals when a reversal occurs by judging the extreme situation of the latest K-line. It has the advantage of taking advantage of the abnormal extreme K-line characteristics, but there are also certain risks. Through parameter optimization and risk control methods, better strategic performance can be achieved.
||

## Overview

The extreme reversal setup strategy is a strategy that utilizes extreme K-line reversals. It will judge based on the entity size of the latest K-line and average value, and generate trading signals when the entity size is greater than the average value and a reversal occurs.

## Strategy Principle  

This strategy mainly judges the entity size of the current K-line and the overall size of the K-line.

It will record the entity size (difference between open and close) of the latest K-line and the overall size of the K-line (difference between highest and lowest).

Then use the Average True Range Moving Average (RMA) to calculate the average entity size and K-line size of the last 20 K-lines.

When the latest K-line rises and the entity size is greater than the average entity size, and the overall K-line size is also greater than 2 times the average K-line size, a long signal is generated.

On the contrary, when the latest K-line falls and the entity size also meets the above conditions, a short signal is generated.

That is, trading signals are generated when extreme K-lines reverse, by judging with average values.

## Advantage Analysis

The main advantages of this strategy are:

1. Use extreme K-line characteristics for easy reversal  
2. Compare extreme values of entity size and overall K-line size to find outliers
3. Use RMA to calculate dynamic averages adaptable to market changes
4. Combine with reversal patterns for more reliable signals

## Risk Analysis  

This strategy also has some risks:

1. Extreme K-lines do not necessarily reverse, may continue to run  
2. Improper parameter settings may cause too sensitive or dull
3. Requires sufficient market volatility to support, not suitable for consolidation  
4. May generate frequent trading signals, increasing transaction costs and slippage risks

To reduce risks, parameters can be adjusted appropriately, or stop loss can be added to control losses.

## Optimization Directions

This strategy can be optimized in the following aspects:

1. Add volume filter to avoid false breakouts  
2. Use volatility indicators to dynamically optimize parameter settings
3. Combine trend indicators to avoid reverse long and short  
4. Add machine learning models to judge K-line reversal probability  
5. Add stop loss mechanism

## Summary  

The extreme reversal setup strategy generates trading signals when reversals occur by judging extreme situations of the latest K-line. It has the advantage of using exceptional extreme K-line features, but also has some risks. Better strategy performance can be obtained through parameter optimization and risk control measures.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.75|bodySize|
|v_input_2|20|Lookback Period|
|v_input_3|2|Bar ATR Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-13 00:00:00
end: 2024-02-20 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Extreme Reversal Setup", overlay=true)

bodySize = input(defval=0.75)
barsBack = input(title="Lookback Period", type=input.integer, defval=20, minval=0)
bodyMultiplier = input(title="Bar ATR Multiplier", type=input.float, defval=2.0, minval=0)

myBodySize = abs(close - open)
averageBody = rma(myBodySize, barsBack)
myCandleSize = abs(high - low)
averageCandle = rma(myCandleSize, barsBack)

signal_long = open[1]-close[1] >= bodySize*(high[1]-low[1]) and 
   high[1]-low[1] > averageCandle*bodyMultiplier and 
   open[1]-close[1] > averageBody and close > open
signal_short = close[1]-open[1] >= bodySize*(high[1]-low[1]) and 
   high[1]-low[1] > averageCandle*bodyMultiplier and 
   close[1]-open[1] > averageBody and open > close

plotshape(signal_long, "LONG", shape.triangleup, location.belowbar, size=size.normal)
plotshape(signal_short, "SHORT", shape.triangledown, location.belowbar, size=size.normal)

strategy.entry("LONG", strategy.long, when=signal_long)
strategy.entry("SHORT", strategy.short, when=signal_short)
```

> Detail

https://www.fmz.com/strategy/442365

> Last Modified

2024-02-21 14:08:09
