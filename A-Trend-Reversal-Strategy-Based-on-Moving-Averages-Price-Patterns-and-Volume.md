
> Name

A-Trend-Reversal-Strategy-Based-on-Moving-Averages-Price-Patterns-and-Volume
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/4f0cd98c90d7263e1b.png)
 [trans]

## Overview
This strategy uses a combination of moving averages, price patterns, and volume to identify reversal points in the market. When the fast moving average crosses the slow moving average, and a bull engulfing pattern appears, breaks through the resistance level, and trading volume increases, the strategy will go long; conversely, when the fast moving average crosses the slow moving average, and a short engulfing pattern appears, falls below the support level, and trading volume amplifies, the strategy will go short.
## Principle
The core idea of ​​this strategy is to use a combination of moving average systems, price patterns, and volume to identify potential reversal points. Specifically, the golden cross and death cross of the moving average can determine the trend conversion. Both price patterns, bull engulfing and bear engulfing, often signal short-term reversals. An influx of trading volume also often signals an impending trend reversal. The combined use of these three signals can relatively accurately grasp the timing of reversal.
From the code logic point of view, first calculate the fast moving average and slow moving average. Then set the judgment conditions for long engulfment and short engulfment. Supportive resistance levels and conditions for volume amplification are also set. When the moving average golden cross is met, the bull engulfing pattern is met, the resistance level is broken through, and the trading volume is enlarged, a long signal is issued; when the moving average death cross is met, the short engulfing pattern is met, the support level is broken, and the trading volume is enlarged, a closing signal is issued.
## Advantages
The biggest advantage of this strategy is that it uses a combination of multiple signals to identify reversals, which can effectively reduce false signals. Specifically, relying solely on a single moving average, price pattern or volume can easily lead to wrong trading signals. But if all three signals appear at the same time, the success rate of predicting a reversal will be greatly improved.
Additionally, this strategy utilizes both trend and reversal factors. Before a reversal signal appears, there must be a trend. In other words, this strategy will only look for reversal opportunities within a trend context. This also reduces randomness and increases the probability of profit.
## Risk
The biggest risk of this strategy is that the reversal fails, that is, after a long signal is issued, the price continues to fall; or after a short signal is issued, the price continues to rise. This is usually due to a misjudgment, and the reversal signal is just an illusion, or it is just a short-term adjustment, and then the original trend continues.
The solution is to adjust the moving average parameters to identify longer-period trends; at the same time, appropriately enlarge the stop loss range and stop the loss in time after the reversal fails. In addition, more factors can also be combined to confirm the reversal, such as the price pattern of a large cycle, etc.
## optimization
This strategy can be optimized through the following aspects:
1. Adjust the moving average parameters to identify more appropriate long and short periods.
2. Test different support and resistance level algorithms, such as Pareto support and resistance levels.
3. Try different trading volume indicators, such as energy tide indicators, trading volume swing indicators, etc.
4. Add more signals that confirm reversal, such as long-term price patterns, dramatic amplification of trading volume, etc.
5. Combine with stock index futures for cross-market confirmation, and use stock index futures to confirm the reversal of individual stocks.
By testing different parameter combinations, this strategy can be further optimized to increase profitability and win rate.
## Summarize
This strategy integrates three factors: moving average system, price pattern and trading volume to identify reversals, achieving an effective combination of multiple signals. It only looks for reversal opportunities in the context of trends and avoids random trading. By further optimizing the parameters and adding confirmation factors, this strategy can become a very practical short-term reversal strategy.
||

## Overview

This strategy combines moving averages, price patterns and volume to identify potential trend reversal points in the market. It goes long when the fast moving average crosses above the slow moving average, a bullish engulfing pattern appears, resistance level breaks, and trading volume surges. It goes short when the opposite conditions occur.  

## Principles

The core idea of this strategy is to use a combination of moving averages, price action patterns and volume as signals for upcoming reversals. Specifically, golden crosses and death crosses of moving averages can indicate shifts in trend. Bullish/bearish engulfing patterns usually imply short-term reversals ahead. Surges in trading volume also often signify trend reversals. By combining all three types of signals, the strategy aims to accurately capture reversal turning points.

In terms of logic, the strategy first calculates fast and slow moving averages. Then it defines conditions to identify bullish/bearish engulfing patterns. Support and resistance levels are incorporated along with volume expansion as additional conditions. The buy signals trigger when the fast MA crosses above the slow MA, a bullish pattern appears, resistance breaks, and volume surges. The opposite conditions trigger sell signals.   

