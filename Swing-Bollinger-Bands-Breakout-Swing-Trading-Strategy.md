
> Name

Bollinger Bands Breakout-Swing-Trading StrategyBollinger-Bands-Breakout-Swing-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2e6fe7d4b586111091d3f6d2773efff176e09e77a6394f5599be1e74958700c5.png)
[trans]

### Overview
This strategy is a breakout trading strategy based on Bollinger Bands. It uses the upper edge and middle line of Bollinger Bands to implement Swing trading. Specifically, it goes long when the price breaks through the upper line of the Bollinger Bands, and closes the position when the price falls below the middle line of the Bollinger Bands. This is a classic trend following strategy.
### Strategy Principles
1. Calculate the Bollinger Bands on the 20th, including the upper track, middle line and lower track
2. When the closing price is greater than the upper track, go long
3. When the closing price is lower than the midline, close the position
The above is the main trading logic of this strategy. It is simple and effective and can capture strong trend conditions.
### Advantage Analysis
This Bollinger Bands Swing strategy mainly has the following advantages:
1. Simple operation and easy to implement.
2. Able to effectively track strong trends, and the holding time will not be too long.
3. Taking advantage of the Bollinger Bands indicator itself, there is a certain probability advantage.
In general, this is a trend strategy that performs relatively well, is simple, practical, and easy to control.
### Risks and Solutions
This strategy also has some risks, mainly including:
1. The Bollinger Bands indicator itself has a certain sensitivity to market fluctuations, which may cause frequent opening and closing of positions. This can be avoided by appropriately adjusting parameters or adding filter conditions.
2. Unable to effectively handle consolidation market conditions, during which losses or frequent small-amount transactions may occur. Consider using other strategies in this market.
In addition, you can also combine more filter indicators or optimize stop loss strategies to control risks.
### Optimization direction
This strategy can be optimized from the following directions:
1. Optimize Bollinger Band parameters to adapt to wider market conditions.
2. Add additional indicator judgments to improve decision-making accuracy. For example, KDJ, MACD, etc.  
3. Optimize the stop loss strategy, set reasonable stop loss points, and control single losses.
4. Optimize position management and use different trading positions for different market conditions.
Through systematic testing and optimization, the strategy can be continuously improved and profitability improved.
### Summarize
This Bollinger Bands Swing strategy is overall very practical. It is simple to operate and easy to implement trend tracking. At the same time, there are also some risks that need attention, which can be solved through parameter adjustment and optimization. This is a recommended quantitative strategy.

|| 

### Overview

This is a breakout trading strategy based on Bollinger Bands. It uses the upper band and middle line of Bollinger Bands to implement swing trading. Specifically, it goes long when the price breaks above the upper band and closes position when the price falls below the middle line. This is a typical trend following strategy.  

### Strategy Logic   

1. Calculate 20-day Bollinger Bands, including upper band, middle line and lower band
2. When close price is above the upper band, go long
3. When close price is below the middle line, close position

The above is the main trading logic of this strategy. It is simple and effective to capture relatively strong trending moves.

### Advantage Analysis

The main advantages of this Bollinger Bands swing strategy are:  

1. Simple to implement and easy to execute.  
2. Can effectively track relatively strong trends without holding position for too long.
3. Utilize the inherent advantage of Bollinger Bands indicator itself for better probability.

In general, this is a relatively well-performed trend following strategy that is simple, practical and easy to control.  

### Risks and Solutions   

There are also some risks with this strategy:   

1. Bollinger Bands itself is sensitive to market fluctuation, may cause frequent opening and closing of positions. This can be avoided by adjusting parameters or adding filters.  
2. Ineffective in range-bound markets, may lead to losses or frequent small trades. Consider using other strategies in such markets.  

Also possible to control risks by combining more filter indicators or optimizing stop loss strategies.

### Optimization Directions   

The strategy can be optimized from the following aspects:

1. Optimize Bollinger Bands parameters to adapt to more market conditions.  
2. Add additional indicators for better decision accuracy, e.g. KDJ, MACD etc.
3. Optimize stop loss strategy, set reasonable stop loss points to control single trade loss.  
4. Optimize position sizing, use different sizes for different market conditions.  

Continuous improvement of the strategy can be done through systematic testing and optimization for better profitability.  

### Summary   

Overall this Bollinger Bands swing trading strategy is very practical. It has simple operation for easy trend following. There are also some risks to note, which can be addressed through parameter tuning and optimization. This is a recommended quantitative strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Bollinger Band Length|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|2|Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-02 00:00:00
end: 2024-01-02 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands Breakout Strategy", overlay=true)

// Bollinger Band Einstellungen
length = input(20, title="Bollinger Band Length")
src = input(close, title="Source")
mult = input(2.0, title="Multiplier")

basis = ta.sma(src, length)
upper_band = basis + mult * ta.stdev(src, length)
lower_band = basis - mult * ta.stdev(src, length)

// Bedingung für den oberen Ausbruch
upper_breakout_condition = close > upper_band

// Bedingung für den Rückgang unter das mittlere Band
below_middle_band_condition = close < basis

// Plot der Bollinger Bänder
plot(upper_band, color=color.blue, title="Upper Bollinger Band")
plot(basis, color=color.purple, title="Middle Bollinger Band")
plot(lower_band, color=color.blue, title="Lower Bollinger Band")

// Kaufregel
if (upper_breakout_condition)
    strategy.entry("Buy", strategy.long)

// Verkaufsregel
if (below_middle_band_condition)
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/437550

> Last Modified

2024-01-03 16:40:38
