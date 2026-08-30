
> Name

Trend-Tracking-Breakout-Strategy Based on Trend-Tracking-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11936cb3419abff41bb.png)
[trans]

## Overview
The Trend Following Breakout Strategy is a trend following strategy based on moving averages and Bollinger Bands indicators. This strategy combines the ideas of trend analysis and breakthrough trading to identify market trends while looking for opportunities with breakthrough potential.
## Strategy Principle
This strategy uses a 50-period simple moving average to determine trend direction. When the closing price crosses the 50-day line, consider going long. At the same time, the closing price is required to be higher than the lower Bollinger Band, and the lowest price of the current K-line is close to the lower Bollinger Band, indicating that the price is near the support position and may form a breakthrough.
After the entry signal is formed, if the opening price of the second K line is higher than the previous day's highest price plus the stop loss position of 1 point, then the real entry is long.
The stop loss position is preset to the lowest price of the entry K line minus 5.7 points. The take-profit position is set to the closing price of entry plus 11.4 points, achieving a risk-reward ratio of 2 times.
## Strategic advantage analysis
This strategy combines trend judgment and breakthroughs formed near key supports, which can effectively filter out false breakthroughs and improve the winning rate of transactions. Stop loss and take profit are set according to the risk-return ratio principle, which is conducive to risk control.
Relatively simple indicators and judgment conditions make the strategy easy to understand and implement, making it suitable for beginners to learn quantitative trading.
## Strategy risk analysis
This strategy mainly relies on moving averages to determine the direction of the trend. When the trend changes, it may produce false signals. Improperly set Bollinger Band parameters may also lead to false breakouts.
A stop-loss position that is too close may result in immediate exit, and a take-profit position that is too large may also limit profits. The settings of these parameters need to be adjusted according to different markets.
This strategy only considers the highest and lowest prices within the day and cannot respond to overnight gaps.
## Strategy optimization direction
You can consider combining other indicators to determine the trend, such as MACD. Or use an adaptive moving average to track changes in trend.
Bollinger Band parameters can be optimized to find the best parameter combination. Stop loss and take profit positions can also be optimized based on backtesting results.
The judgment logic for overnight short jumps can be added to avoid the expansion of losses after short jumps.
## Summarize
This strategy integrates trend judgment and breakthrough trading ideas, and uses simple indicators to form a filtering effect. The advantage of the strategy is that it is easy to understand and implement, and better results can be obtained through parameter optimization. However, there are also certain market risks, which need to be continuously improved based on the actual results.
||  

## Overview

The Trend Tracking Breakout Strategy is a trend following strategy based on moving average and Bollinger Bands indicators. It combines the ideas of trend analysis and breakout trading, seeking breakout opportunities while determining the market trend.  

## Strategy Logic  

The strategy uses the 50-period simple moving average (SMA) to determine the trend direction. A long position is considered when the closing price crosses above the 50-day SMA, indicating a potential upward trend.  

At the same time, it requires the closing price to be above the lower Bollinger Band, suggesting the price is not in the lower extreme and may be poised for an upward move. The low of the candle must be within 1% of the lower Bollinger Band, indicating potential support near that level for a breakout.

After the entry signal is triggered, the strategy checks if the next day's opening price is above the stop level, which is set at 1 point above the highest price of the previous day, to confirm the actual entry. 

The stop loss is preset at 5.7 points below the low of the entry bar. Take profit is set at 11.4 points above the closing price of the entry bar to achieve a 2:1 risk-reward ratio.

## Advantage Analysis 

The strategy combines trend judgment and breakout near key support levels to effectively filter false breakouts and improve win rate. Stop loss and take profit are set according to risk-reward principles to aid risk control.

The relatively simple indicators and entry rules make the strategy easy to understand and implement, suitable for beginners to learn algorithmic trading.  

## Risk Analysis

The strategy relies mainly on moving averages to determine trend direction, which may generate incorrect signals when the trend changes. Improper Bollinger Bands parameters could also lead to false breakouts.

The stop loss being too close may get stopped out prematurely. Take profit being too wide could also limit profits. These parameters need adjusting for different markets.

The strategy only considers the daily high and low prices and cannot react to overnight gaps.  

## Optimization Directions 

Other indicators could be combined to determine the trend, like MACD. Or adaptive moving averages can be used to track trend changes.

Bollinger Bands parameters can be optimized to find the best combination. Stop loss and take profit levels can also be optimized based on backtesting results. 

Logic can be added to judge overnight gaps, avoiding widened losses after gaps.

## Conclusion  

The strategy integrates the ideas of trend following and breakout trading, using simple indicators to create a filtering effect. Its advantage lies in being easy to understand and implement. Through parameter optimization, better results can be achieved. But there are also market risks to be aware of, requiring continuous improvements based on live trading results.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-25 00:00:00
end: 2023-12-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Custom Strategy", overlay=true)

// Input variables
smaLength = 50
bbLength = 20
supportPercentage = 1
riskRewardRatio = 2

// Calculate indicators
sma = sma(close, smaLength)
bb_lower = sma(close, bbLength) - 2 * stdev(close, bbLength)

// Entry conditions based on provided details
enterLongCondition = crossover(close, sma) and close > bb_lower and low <= (bb_lower * (1 + supportPercentage / 100))

// Entry and exit logic
if (enterLongCondition)
    strategy.entry("Long", strategy.long)

// Assuming the details provided are for the daily timeframe
stopLossPrice = low - 5.70
takeProfitPrice = close + 11.40

strategy.exit("Take Profit/Stop Loss", from_entry="Long", loss=stopLossPrice, profit=takeProfitPrice)

// Plotting
plot(sma, color=color.blue, title="50 SMA")
plot(bb_lower, color=color.green, title="Lower Bollinger Band")

// Plot entry points on the chart
plotshape(series=enterLongCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="Buy")

```

> Detail

https://www.fmz.com/strategy/436603

> Last Modified

2023-12-26 10:52:51
