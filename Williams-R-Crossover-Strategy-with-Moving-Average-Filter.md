
> Name

Williams-R-Crossover-Strategy-with-Moving-Average-Filter trading strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the William indicator crossover signal and filters with the moving average to achieve a more flexible short-term trading strategy. This strategy can capture clearer overbought and oversold conditions, while moving average filtering can avoid being affected by market shocks, thus having higher stability.
## Strategy Principle
1. Calculate the William indicator (%R) and the 200-period simple moving average.
2. When the William indicator breaks through the -50 line upwards and reaches the set threshold, and the closing price is higher than the moving average, go long.
3. When the William indicator falls below the -50 line and reaches the set threshold, and the closing price is lower than the moving average, go short.
4. After going long, close the position if the closing price reaches the take-profit level (entry price plus take-profit points) or the stop-loss level (entry price minus stop-loss points).
5. After shorting, if the closing price reaches the take-profit level (entry price minus take-profit points) or the stop-loss level (entry price plus stop-loss points), the position will be closed.
This strategy makes full use of the overbought and oversold characteristics of the William indicator, combined with the trend judgment of the moving average, to make the trading signals clearer and more reliable. The stop-profit and stop-loss strategy is also relatively clear and concise, and overall it is a relatively complete short-term strategy system.
## Strategic advantage analysis
1. The William indicator can effectively identify overbought and oversold conditions, and the signal is relatively clear.
2. Moving average filtering increases the judgment of trends and avoids being affected by shocks.
3. Indicator parameters and filters are customizable and can be flexibly adjusted.
4. Use trend following stop loss method to lock in most of the profits.
5. The strategy signal rules are simple and clear, easy to understand and implement, and are suitable for short-term trading.
6. Can be applied to a variety of varieties and is flexible and versatile.
## Risk Analysis
1. There is a lag in the William indicator and some opportunities may be missed.
2. The moving average as a filter also has a lag problem.
3. Strict judgment of overbought and oversold may miss some trend opportunities.
4. If the stop loss is too small, the loss may be stopped due to price fluctuations.
5. Stop loss that is too large may limit profits.
6. Parameters need to be adjusted to suit different market environments.
## Strategy optimization direction
1. Optimize indicator parameters and improve strategy winning rate.
2. Add other indicators for filtering, such as MACD, KDJ, etc.
3. Try different types of moving averages, such as exponential moving averages.
4. Increase trend judgment and only trade in the direction of the trend.
5. Optimize stop-profit and stop-loss strategies, such as dynamic stop-loss, shrinking stop-loss, etc.
6. Try to add position management, such as fixed positions, martingale, etc.
7. Use machine learning to find better parameter combinations.
## Summarize
This strategy integrates the overbought and oversold judgment of the William indicator and the trend filtering of the moving average to form a simple and practical short-term strategy. It has clear trading signals and take-profit and stop-loss rules. Through improvements in parameter optimization, indicator optimization, stop loss management, etc., the strategy can be made more stable and realistic. This strategy is easy to implement and expand, and is very suitable for short-term traders.
|| 

## Overview

This strategy utilizes the Williams %R crossover signals and adds a moving average filter to create a flexible short-term trading system. It can capture overbought and oversold situations clearly, while the MA filter avoids market noise for higher stability.

## Strategy Logic

1. Calculate Williams %R and 200-period simple moving average (MA).

2. Go long when %R crosses above -50 level by a threshold and close is above MA. 

3. Go short when %R crosses below -50 level by a threshold and close is below MA.

4. If long, close position when close reaches take profit (entry price + take profit pips) or stop loss level (entry price - stop loss pips).

5. If short, close position when close reaches take profit (entry price - take profit pips) or stop loss level (entry price + stop loss pips).

The strategy capitalizes on the overbought/oversold nature of Williams %R, and combines MA trend filter for more reliable signals. The stop loss/take profit logic is simple and clear. Overall it is a complete short-term system.

## Advantage Analysis

1. Williams %R effectively identifies overbought/oversold levels with clear signals.

2. MA filter adds trend bias to avoid whipsaws.

3. Customizable parameters for flexibility.

4. Trailing stop loss locks in most profits.

5. Simple clear logic, easy to understand and implement. Good for short-term trading.

6. Applicable to multiple products with flexibility.

## Risk Analysis 

1. Williams %R has lagging effect, may miss some opportunities.

2. MA filter also has some lag.

3. Strict overbought/oversold rules may miss some trends. 

4. Stop loss too tight may be stopped out by whipsaws.

5. Stop loss too wide may limit profits.

6. Parameters need tuning for different market environments.

## Optimization Directions

1. Optimize parameters for higher win rate.

2. Add other filters like MACD, KDJ etc.

3. Try different MA types like exponential MA. 

4. Add trend bias, only trade in trend direction.

5. Optimize stop loss strategies like dynamic stops, chandelier exits etc.

6. Try position sizing like fixed fractional, Martingale etc.

7. Utilize machine learning for better parameter optimization.

## Conclusion

This strategy combines Williams %R overbought/oversold signals with MA trend filter into a simple short-term system. It has clear entry signals and stop loss/take profit logic. Further improvements can be made through parameter tuning, indicator selection, stop loss management etc for more robustness. Easy to implement and expand on, this strategy is well suited for short-term traders.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Williams %R Length|
|v_input_2|10|Cross Threshold (Pips)|
|v_input_3|30|Take Profit (Pips)|
|v_input_4|20|Stop Loss (Pips)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Williams %R Cross Strategy with MA Filter", overlay=true)

// User Inputs
wrLength = input(14, title="Williams %R Length")
crossPips = input(10, title="Cross Threshold (Pips)")
takeProfitPips = input(30, title="Take Profit (Pips)")
stopLossPips = input(20, title="Stop Loss (Pips)")

// Calculate Williams %R
wrHigh = ta.highest(high, wrLength)
wrLow = ta.lowest(low, wrLength)
wr = (wrHigh - close) / (wrHigh - wrLow) * -100

// Calculate 200-period Simple Moving Average
ma200 = ta.sma(close, 200)

// Entry Conditions
enterLong = ta.crossover(wr, -50 - crossPips) and close > ma200
enterShort = ta.crossunder(wr, -50 + crossPips) and close < ma200

// Exit Conditions
exitLong = close >= (strategy.position_avg_price + (takeProfitPips / syminfo.mintick)) or close <= (strategy.position_avg_price - (stopLossPips / syminfo.mintick))
exitShort = close <= (strategy.position_avg_price - (takeProfitPips / syminfo.mintick)) or close >= (strategy.position_avg_price + (stopLossPips / syminfo.mintick))

// Order Management
if enterLong
    strategy.entry("Long", strategy.long)
    
if enterShort
    strategy.entry("Short", strategy.short)

if exitLong
    strategy.close("Long")

if exitShort
    strategy.close("Short")

```

> Detail

https://www.fmz.com/strategy/427310

> Last Modified

2023-09-19 21:57:46
