
> Name

Bollinger-Bands-Strategy-with-RSI-Filter based on RSI filter
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/805c68db37f0c9dbefb9cc3a7c1414cb1d19854f5326b33c78823fbb39c720d3.png)

[trans]

## Overview
The name of this strategy is "Bollinger Band Strategy Based on RSI Filter". It is a quantitative strategy that uses the Bollinger Band principle and combines the RSI indicator as a filter to determine entry. This strategy can effectively judge market trends, buy low and sell high, and obtain better returns.
## Strategy Principle
The core indicator of this strategy is Bollinger Bands. Bollinger Bands consist of a middle line, an upper line, and a lower line. The middle line is the n-day moving average, the upper line is the middle line plus k times the n-day standard deviation, and the lower line is the middle line minus k times the n-day standard deviation. When the price is close to the upper line, it means that the market is overvalued, and you should consider going short. When the price is close to the lower line, it means that the market is undervalued, and you should consider going long.
This strategy is based on Bollinger Bands and adds the RSI indicator as an entry filter. RSI can determine whether the market is overbought or oversold. When the RSI is above 70, it means overbought, and when it is below 30, it means oversold. This strategy will only consider entering the market when the Bollinger Bands send out a trading signal and the RSI meets the overbought and oversold conditions.
Specifically, when the price breaks through the lower line of the Bollinger Bands from bottom to top and the RSI is below the oversold line of 30, a buy signal is generated; when the price breaks through the upper line of the Bollinger Bands from top to bottom and the RSI is above the overbought line of 70, a sell signal is generated.
## Advantage Analysis
This strategy combines Bollinger Bands and RSI indicators to effectively determine the overbought and oversold conditions in the market and avoid unnecessary losses caused by false breakthroughs. At the same time, the RSI indicator serves as a filter, which can filter out some noisy trading signals and make the entry timing more accurate.
This strategy requires fewer parameters, the implementation process is simple and clear, and is suitable for quantitative traders of different levels. Medium and long-term holdings are more effective and avoid being disturbed by short-term market fluctuations.
In general, this strategy has the following advantages:
1. Combined with Bollinger Bands and RSI, the judgment ability is stronger
2. Reduce losses caused by false breakthroughs
3. Simple parameters and easy to implement
4. Medium and long-term holding, smaller retracement
## Risk Analysis
There are also some risks in this strategy that you need to be wary of:
1. Improper setting of Bollinger Band parameters will cause the effect of trading signals to deteriorate.
2. In trending markets, Bollinger Bands often move along with prices and should not be used.
3. RSI is prone to divergence, affecting the accuracy of trading signals.
4. The number of transactions may be small and long-term losses may occur easily.
To control these risks, it is recommended to:
1. Optimize Bollinger Band parameters and select the best parameter combination
2. Pay attention to large-scale market structures and avoid using them in volatile trends.
3. Confirm RSI signals in combination with other indicators to prevent false signals
4. Appropriately adjust the holding time to prevent huge losses
## Optimization direction
There is room for further optimization of this strategy:
1. Can test different RSI parameter settings
2. You can add a stop-loss strategy to better control risks
3. Can be combined with other indicators for combined verification
4. Parameters can be automatically optimized through machine learning methods
These optimizations can make the strategy more stable, parameters more optimized, and risk control better.
## Summarize
The name of this strategy is "Bollinger Band Strategy Based on RSI Filter". It integrates the ability of Bollinger Bands to judge overbought and oversold, and the ability of RSI to judge market momentum to form a strong quantitative strategy. This strategy has unique advantages in judging long and short market opportunities and can bring better excess returns.
Despite this, there is still room for improvement in this strategy. Through parameter optimization, risk control and other means, the strategy can be more effective and adapt to more different market conditions. This is also a major research direction in the future.
||
## Overview  

The name of this strategy is “Bollinger Bands Strategy with RSI Filter”. It utilizes the principles of Bollinger Bands combined with the RSI indicator as a filter for entry signals. This strategy can effectively determine market trends for buying low and selling high to achieve decent profits.   

## Strategy Principle

The core indicator of this strategy is Bollinger Bands, consisting of the middle band, upper band and lower band. The middle band is the n-period moving average, the upper band is the middle band plus k times the n-period standard deviation, and the lower band is the middle band minus k times the n-period standard deviation. When the price approaches the upper band, the market is overvalued and short positions should be considered. When the price approaches the lower band, the market is undervalued and long positions should be considered.   

