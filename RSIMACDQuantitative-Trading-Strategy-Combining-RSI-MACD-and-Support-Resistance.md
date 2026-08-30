
> Name

Quantitative-Trading-Strategy-Combining-RSI-MACD-and-Support-Resistance
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3b079b570c182b6a7cf6a0cf77f48c94723264be04a865d00efb299f4beffb69.png)

[trans]

## Overview
This strategy is based on RSI and MACD indicators, combined with support and resistance levels to judge trading signals. It’s called the “Panda Sticking Out Its Tongue” strategy. This strategy uses the RSI indicator to determine overbought and oversold, and the MACD indicator to determine the long-short trend, and combines the highest and lowest prices within 100 periods to draw support and resistance surfaces. It generates buy signals near the support and sell signals near the resistance. It is a common trend following strategy.
## Strategy Principle
This strategy is mainly based on two indicators: RSI and MACD. The RSI indicator determines the overbought and oversold status, and the MACD indicator determines the long-short trend status. First calculate the 14-period RSI value and specify the overbought line as 70 and the oversold line as 30. Then calculate the MACD value of the 12-day fast line, the 26-day slow line, and the 9-day signal line. When the RSI is below 30, it is considered oversold; when the RSI is above 70, it is considered overbought. When the MACD fast and slow line crosses golden, it is a buy signal, and when it crosses dead, it is a sell signal.
In addition, the strategy also calculates the highest and lowest prices over a 100-period period as support and resistance levels. When a buy signal is generated, the price needs to be close to the support level, that is, the closing price must be within 1% above the support level before a buy signal is actually issued; when a sell signal is generated, the closing price must be within 1% below the resistance level before a sell signal is actually issued.
## Strategic Advantages
This strategy combines trend analysis and overbought and oversold judgments to avoid false signals caused by relying only on a single indicator. At the same time, support and resistance levels are introduced as filters to reduce erroneous transactions caused by rebounds at common support and resistance levels. MACD fast and slow lines combined with RSI indicators can more accurately determine price trends and overbought and oversold conditions. Compared with a simple moving average strategy, this strategy can capture the long-term trend of prices more flexibly.
## Strategy Risk
This strategy mainly has the following risks:
1) In a strong market, the strategy may miss most of the profits because it tends to enter the market only after the reversal cycle is over;
2) Improper setting of RSI and MACD parameters may lead to incorrect trading signals;
3) The support and resistance detection algorithm is simple and may overestimate or underestimate the true support and resistance levels;
4) The stop loss mechanism is missing. In extreme market conditions, losses cannot be effectively controlled.
To address these risks, optimization can be done by introducing adaptive MACD, optimizing RSI parameters to make them closer to the characteristics of different varieties, improving support and resistance judgment algorithms, and adding market modeling judgments.
## Strategy optimization direction
This strategy can be optimized from the following dimensions:
1) Introduce a stop loss mechanism, such as canvas AMO indicator combined with trailing stop loss
2) Use adaptive MACD to optimize MACD parameters in real time
3) Introduce market classification judgment and determine more scientific support and resistance levels
4) Combine more data to establish market status judgments, using different parameters for different statuses
5) Use machine learning algorithms for end-to-end optimization of strategies
Through these improvements, retracements can be further reduced and strategy stability improved.
## Summarize
This strategy comprehensively uses RSI and MACD indicators to determine overbought and oversold conditions, and trades near support and resistance. It is a trend following strategy with good performance. At the same time, reduce risks by combining support and resistance judgments. The advantage of this strategy is that the strategy signal is stable, the risk is controllable, and it is suitable for medium and long-term holdings. However, some parameters such as indicator parameters, support and resistance ranges, etc. can still be further optimized to improve profitability. Generally speaking, this strategy has good performance for tracking market trends and is a quantitative strategy that is easy to implement and has controllable risks.
||

## Overview

This strategy is based on the RSI and MACD indicators, combined with support/resistance levels for trade signal judgment. Its name is "Panda Sticking Out Tongue" strategy. The strategy uses the RSI indicator to determine overbought/oversold levels, the MACD indicator to determine bullish/bearish trends, and draws support/resistance levels based on the highest and lowest prices over the past 100 periods, generating buy signals near support and sell signals near resistance. It belongs to a common trend-following strategy.  

## Strategy Logic

The strategy mainly relies on two indicators - RSI and MACD. The RSI indicator judges overbought/oversold statuses, while the MACD indicator determines bullish/bearish trend statuses. It first calculates the 14-period RSI value, and sets the overbought threshold as 70 and oversold threshold as 30. Then it calculates the MACD value based on 12-day fast line, 26-day slow line, and 9-day signal line. RSI below 30 is considered oversold; RSI above 70 is considered overbought. MACD golden cross is the buy signal while death cross is the sell signal.   

