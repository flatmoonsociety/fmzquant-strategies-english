
> Name

Average-Line-Breakthrough-Strategy Based on Average-Line-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/124c76bc31ac5562b35.png)
[trans]
## Overview
The moving average reversion breakthrough strategy is a typical quantitative trading strategy that follows trends. This strategy uses moving averages and their standard deviation channels to determine market trends and generate trading signals when price breaks out of the standard deviation channels.
## Strategy Principle
This strategy first calculates the simple moving average SMA of N days (default 50 days), and then calculates the standard deviation StdDev of the price in that period based on the SMA. Use SMA as the central axis, and use 2 times StdDev as the upper and lower rails to construct a "standard deviation channel". When the price goes above the upper band, go short; when the price goes below the lower band, go long.
After entering the market, the strategy will set stop loss and take profit levels. Specifically, after going long, the stop-loss line is (100 - stop loss percentage) of the closing price when entering the market; after going short, the take-profit line is (100 + take-profit percentage) of the closing price when entering the market.
## Advantage Analysis
This strategy has the following advantages:
1. Strong ability to track trends. Use the standard deviation channel to dynamically track market fluctuations.
2. Strong retracement control ability. Using trailing stop loss can effectively control single losses.
3. Simple to implement. It saves a lot of parameter optimization and is very easy to implement.
## Risk Analysis
There are also some risks with this strategy:
1. Trend reversal risk. Trend-following strategies are prone to exiting at a loss and then reversing.
2. Parameter sensitivity risk. The parameter selection of the moving average period and standard deviation multiple will have a great impact on the performance of the strategy.
3. Stop loss that is too aggressive may cause additional losses. Improperly set stop loss points may result in additional losses.
The solutions corresponding to the risks are as follows:
1. Combine with volatility indicators to avoid false breakthroughs.
2. Optimize the parameters to find the optimal parameter combination. 
3. Adjust the stop loss mechanism to prevent being too aggressive.
## Optimization direction
There is room for further optimization of this strategy:
1. Use moving averages of multiple time periods for verification to avoid the curve being too sensitive.
2. Combine with other indicators such as MACD to determine trends and divergences.
3. Introduce machine learning algorithm to dynamically optimize parameters.
## Summarize
The moving average regression breakthrough strategy is overall a very practical quantitative trading strategy. It has the advantages of tracking trends and controlling retracement, is simple to implement, and is suitable for the needs of quantitative trading. At the same time, we also need to pay attention to some parameter selection and stop loss setting issues. With multi-timeline analysis and parameter optimization, we can obtain better strategy performance.
||

## Overview  

The average line breakthrough strategy is a typical quantitative trading strategy that tracks trends. This strategy uses moving averages and their standard deviation bands to judge market trends and generate trading signals when prices break through the standard deviation bands.  

## Strategy Principle

The strategy first calculates the N-day (default 50-day) simple moving average SMA, and then calculates the standard deviation StdDev of the price based on the SMA for this cycle. With the SMA as the center axis and the upper and lower rails as 2 times the StdDev, the "standard deviation channel" is constructed. When the price goes above the upper rail, go short; when the price falls below the lower rail, go long.

After entering the market, the strategy will set stop loss and take profit points. Specifically, after going long, the stop loss line is the closing price at the time of entry (100 - stop loss percentage); after going short, the take profit line is the closing price at the time of entry (100 + take profit percentage).

## Advantage Analysis 

The strategy has the following advantages:

1. Strong trend tracking capability. Using standard deviation channels can dynamically track market fluctuations.

2. Strong drawdown control capability. Using mobile stop losses can effectively control single losses.

3. Simple implementation. Saves a lot of parameter optimization and is very easy to implement.

## Risk Analysis

The strategy also has some risks:

1. Trend reversal risk. Trend tracking strategies are prone to losses and then reversals.

2. Parameter sensitivity risk. The choice of parameters such as moving average period and standard deviation multiplier will have a greater impact on strategy performance.

3. Stop loss is too aggressive to cause additional losses. Improper stop loss point settings can cause additional losses.

The solutions to the corresponding risks are as follows:

1. Combine volatility indicators to avoid false breakouts.

2. Optimize parameters to find the optimal parameter combination.

3. Adjust the stop loss mechanism to prevent excessive aggression.

## Optimization Directions

There is still room for further optimization of the strategy:

1. Use multiple time frame moving averages for verification to avoid overly sensitive curves.

2. Incorporate other indicators such as MACD to judge trends and divergence.  

3. Introduce machine learning algorithms to dynamically optimize parameters.

## Summary  

Overall, the moving average regression breakthrough strategy is a very practical quantitative trading strategy. It has the advantages of tracking trends and controlling drawdowns, simple implementation, and meets the needs of quantitative trading. At the same time, attention should also be paid to issues such as parameter selection and stop loss settings. With multi-time axis analysis and parameter optimization, better strategy performance can be obtained.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|2|Standard Deviation Multiplier|
|v_input_int_1|50|Moving Average Length|
|v_input_float_2|12|Stop Loss Percentage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-16 00:00:00
end: 2024-02-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Standard Deviation Bands with Buy/Sell Signals", overlay=true)

// Input for the number of standard deviations
deviationMultiplier = input.float(2.0, title="Standard Deviation Multiplier")

// Input for the length of the moving average
maLength = input.int(50, title="Moving Average Length")

// Input for the stop loss percentage
stopLossPercentage = input.float(12, title="Stop Loss Percentage")

// Calculate the moving average
sma = ta.sma(close, maLength)

// Calculate the standard deviation of the price
priceDeviation = ta.stdev(close, maLength)

// Calculate the upper and lower bands
upperBand = sma + (priceDeviation * deviationMultiplier)
lowerBand = sma - (priceDeviation * deviationMultiplier)

// Plot the bands
plot(upperBand, color=color.green, title="Upper Band")
plot(lowerBand, color=color.red, title="Lower Band")

// Plot the moving average
plot(sma, color=color.blue, title="SMA", linewidth=2)

// Buy Signal
buyCondition = ta.crossover(close, lowerBand)
sellCondition = ta.crossunder(close, upperBand)

// Calculate stop loss level
stopLossLevelBuy = close * (1 - stopLossPercentage / 100)
stopLossLevelSell = close * (1 + stopLossPercentage / 100)

// Create Buy and Sell Alerts
alertcondition(buyCondition, title="Buy Signal", message="Buy Signal - Price Crossed Below Lower Band")
alertcondition(sellCondition, title="Sell Signal", message="Sell Signal - Price Crossed Above Upper Band")

// Plot Buy and Sell Arrows on the chart
plotshape(buyCondition, style=shape.triangleup, location=location.belowbar, color=color.green, title="Buy Signal Arrow")
plotshape(sellCondition, style=shape.triangledown, location=location.abovebar, color=color.red, title="Sell Signal Arrow")

// Exit Long and Short Positions
var float stopLossBuy = na
var float stopLossSell = na

if ta.crossover(close, sma)
    stopLossBuy := stopLossLevelBuy
if ta.crossunder(close, sma)
    stopLossSell := stopLossLevelSell

strategy.entry("Buy", strategy.long, when = buyCondition)
strategy.exit("Stop Loss/Take Profit Buy", from_entry = "Buy", stop = stopLossBuy)
strategy.entry("Sell", strategy.short, when = sellCondition)
strategy.exit("Stop Loss/Take Profit Sell", from_entry = "Sell", stop = stopLossSell)

```

> Detail

https://www.fmz.com/strategy/442648

> Last Modified

2024-02-23 14:46:37
