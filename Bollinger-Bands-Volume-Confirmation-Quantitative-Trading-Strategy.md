
> Name

Double confirmation quantitative trading strategy based on Bollinger Bands and trading volume Bollinger-Bands-Volume-Confirmation-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11c72904cb4f8a38682.png)
[trans]

## Overview
This strategy is called "Bollinger Bands Volume Confirmation Strategy". Its core idea is to combine Bollinger Bands indicators and trading volume indicators to achieve double confirmation of price trends and trading volumes, thereby generating more reliable buy and sell signals.
## Strategy Principle
This strategy mainly consists of two parts:
1. Bollinger Bands indicator part. This part calculates the simple moving average of the closing prices for a certain period (such as the 20th), and calculates the standard deviation of these closing prices relative to its moving average. Then based on the value of the standard deviation, a band-shaped area corresponding to one standard deviation range above and below the moving average is calculated, which is called the Bollinger Band. The band area of ​​Bollinger Bands can clearly show whether the current price is in an "abnormal state".
2. Transaction volume part. This part calculates the moving average of the trading volume within the same period (such as the 20th), and then uses a multiplier (such as 2.0) to set the trading volume threshold. Only when the trading volume exceeds this threshold is the effective "large" trading volume occurring.
When the price goes above the upper Bollinger Band and the trading volume exceeds the trading volume threshold, a buy signal is generated; when the price goes below the lower Bollinger Band and the trading volume exceeds the trading volume threshold, a sell signal is generated.
Through double confirmation of price and trading volume, some false signals can be filtered out, making the trading strategy more reliable.
## Strategic Advantages
1. Double confirmation mechanism to avoid false breakthroughs and filter out noise. Combining price and trading volume indicators will only generate signals when both are confirmed at the same time, which can effectively avoid some false signals caused by price breakthroughs in short situations.
2. The parameters are highly adjustable. Users can set the cycle parameters of Bollinger Bands and the multiple parameters of the transaction volume threshold by themselves to adapt to different market environments.
3. Intuitive diagram. Visual indicators of upper and lower Bollinger Bands, trading volume and trading volume thresholds make strategy signals more intuitive and clear.
## Risk and optimization analysis
1. Bollinger Bands by themselves do not perfectly identify trend reversal points. Bollinger Bands can only clearly show the "abnormal state" of price, but cannot predict price reversal. Therefore, it still needs to be judged in combination with other indicators.
2. Volume signals may lag. When quickly breaking through the upper and lower Bollinger Bands, the reaction of trading volume may lag behind, resulting in a lag in signal generation and failure to perfectly capture the turning point.
3. You can try to combine it with other indicators. Indicators such as KDJ and MACD introduce more variables and establish more complex multi-trading strategies, thereby improving the practicality of the strategy.
## Summarize
This strategy filters out excessive noise to a certain extent through double confirmation and parameter adjustment, making trading decisions more reliable. However, we still need to be wary of the limitations of Bollinger Bands itself. Later, we can try to introduce other indicators for optimization and establish a diversified quantitative strategy.

||


## Overview  

This strategy is called “Bollinger Bands Volume Confirmation Strategy”. Its core idea is to combine the Bollinger Bands indicator and volume indicator to achieve double confirmation of price movement and trading volume, thereby generating more reliable buy and sell signals.

## Strategy Principle

The strategy mainly includes two parts:  

1. Bollinger Bands part. This part calculates the simple moving average of closing prices over a certain period (such as 20 days) and calculates the standard deviation of these closing prices relative to their moving average. Then, according to the value of the standard deviation, two bands are calculated at a standard deviation range above and below the moving average, which is called Bollinger Bands. The band area of Bollinger Bands can clearly show whether the current price is in an "abnormal state".   

2. Volume part. This part calculates the moving average value of trading volume over the same period (such as 20 days), and then uses a multiplier (such as 2.0) to set a trading volume threshold. Only when the trading volume exceeds this threshold is it regarded as a valid "large" trading volume.

When the price breaks through the upper track of Bollinger Bands and the trading volume exceeds the trading volume threshold, a buy signal is generated; when the price breaks through the lower track of Bollinger Bands, and the trading volume exceeds the trading volume threshold, a sell signal is generated.  

By the double confirmation of price and trading volume, some false signals can be filtered out, making the trading strategy more reliable.  

## Strategy Advantages 

1. Double confirmation mechanism to avoid false breakouts and filter noise. Combining price and volume indicators, signals are generated only when both confirm at the same time, which can effectively avoid some erroneous signals caused by empty price breakouts.  

2. Adjustable parameters. Users can set the period parameters of Bollinger Bands and the multiplier parameters of the trading volume threshold independently to adapt to different market environments.   

3. Intuitive illustration. The upper and lower Bollinger Bands, trading volume, and trading volume threshold indicators enable more intuitive and clear strategy signals.  

## Risks and Optimization  

1. Bollinger Bands itself cannot perfectly identify trend reversal points. Bollinger Bands can only clearly show the "abnormal state" of prices but cannot predict price reversals. Therefore, it still needs to be combined with other indicators for judgment.  

2. Volume signals may lag. When there is a rapid breakout of the upper and lower Bollinger Bands, the reaction of the trading volume may lag, resulting in a lag in signal generation and inability to perfectly capture turning points.  

3. Try to combine other indicators. Indicators such as KDJ, MACD, etc., introduce more variables to establish more complex multivariate trading strategies, thereby improving the practicality of the strategy.  

## Summary  

By using the method of double confirmation and parameter adjustment, this strategy has filtered out too much noise to some extent, making trading decisions more reliable. But the limitations of Bollinger Bands itself still need to be guarded against. In the future, other indicators can be introduced to optimize and establish diversified quantitative strategies.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|BB Length|
|v_input_2|2|Multiplier|
|v_input_3|2|Volume Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-26 00:00:00
end: 2024-01-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Volume + Bollinger Bands Strategy", overlay = true, shorttitle="Vol BB Strategy")

// Bollinger Bands Parameters
length = input(20, title="BB Length")
src = close
mult = input(2.0, title="Multiplier")
basis = ta.sma(src, length)
upper = basis + mult * ta.stdev(src, length)
lower = basis - mult * ta.stdev(src, length)

// Volume Parameters
volMultiplier = input(2.0, title="Volume Multiplier")
avgVolume = ta.sma(volume, length)

// Strategy Logic
buyCondition = close > upper and volume > volMultiplier * avgVolume
sellCondition = close < lower and volume > volMultiplier * avgVolume

// Plotting
plot(upper, color=color.red, title="Upper Band")
plot(lower, color=color.green, title="Lower Band")
plot(volume, color=color.blue, style=plot.style_columns, title="Volume", transp=85)
plot(avgVolume * volMultiplier, color=color.orange, title="Avg Volume x Multiplier")

// Strategy Execution
strategy.entry("Buy", strategy.long, when=buyCondition)
strategy.close("Buy", when=sellCondition)

bgcolor(buyCondition ? color.new(color.green, 90) : sellCondition ? color.new(color.red, 90) : na)

```

> Detail

https://www.fmz.com/strategy/437386

> Last Modified

2024-01-02 11:04:35