In addition, the strategy also calculates the highest and lowest prices over the past 100 periods as the support/resistance levels. When a buy signal is triggered, the price needs to be close to the support level, i.e. within 1% of the support level, to actually issue a buy order. Similarly when a sell signal is triggered, the price needs to be within 1% below the resistance level to actually issue a sell order.  

## Advantages of the Strategy

The strategy combines trend analysis and overbought/oversold level detection to avoid false signals relying on single indicator only. By introducing support/resistance filter, it can reduce wrong trades due to rebounds near key S/R levels. The combination of MACD and RSI can accurately identify price movements and OB/OS statuses. Compared to simple Moving Average strategies, this strategy can capture long-term price trends more flexibly.  

## Risks of the Strategy

The main risks of this strategy includes:  

1) It may miss most profits in strong trends, as it tends to enter after reversal finishes.  

2) Inappropriate RSI and MACD parameter settings may cause wrong signals.   

3) Simple S/R detection logic may overestimate or underestimate actual S/R zones.  

4) Lack of stop loss mechanism. Unable to effectively control losses in extreme market conditions.

To address these risks, methods like adaptive MACD, optimized RSI parameters tuning, improved S/R identification, market regime modeling etc. can be used to improve the strategy.  

## Directions for Enhancement

The strategy can be enhanced from the following dimensions:  

1) Introduce stop loss mechanisms e.g. CANVAS stop loss 

2) Use adaptive MACD for dynamic parameter tuning  

3) Introduce price pattern recognition for more scientific S/R identification   

4) Incorporate more data to establish market state detection logic for using different parameters adaptively  

5) Use machine learning algorithms to optimize the strategy end-to-end

Through these improvements, we can further reduce drawdown and improve stability of the strategy.

## Conclusion
The strategy integrates RSI and MACD indicators to determine OB/OS statuses, and trade around support/resistance levels, representing a trend-following approach. By incorporating support/resistance filter, the risk is reduced. The advantage lies in stable signals and controllable risk suitable for long-term holding. Still some components e.g. indicator parameters, S/R range can be further tuned to improve profitability. Overall it shows good performance in following market trends with easy implementation and risk control.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|70|RSI Overbought Threshold|
|v_input_2|30|RSI Oversold Threshold|
|v_input_3|12|MACD Fast Length|
|v_input_4|26|MACD Slow Length|
|v_input_5|9|MACD Signal Smoothing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-28 00:00:00
end: 2024-01-04 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("RSI + MACD with Support and Resistance", shorttitle="RSI_MACD_SR", overlay=true)

// Input for RSI and MACD values
rsiOverbought = input(70, title="RSI Overbought Threshold")
rsiOversold = input(30, title="RSI Oversold Threshold")
macdFastLength = input(12, title="MACD Fast Length")
macdSlowLength = input(26, title="MACD Slow Length")
macdSignalSmoothing = input(9, title="MACD Signal Smoothing")

// Calculating RSI and MACD
rsiValue = ta.rsi(close, 14)
[macdLine, signalLine, _] = ta.macd(close, macdFastLength, macdSlowLength, macdSignalSmoothing)

// Support and Resistance
support = ta.lowest(100)
resistance = ta.highest(100)

// Drawing support and resistance lines
// line.new(x1=bar_index[0], y1=support, x2=bar_index[-1], y2=support, color=color.green, width=1)
// line.new(x1=bar_index[0], y1=resistance, x2=bar_index[-1], y2=resistance, color=color.red, width=1)

// Buy Condition: If RSI is oversold and MACD line crosses above the signal line
// Additionally, check if price is near the support line
longCondition = ta.crossover(macdLine, signalLine) and rsiValue < rsiOversold and (close - support) < (close * 0.01)
strategy.entry("Long", strategy.long, when=longCondition, comment="Buy")

// Sell Condition: If RSI is overbought and MACD line crosses below the signal line
// Additionally, check if price is near the resistance line
shortCondition = ta.crossunder(macdLine, signalLine) and rsiValue > rsiOverbought and (resistance - close) < (close * 0.01)
strategy.entry("Short", strategy.short, when=shortCondition, comment="Sell")

// Plot values on the chart for visualization
plotshape(series=longCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="Buy")
plotshape(series=shortCondition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="Sell")
```

> Detail

https://www.fmz.com/strategy/437801

> Last Modified

2024-01-05 16:24:58