In addition to Bollinger Bands, this strategy incorporates the RSI indicator as a filter for entry signals. The RSI judges whether the market is overbought or oversold. Values above 70 indicate overbought conditions and values below 30 indicate oversold conditions. This strategy only enters trades when Bollinger Bands give signal concurrently with RSI reaching overbought or oversold levels.   

Specifically, when the price breaks above the lower Bollinger Band from below while the RSI is below 30, a buy signal is generated. When the price breaks below the upper Bollinger Band from above while the RSI is above 70, a sell signal is generated.  

## Advantage Analysis  

This strategy combines Bollinger Bands with the RSI indicator to effectively identify overbought and oversold market conditions, avoiding unnecessary losses from false breakouts. The RSI acts as a filter to remove some market noise, making entry timing more accurate.  

The strategy has few parameters and is simple to implement, suitable for quantitative traders of all skill levels. A mid to long-term holding strategy avoids interference from short-term market fluctuations.   

In summary, the advantages are:  

1. Stronger judgment integrating Bollinger Bands and RSI  
2. Reduces losses from false breakouts
3. Simple parameters, easy to implement   
4. Smaller drawdowns with mid to long-term holdings  

## Risk Analysis   

Some risks to be aware of with this strategy include:   

1. Inappropriate Bollinger Bands parameter settings worsen signal quality  
2. Bollinger Bands tend to follow price action in trending markets  
3. RSI divergences affect signal accuracy
4. Infrequent trading signals risk long-term losses  

To control these risks:  

1. Optimize parameters to find best combinations  
2. Consider higher timeframe structure to avoid ranging markets   
3. Confirm RSI signals with other indicators to avoid false signals  
4. Adjust holding period to prevent severe losses  

## Optimization Directions   

Further improvements:  

1. Test different RSI parameters   
2. Incorporate stop losses to better control risk
3. Add other indicators to combine confirmations  
4. Utilize machine learning for automated parameter optimization   

These enhancements can improve stability, optimize parameters, and strengthen risk management.  

## Conclusion  

The “Bollinger Bands Strategy with RSI Filter” integrates Bollinger Bands’ overbought/oversold identification with RSI’s momentum gauge to form a robust quantitative strategy. The strategy has unique advantages in determining market opportunities across timeframes, capable of generating significant alpha. 

Nonetheless, there is room for improvement via parameter optimization and risk control to adapt performance across diverse market conditions, an area warranting further research.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|length|
|v_input_float_1|2|mult|
|v_input_1|14|RSI Length|
|v_input_2|70|RSI Overbought Level|
|v_input_3|30|RSI Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-28 00:00:00
end: 2023-11-27 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands Strategy with RSI Filter", overlay=true)
source = close
length = input.int(20, minval=1)
mult = input.float(2.0, minval=0.001, maxval=50)
basis = ta.sma(source, length)
dev = mult * ta.stdev(source, length)
upper = basis + dev
lower = basis - dev

// RSI Filter
rsiLength = input(14, title="RSI Length")
rsiOverbought = input(70, title="RSI Overbought Level")
rsiOversold = input(30, title="RSI Oversold Level")
rsiValue = ta.rsi(source, rsiLength)

// Buy and Sell Conditions with RSI Filter
buyEntry = ta.crossover(source, lower) and rsiValue < rsiOversold
sellEntry = ta.crossunder(source, upper) and rsiValue > rsiOverbought

// Entry and Exit Logic
if (buyEntry)
    strategy.entry("BBandLE", strategy.long, stop=lower, oca_name="BollingerBands", comment="BBandLE")
else
    strategy.cancel(id="BBandLE")

if (sellEntry)
    strategy.entry("BBandSE", strategy.short, stop=upper, oca_name="BollingerBands", comment="BBandSE")
else
    strategy.cancel(id="BBandSE")

// Plot Bollinger Bands on the chart
plot(upper, color=color.red, title="Upper Band")
plot(lower, color=color.green, title="Lower Band")

// Plot RSI on the chart
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiOversold, "Oversold", color=color.green)
plot(rsiValue, color=color.blue, title="RSI")

// Plot buy and sell signals on the chart
plotshape(series=buyEntry, title="Buy Signal", color=color.green, style=shape.triangleup, location=location.belowbar)
plotshape(series=sellEntry, title="Sell Signal", color=color.red, style=shape.triangledown, location=location.abovebar)

```

> Detail

https://www.fmz.com/strategy/433528

> Last Modified

2023-11-28 12:12:41
