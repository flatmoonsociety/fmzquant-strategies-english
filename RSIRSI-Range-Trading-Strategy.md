
> Name

RSI range trading strategy RSI-Range-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/997d13893933dace65c472dd168b8c0aac3f758f2744ba8a68657ddaa17743e4.png)
[trans]

## Overview
The RSI range trading strategy profits from price ranges by trading in the opposite direction when the RSI reaches the overbought and oversold range. This strategy is based on the assumption that prices will never rise or fall in one direction forever, and makes profits by capturing the opportunity for a price correction when the RSI reaches overbought or oversold.
## Strategy Principle
This strategy determines whether the price has reached an overbought or oversold range by calculating the RSI indicator. Specifically, the strategy first calculates the length of the RSI indicator as 2 periods. Then set the RSI overbought line to 91 and the oversold line to 11. When the RSI goes above the oversold zone, go short; when the RSI goes below the oversold zone, go long. The position of each transaction is set according to the maximum position proportion parameter, which is currently fixed at 5%.
In order to control risks, the strategy also sets up stop-loss techniques. Specifically, after going long, if the price moves downward by more than 0.5% of the long entry price, the position will be stopped and closed; after going short, if the price moves upward by more than 0.5%, the position will be stopped and closed. This can avoid losses caused by violent unilateral price breakthroughs.
In summary, the core logic of this strategy is: monitor the RSI indicator to determine whether the price is overbought or oversold, conduct reverse trading based on the configured RSI parameters, and set a stop loss to control risks.
## Advantage Analysis
- Use the RSI indicator to determine overbought and oversold, which is a more classic and reliable trading signal.
- Reverse trading of overbought and oversold is in line with the assumption that prices will not always rise or fall unilaterally, and can profit from price range fluctuations.
- Set a stop loss to control losses on a single trade.
- The strategy backtesting framework is simple and clear, easy to understand and modify.
- RSI parameters and stop loss range can be set flexibly to adapt to market changes.
## Risk Analysis
- RSI is a trend indicator, and if there is a sustained price trend rather than a shock, the strategy may generate continuous losses.
- Improper setting of RSI parameters may result in increased trading signals but lower winning rate.
- Improper setting of the stop loss range may cause the stop loss to be triggered by a small price range, or the single loss may be too large.
- This strategy is more suitable for a volatile and rebounding market environment, and may not be effective in a market with significant trends.
- Setting a position that is too large will also lead to larger losses in a single transaction.
## Optimization direction
- You can consider combining other indicators such as MACD and RSI to form a combined signal to improve the accuracy of trading decisions.
- You can study the statistical characteristics of RSI under different parameters and find the best parameter combination.
- You can set up a dynamic adjustment mechanism for position ratio and test its effect in backtesting.
- You can consider using indicators such as ATR to calculate the stop loss range to make the stop loss more adaptable.
- Can combine machine learning and other methods to find the optimal parameter combination.
- You can explore other reversal trading strategies combined with RSI to form a more robust trading system.
## Summarize
The RSI range oscillation trading strategy uses a simple RSI indicator to determine whether the price is overbought or oversold, conduct reverse trading, and set a stop loss to control risk. This strategy is suitable for a volatile and rebounding market environment and makes profits by capturing price fluctuations in the range. However, RSI also has its limitations as a trend indicator, and this strategy may not be suitable for markets with obvious trends. Through parameter optimization, improvement of stop loss rules, and combination with other indicators and strategies, the stability and adaptability of the strategy can be improved. Generally speaking, the RSI range-bound trading strategy has certain reference value, but it needs to be used and optimized in a timely manner in real trading.
|| 

## Overview

The RSI range trading strategy makes profit by trading against the trend when RSI reaches overbought or oversold levels. It is based on the assumption that prices do not trend in one direction forever but oscillate back and forth within a range. This strategy aims to take advantage of the pullbacks when RSI hits extremes.

## Strategy Logic

