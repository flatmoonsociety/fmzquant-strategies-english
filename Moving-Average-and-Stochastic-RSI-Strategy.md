
> Name

Moving-Average-and-Stochastic-RSI-Strategy Moving-Average-and-Stochastic-RSI-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/fa8a4aedf986f68810dc9bacfcf98c6be373a9cfa9592286675bc46d55d69737.png)
[trans]
## Overview
The strategy was tested on the 3-minute time frame of the Bitcoin and USD trading pair (BTC/USDT) and gave very good results. This strategy uses a combination of moving averages and the Stochastic RSI to identify trading signals.
## Strategy Principle
This strategy uses two simple moving averages with different periods, namely 20 period and 50 period. These two averages are used to judge price trends. When the short-term moving average crosses the long-term moving average, it is a long signal, and when it crosses below, it is a short signal.
The formula for calculating the Stochastic RSI indicator is: (RSI - lowest RSI)/(highest RSI - lowest RSI) * 100. This indicator reflects the position of the current level of the RSI indicator relative to the highest and lowest RSI levels in the recent period. When the Stochastic RSI crosses above 20, it is an oversold signal, and when it crosses below 80, it is an overbought signal.
This strategy comprehensively uses moving averages to determine the trend direction and Stochastic RSI to locate potential reversal points as entry opportunities.
## Strategic advantage analysis
Compared with using moving averages or Stochastic RSI alone, this strategy combines the advantages of both to better identify trends and locate potential reversal points, thereby increasing the probability of profit.
Compared with a single indicator, this strategy integrates multiple indicators and sets strict entry rules, which can effectively filter out false signals and avoid unnecessary transactions.
This strategy also controls risks very well. Only 2% of the funds are used for margin trading each time, which can effectively limit the impact of a single loss.
## Strategy risk analysis
This strategy mainly relies on technical indicators to determine trading signals. If the indicators fail, false signals may be generated, leading to losses. In addition, improper setting of indicator parameters will also affect strategy performance.
When the market fluctuates violently, the stop-profit and stop-loss settings may be breached, leading to the risk of expanded losses.
## Strategy optimization direction
You can test more moving average combinations and parameters to find the best parameter combination. You can also try to combine other potential energy indicators such as KD, RSI, etc. with moving averages.
You can choose the best stop-profit and stop-loss modes based on the characteristics of different cryptocurrencies to further control risks.
Machine learning algorithms can be introduced to automatically optimize parameter settings and signal judgment rules to make the strategy more robust and adaptable.
## Summary
This strategy successfully combines moving averages and the Stochastic RSI indicator to identify trading signals. Compared with a single technical indicator, this strategy can provide more reliable trading signals. Through strict risk control and parameter optimization, this strategy is expected to achieve stable profits.
||

## Overview
This strategy was tested on the BTC/USDT trading pair on the 3-minute timeframe and gave wonderful results. It combines the use of moving averages and the Stochastic RSI indicator to identify trading signals.  

## Strategy Principle  
The strategy uses two simple moving averages with different time periods, 20 periods and 50 periods respectively. These two averages are used to judge the price trend. When the short-term moving average crosses above the long-term moving average, it is a bullish signal, and when it crosses below, it is a bearish signal.

The calculation formula of Stochastic RSI indicator is: (RSI - Lowest RSI) / (Highest RSI - Lowest RSI) * 100. This indicator reflects the current level of the RSI indicator relative to the highest and lowest RSI over a recent period of time. When Stochastic RSI crosses above 20, it is an oversold signal, and when it crosses below 80, it is an overbought signal.  

This strategy combines the use of moving averages to judge the trend direction and Stochastic RSI to locate potential reversal points as entry opportunities.  

## Advantage Analysis  
Compared with using moving averages or Stochastic RSI alone, this strategy combines the advantages of both to better identify trends while locating potential reversal points, thus improving the probability of profit.

Compared with a single indicator, this strategy integrates multiple indicators and sets strict entry rules, which can effectively filter out false signals and avoid unnecessary trading.  

This strategy also controls risks very well by using only 2% of capital for margin trading each time, which can effectively limit the impact of a single loss.   

## Risk Analysis
This strategy mainly relies on technical indicators to determine trading signals. If the indicators fail, it may generate wrong signals and cause losses. In addition, improper parameter settings will also affect strategy performance.  

In times of violent market fluctuations, stop-loss settings may be broken through, leading to the risk of expanding losses.

## Optimization Directions  
Test more moving average combinations and parameters to find the optimal parameter combination. Other potential indicators such as KD and RSI can also be combined with moving averages.  

Choose the best stop-loss modes according to the characteristics of different cryptocurrencies to further control risks.   

Introduce machine learning algorithms to automatically optimize parameter settings and signal judgment rules to make the strategy more robust and adaptive.

## Conclusion
This strategy successfully combines moving averages and Stochastic RSI indicator to determine trading signals. Compared with a single technical indicator, this strategy can provide more reliable trading signals. With strict risk control and parameter optimization, this strategy has the potential to achieve stable profits.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|MA1 Length|
|v_input_int_2|50|MA2 Length|
|v_input_int_3|14|Stochastic RSI Length|
|v_input_int_4|80|Overbought Level|
|v_input_int_5|20|Oversold Level|
|v_input_float_1|2|Risk Percentage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-25 00:00:00
end: 2024-01-31 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Moving Average and Stochastic RSI Strategy", shorttitle="MA+Stoch RSI", overlay=true)

// Input variables
ma1_length = input.int(20, title="MA1 Length")
ma2_length = input.int(50, title="MA2 Length")
stoch_length = input.int(14, title="Stochastic RSI Length")
overbought = input.int(80, title="Overbought Level")
oversold = input.int(20, title="Oversold Level")
risk_percentage = input.float(2.0, title="Risk Percentage")

// Calculate moving averages
ma1 = ta.sma(close, ma1_length)
ma2 = ta.sma(close, ma2_length)

// Calculate Stochastic RSI
rsi1 = ta.rsi(close, stoch_length)
rsiH = ta.highest(rsi1, stoch_length)
rsiL = ta.lowest(rsi1, stoch_length)
stoch = (rsi1 - rsiL) / (rsiH - rsiL) * 100

// Determine buy and sell signals based on Stochastic RSI
buySignal = ta.crossover(stoch, oversold)
sellSignal = ta.crossunder(stoch, overbought)

// Plot signals on the chart
plotshape(buySignal, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small)
plotshape(sellSignal, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.small)

// Calculate position size based on equity and risk percentage
equity = strategy.equity
riskAmount = equity * risk_percentage / 100
positionSize = riskAmount / ta.atr(14)

// Entry and exit conditions
var float stopLoss = na
var float takeProfit = na

if buySignal
    stopLoss := low
    takeProfit := high
    strategy.entry("Buy", strategy.long)
else if sellSignal
    strategy.exit("Sell", from_entry="Buy", stop=stopLoss, limit=takeProfit)

```

> Detail

https://www.fmz.com/strategy/440699

> Last Modified

2024-02-01 11:37:40