## Advantages

The biggest advantage of this strategy is using a combination of multiple signals to confirm reversals, which helps avoid false signals. Relying solely on a single indicator like moving averages or candlestick patterns tends to produce erroneous trades. By requiring alignment of all three factors, the likelihood of accurately capturing reversals improves significantly.

Additionally, this strategy utilizes both trend and reversal concepts. Reversals are only sought after an existing trend. In other words, the strategy only looks for countertrend retracements within trending markets. This helps reduce randomness and boosts profitability.

## Risks 

The biggest risk of this strategy is failed reversals, where the price continues moving against the trade direction after entry signals. This typically happens when the reversal signals turn out to be false, or only short-term corrections within a persisting trend. 

The solutions include adjusting moving average periods to define better trends, using wider stop losses, and incorporating more confirmation factors before trading reversal signals. Adding filters based on higher timeframe trends could also help avoid false breakout trades.

## Enhancements

Possible optimization avenues for this strategy include:

1. Tuning moving average periods to identify optimal long/short term trends. 

2. Testing different support/resistance calculation methods like Pivot Points.

3. Trying other volume indicators like Chaikin Money Flow, Volume Oscillator.

4. Incorporating more reversal confirmation factors like long-term chart patterns, huge volume spikes etc.

5. Using stock index futures to cross-verify signals across markets.

Through rigorous testing of parameter combinations, further improvements in performance can be achieved.

## Conclusion

This strategy neatly combines moving averages, price action and volume to trade reversals only in trending markets. By optimizing the parameters and adding more signal confirmations, it can become a robust system for short-term countertrend trading.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Fast MA Length|
|v_input_2|20|Slow MA Length|
|v_input_3|true|Take Profit (%)|
|v_input_4|true|Stop Loss (%)|
|v_input_5|true|Trailing Stop (%)|
|v_input_6|100|Support Level|
|v_input_7|200|Resistance Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-10 00:00:00
end: 2024-01-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Profit Table Strategy", overlay=true)

// Input parameters
fastLength = input(10, title="Fast MA Length")
slowLength = input(20, title="Slow MA Length")
takeProfitPercent = input(1, title="Take Profit (%)") / 100
stopLossPercent = input(1, title="Stop Loss (%)") / 100
trailingStopPercent = input(1, title="Trailing Stop (%)") / 100

// Price action conditions
bullishEngulfing = close > open and close > open[1] and open < close[1] and open[1] > close[1]
bearishEngulfing = close < open and close < open[1] and open > close[1] and open[1] < close[1]

// Support and resistance levels
supportLevel = input(100, title="Support Level")
resistanceLevel = input(200, title="Resistance Level")

// Volume conditions
volumeCondition = volume > ta.sma(volume, 20)

// Calculate moving averages
fastMA = ta.sma(close, fastLength)
slowMA = ta.sma(close, slowLength)

// Buy condition
buyCondition = (fastMA > slowMA) and (close > resistanceLevel) and bullishEngulfing and volumeCondition

// Sell condition
sellCondition = (fastMA < slowMA) and (close < supportLevel) and bearishEngulfing and volumeCondition

// Strategy logic
strategy.entry("Buy", strategy.long, when=buyCondition)
strategy.close("Buy", when=sellCondition)

// Calculate take profit, stop loss, and trailing stop levels
takeProfitLevel = strategy.position_avg_price * (1 + takeProfitPercent)
stopLossLevel = strategy.position_avg_price * (1 - stopLossPercent)
trailingStopLevel = strategy.position_avg_price * (1 - trailingStopPercent)

// Plotting levels on the chart
plot(supportLevel, color=color.blue, style=plot.style_line, linewidth=2, title="Support Level")
plot(resistanceLevel, color=color.purple, style=plot.style_line, linewidth=2, title="Resistance Level")
plot(takeProfitLevel, color=color.green, style=plot.style_line, linewidth=2, title="Take Profit Level")
plot(stopLossLevel, color=color.red, style=plot.style_line, linewidth=2, title="Stop Loss Level")
plot(trailingStopLevel, color=color.orange, style=plot.style_line, linewidth=2, title="Trailing Stop Level")

// Plotting buy and sell signals on the chart
plotshape(series=buyCondition, title="Buy Signal", color=color.green, style=shape.labelup, location=location.belowbar)
plotshape(series=sellCondition, title="Sell Signal", color=color.red, style=shape.labeldown, location=location.abovebar)

```

> Detail

https://www.fmz.com/strategy/439107

> Last Modified

2024-01-17 17:48:40