The strategy calculates the RSI indicator to determine if the price has reached overbought or oversold levels. Specifically, the RSI period is set to 2 bars. The overbought line is 91 and oversold line is 11. A short signal is generated when RSI crosses above the overbought level. A long signal is generated when RSI crosses below the oversold level. The position size is set at 5% of the maximum risk per trade. 

To control risks, a stop loss mechanism is implemented. If the price moves 0.5% against the long position after opening long, the position will be closed. Similarly for the short position. This avoids excessive loss when price trends strongly in one direction.

In summary, the core logic is to monitor RSI for overbought/oversold, trade against the trend based on configured RSI levels, and manage risks via stop loss.

## Advantage Analysis

- RSI is a proven indicator for identifying overbought/oversold levels.

- Trading against extremes fits the assumption of price oscillation instead of one-way trend.

- Stop loss controls loss for individual trades.

- Simple and clear backtesting framework, easy to understand and modify.

- Flexible RSI parameters and stop loss level adaptable to changing market.

## Risk Analysis

- RSI is a trend following indicator, continuous losses may occur during persistent trend instead of range-bound price.

- Improper RSI parameters may generate more signals but with lower win rate. 

- Stop loss may get triggered by small moves or cause large losses if not set properly.

- The strategy works better in range-bound market, may underperform in strong trending scenarios.

- Excessive position size can magnify losses.

## Optimization Directions

- Combine RSI with other indicators like MACD to improve signal accuracy.

- Research statistical RSI behaviors with different parameters to find optimal settings.

- Test dynamic position sizing mechanisms in backtests.

- Use ATR to set adaptive stop loss levels.

- Apply machine learning to discover optimal parameter combinations. 

- Explore combining other mean-reversion strategies with RSI to build robust systems.

## Summary

The RSI range trading strategy makes simple reversal trades based on RSI overbought/oversold levels and manages risk via stop loss. It works for range-bound oscillating markets but has limitations in strong trending scenarios. Fine-tuning parameters, improving stop loss rules, combining with other indicators and strategies can enhance its stability and adaptability. Overall this strategy provides some valuable insights but needs prudent application and optimization in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|rsi Length|
|v_input_2|11|What rsi level triggers a long|
|v_input_3|91|What rsi level triggers a short|
|v_input_4|0.05|Maximum risk/ trade|
|v_input_5|0.005|Max Movment in the opposite direction / trade|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-30 00:00:00
end: 2023-11-05 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Simple RSI Strategy", overlay=true)

var rsiLength = input(2, title = "rsi Length")
var float rsiBuyLevel = input(11, title = "What rsi level triggers a long")
var float rsiShortLevel = input(91, title = "What rsi level triggers a short")
var float maxRisk =  input(.05, title="Maximum risk/ trade")
var chartEntryStop = input(.005, title="Max Movment in the opposite direction / trade")
var float longEntryPrice = na
var float shortEntryPrice = na 
rsiValue = ta.rsi(close, rsiLength)

var float maxRiskValue = (strategy.equity * maxRisk) / chartEntryStop
var float maxRsi = 0

//Conditions


// Strategy Execution
if( close <= longEntryPrice-(longEntryPrice*chartEntryStop ))
    strategy.close("Long")

if( close >= shortEntryPrice+(shortEntryPrice*chartEntryStop ))
    strategy.close("Short")

if (rsiValue <= rsiBuyLevel and maxRsi == rsiShortLevel)
    maxRsi := rsiBuyLevel 
    strategy.close("Short")
    strategy.entry("Long", strategy.long)
    longEntryPrice := close
    
   
else if (rsiValue >= rsiShortLevel and maxRsi == rsiBuyLevel)
    maxRsi := rsiShortLevel
    strategy.close("Long")
    strategy.entry("Short", strategy.short)
    shortEntryPrice := close

else if (rsiValue >= rsiShortLevel )
    maxRsi := rsiShortLevel
    strategy.close("Long")

else if (rsiValue <= rsiBuyLevel )
    maxRsi := rsiBuyLevel
    strategy.close("Short")
```

> Detail

https://www.fmz.com/strategy/431274

> Last Modified

2023-11-06 16:12:23
