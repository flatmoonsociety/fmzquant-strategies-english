
> Name

Based on the Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12e20feb1ef9f3ae8e6.png)
[trans]

## Strategy Overview
The double moving average crossover strategy is a classic trend following strategy. This strategy uses two moving averages of different periods to capture market trends. When the fast moving average crosses the slow moving average, a long signal is generated, and when the fast moving average crosses below the slow moving average, a short signal is generated. The core idea of ​​this strategy is that the fast moving average is more sensitive to price changes and can respond faster to changes in market trends, while the slow moving average reflects the long-term trend of the market. Through the intersection of two moving averages, the change in market trend can be judged and transactions can be carried out.
## Strategy Principle
Two moving averages are used in this strategy code, one is a fast moving average (default is 14 periods), and the other is a slow moving average (default is 28 periods). The moving average types can be selected from simple moving average (SMA), exponential moving average (EMA), weighted moving average (WMA) and relative moving average (RMA).
The main logic of the strategy is as follows:
1. Calculate the values of fast moving average and slow moving average
2. If the fast moving average crosses the slow moving average, a long signal will be generated and a long position will be opened.
3. If the fast moving average crosses the slow moving average and shorting is allowed (allowShorting=true), a shorting signal will be generated and a short position will be opened.
4. If the fast moving average crosses the slow moving average and shorting is not allowed (allowShorting=false), close the long position
Through this logic, the strategy can track the main trend of the market, hold long positions in the upward trend, hold short positions in the downward trend or wait for the short position. The moving average period and type can be adjusted and optimized according to different markets and trading varieties.
## Strategic Advantages
1. The logic is simple and clear, easy to understand and implement
2. It is suitable for trending markets and can effectively capture the mid- to long-term trends of the market.
3. Adjustable parameters, suitable for different markets and trading varieties
4. You can flexibly choose whether to allow short selling based on market characteristics and personal preferences.
5. Moving average is a classic technical analysis indicator and is widely used and verified.
## Strategy Risk
1. In a volatile market, frequent moving average crossovers may lead to frequent transactions and increase transaction costs.
2. Choosing a fast moving average that is too short or a slow moving average that is too long may cause signals to lag and miss the best trading opportunities.
3. The strategy may suffer continuous losses when the market trend changes.
4. Fixed moving average cycle parameters may not adapt to dynamic changes in the market
To address these risks, the following measures can be taken:
1. According to market characteristics, optimize the moving average cycle parameters and select the appropriate fast and slow moving average lengths
2. In a volatile market, you can consider adding filtering conditions, such as ATR filtering, or moving average cross angle filtering, etc.
3. Set stop loss and profit appropriately to control the risk of a single transaction
4. Regular backtest evaluation and adjust strategy parameters according to market changes
## Strategy optimization
1. Introduce more technical indicators, such as MACD, RSI, etc., to build multi-factor strategies and improve signal accuracy
2. Optimize position management, such as dynamically adjusting position size considering factors such as ATR or volatility.
3. For volatile markets, you can consider introducing trend judgment indicators, such as ADX, etc. to avoid frequent transactions.
4. Use machine learning or optimization algorithms to automatically find the optimal parameter combination
These optimizations can improve the adaptability and stability of the strategy and better adapt to different market conditions. But at the same time, we should also note that over-optimization may lead to over-fitting of the strategy and poor performance in real trading. Further validation in out-of-sample data is needed.
## Summarize
The double moving average crossover strategy is a classic trend following strategy that generates trading signals through the intersection of two moving averages with different periods. Its logic is simple, easy to implement, and suitable for trending markets. However, in a volatile market, frequent transactions and continuous losses may occur. Therefore, when using this strategy, it is necessary to optimize the moving average cycle parameters according to market characteristics and set stop loss and profit reasonably. In addition, the adaptability and stability of the strategy can be improved by introducing more technical indicators, optimizing position management, trend judgment, etc. However, over-optimization may lead to over-fitting and needs to be treated with caution. In general, the double moving average crossover strategy is a classic strategy worth learning and researching. Through continuous optimization and improvement, it can become an effective trading tool.
|| 

## Strategy Overview

The Dual Moving Average Crossover Strategy is a classic trend-following strategy. This strategy uses two moving averages with different periods to capture market trends. When the fast moving average crosses above the slow moving average, it generates a long signal. When the fast moving average crosses below the slow moving average, it generates a short signal. The core idea of this strategy is that the fast moving average is more sensitive to price changes and can react more quickly to changes in market trends, while the slow moving average reflects the long-term trend of the market. By analyzing the crossover of the two moving averages, we can determine the turning point of the market trend and make trades accordingly.

## Strategy Principle

In this strategy code, two moving averages are used: a fast moving average (default 14 periods) and a slow moving average (default 28 periods). The type of moving average can be selected from Simple Moving Average (SMA), Exponential Moving Average (EMA), Weighted Moving Average (WMA), and Relative Moving Average (RMA).

The main logic of the strategy is as follows:

1. Calculate the values of the fast moving average and the slow moving average
2. If the fast moving average crosses above the slow moving average, it generates a long signal and opens a long position
3. If the fast moving average crosses below the slow moving average and shorting is allowed (allowShorting=true), it generates a short signal and opens a short position
4. If the fast moving average crosses below the slow moving average and shorting is not allowed (allowShorting=false), it closes the long position

Through this logic, the strategy can track the main trend of the market, holding long positions in an uptrend and short positions or no positions in a downtrend. The moving average period and type can be adjusted and optimized according to different markets and trading instruments.

## Strategy Advantages

1. Simple and clear logic, easy to understand and implement
2. Suitable for trending markets, can effectively capture medium and long-term market trends
3. Adjustable parameters, suitable for different markets and trading instruments 
4. Can flexibly choose whether to allow shorting based on market characteristics and personal preferences
5. Moving averages are classic technical analysis indicators that are widely used and validated

## Strategy Risks

1. In range-bound markets, frequent moving average crossovers may lead to frequent trading and increase transaction costs
2. If the fast moving average is chosen too short or the slow moving average is chosen too long, it may cause signal lag and miss the best trading opportunities
3. When the market trend reverses, the strategy may experience consecutive losses
4. Fixed moving average period parameters may not adapt to dynamic changes in the market

To address these risks, the following measures can be taken:

1. Optimize moving average period parameters based on market characteristics and choose appropriate lengths for fast and slow moving averages
2. In range-bound markets, consider adding filtering conditions such as ATR filtering or moving average crossover angle filtering
3. Set reasonable stop-loss and take-profit levels to control single trade risk
4. Conduct regular backtesting and evaluation, and adjust strategy parameters according to market changes

## Strategy Optimization

1. Introduce more technical indicators such as MACD and RSI to build a multi-factor strategy and improve signal accuracy
2. Optimize position management, such as considering factors like ATR or volatility to dynamically adjust position sizes
3. For range-bound markets, consider introducing trend determination indicators such as ADX to avoid frequent trading
4. Use machine learning or optimization algorithms to automatically find the optimal parameter combination

These optimizations can improve the adaptability and stability of the strategy to better adapt to different market conditions. However, it should also be noted that over-optimization may lead to overfitting of the strategy and poor performance in live trading. Further validation on out-of-sample data is needed.

## Summary

The Dual Moving Average Crossover Strategy is a classic trend-following strategy that generates trading signals through the crossover of two moving averages with different periods. It has simple logic, is easy to implement, and is suitable for trending markets. However, in range-bound markets, it may experience frequent trading and consecutive losses. Therefore, when using this strategy, it is necessary to optimize the moving average period parameters based on market characteristics and set reasonable stop-loss and take-profit levels. In addition, the adaptability and stability of the strategy can be improved by introducing more technical indicators, optimizing position management, trend determination, etc. However, over-optimization may lead to overfitting and should be treated with caution. Overall, the Dual Moving Average Crossover Strategy is a classic strategy worth learning and researching. Through continuous optimization and improvement, it can become an effective trading tool.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|true|Allow Shorting|
|v_input_int_1|14|Fast MA Length|
|v_input_int_2|28|Slow MA Length|
|v_input_string_1|Simple|Fast MA Type|
|v_input_string_2|Simple|Fast MA Type|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-09 00:00:00
end: 2024-03-10 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © z4011

//@version=5
strategy("#2idagos", overlay=true, margin_long=100, margin_short=100)
allowShorting = input.bool(true, "Allow Shorting")
fastMALength = input.int(14, "Fast MA Length")
slowMALength = input.int(28, "Slow MA Length")
fastMAType = input.string("Simple", "Fast MA Type", ["Simple", "Exponential", "Weighted", "Relative"])
slowMAType = input.string("Simple", "Fast MA Type", ["Simple", "Exponential", "Weighted", "Relative"]) 

float fastMA = switch fastMAType
    "Simple" => ta.sma(close, fastMALength)
    "Exponential" => ta.ema(close, fastMALength)
    "Weighted" => ta.wma(close, fastMALength)
    "Relative" => ta.rma(close, fastMALength)

plot(fastMA, color = color.aqua, linewidth = 2)

float slowMA = switch slowMAType
    "Simple" => ta.sma(close, slowMALength)
    "Exponential" => ta.ema(close, slowMALength)
    "Weighted" => ta.wma(close, slowMALength)
    "Relative" => ta.rma(close, slowMALength)

plot(slowMA, color = color.blue, linewidth = 2)


longCondition = ta.crossover(fastMA, slowMA)
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = ta.crossunder(fastMA, slowMA) and allowShorting
if (shortCondition)
    strategy.entry("Short", strategy.short)

closeCondition = ta.crossunder(fastMA, slowMA) and not allowShorting
if (closeCondition)
    strategy.close("Long", "Close")

```

> Detail

https://www.fmz.com/strategy/444363

> Last Modified

2024-03-11 12:06:22
