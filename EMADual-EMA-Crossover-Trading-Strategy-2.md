
> Name

Dual-EMA-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The double EMA span trading strategy is a trend following strategy, which determines the market trend and conducts transactions by calculating the span ratio of two EMAs of different periods. This strategy is relatively simple and direct, can effectively track medium and long-term trends, and is very suitable for medium- and long-term trend traders.
## Strategy Principle
This strategy is mainly based on the numerical size of two EMAs and the span between them to determine the trend direction. The strategy first calculates a short-term EMA and a long-term EMA. Typical configurations are 13-period and 26-period EMA. Then calculate the span percentage between the two EMAs. If the short-term EMA is higher than the long-term EMA, and the span is greater than the set threshold (such as 5%), it is judged that the trend is upward, and a long transaction is performed; if the short-term EMA is lower than the long-term EMA, and the span is greater than the set threshold, the trend is judged to be downward, and a short transaction is performed. When the price falls below or breaks through the short-term EMA again, close the position.
The core logic of this strategy is:
1. Calculate short-term EMA and long-term EMA
2. Determine whether the short-term EMA is higher or lower than the long-term EMA
3. Calculate whether the span percentage between two EMAs is higher than the set threshold
4. Determine the direction according to the trend, go long or short
5. Close the position when the price falls below or breaks through the short-term EMA again
Through such a design, mid- and long-term trends can be effectively tracked and the direction can be switched in time when the trend changes. At the same time, the setting of span threshold can also avoid unnecessary transactions caused by adjustments in non-critical periods.
## Strategic Advantages
- This strategy is direct and effective, very suitable for medium and long-term trend tracking
- Using EMA helps filter out short-term market noise
- Configurable EMA period and span thresholds, highly adaptable
- Use span calculations to ensure you only trade when the trend is clear
- Combined with breaking the short-term EMA to stop loss, the risk can be controlled
## Strategic risks and countermeasures
- Unable to exit before the trend reverses, and need to bear a larger retracement
- Easy to get caught in the shock and consolidation
- The EMA cycle and span thresholds need to be reasonably configured according to specific varieties.
Risks can be reduced by:
1. Combine with other indicators to judge trend reversal signals and close positions in advance
2. Add trend filter conditions to avoid trading in volatile market conditions
3. Optimize parameter configuration and select the EMA period and span threshold suitable for specific varieties.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Parameter optimization: Optimize EMA cycle parameters and span thresholds through backtesting to find the best parameter combination
2. Trend filtering: Add other indicators to identify trends, such as MACD, Bollinger Bands, etc., to avoid being stuck in volatile market conditions
3. Stop loss strategy: Set up trailing stop loss or time stop loss to control single loss
4. Profit-taking: Set a partial profit and then move the take-profit point to lock in part of the profit
5. Quantitative optimization: Use machine learning and other methods to automatically optimize parameters and filtering conditions to achieve quantitative optimization of strategies
6. Combination optimization: Combine this strategy with other non-correlated strategies to reduce drawdowns and improve stability
Through the optimization of parameters, filtering conditions, stop loss, profit taking and other aspects, the strategy can be made more stable, adaptable to more market conditions, more scientific and effective. Quantitative and portfolio optimization can also significantly improve the effectiveness of strategies.
## Summarize
The double EMA span strategy is a simple and straightforward strategy suitable for trend following. It only needs two EMAs to determine the trend direction, which is very suitable for medium and long-term positions. At the same time, it can be improved through parameter optimization, trend filtering, stop-loss strategies and other methods to make the strategy more stable and reliable. This strategy is easy to implement and quantitatively optimized. It is a recommended trend following strategy.
|| 


## Overview

The dual EMA crossover trading strategy is a trend following strategy that uses the crossover of two EMAs of different lengths to determine market trend and make trades. This simple and straightforward strategy can effectively track medium- to long-term trends, making it very suitable for swing traders.

## Strategy Logic

The strategy mainly uses the values and crossover of a short-term and long-term EMA to determine trend direction. It first calculates a short-term EMA (e.g. 13 periods) and a long-term EMA (e.g. 26 periods), then computes the percentage crossover between the two EMAs. If the short EMA is above the long EMA and the crossover is larger than a threshold (e.g. 5%), it signals an upward trend and long trades are taken. If the short EMA is below the long EMA and the crossover is larger than the threshold, it signals a downward trend and short trades are taken. Trades are closed when price crosses back above or below the short EMA. 

The key logic is:

1. Calculate short-term and long-term EMAs
2. Check if short EMA is above or below long EMA 
3. Compute percentage crossover between the two EMAs
4. Determine trend direction for long or short trades
5. Close trades when price crosses back the short EMA

This allows the strategy to effectively track medium- to long-term trends and switch direction when the trend changes. The crossover threshold also avoids unnecessary trades during non-trending periods.

## Advantages

- Simple and effective for tracking long-term trends
- EMAs help filter out short-term market noise
- Configurable EMA periods and crossover threshold for flexibility
- Crossover threshold ensures trades only when trend is strong
- Short EMA breakout for stop loss helps manage risk

## Risks and Mitigations

- Unable to exit before trend reversal, larger drawdowns
- Can get whipsawed during range-bound price action
- Need to set suitable EMA periods and threshold per instrument  

Risks can be reduced by:

1. Adding filters to identify trend reversal signals for early exits
2. Increasing trend filter rules to avoid trading range-bound action
3. Optimizing EMA periods and threshold for each instrument

## Enhancement Opportunities

The strategy can be enhanced in areas like:

1. Parameter optimization via backtesting to find optimal EMA periods and threshold

2. Trend filtering using additional indicators like MACD, Bollinger Bands to avoid whipsaws

3. Stop loss strategies like trailing stops or time-based stops to limit losses

4. Profit taking by moving stop loss to lock in partial profits after hits

5. Quantitative optimization using machine learning to auto-tune parameters and filters

6. Portfolio optimization by combining with non-correlated strategies to lower drawdown and increase robustness

Through parameter optimization, better filters, stop loss, profit taking, and quantitative & portfolio optimization, the strategy can be made more robust, adaptive, and scientifically effective.

## Conclusion

The dual EMA crossover is a simple and direct trend following strategy suitable for swing trading. It only requires two EMAs to determine trend direction, ideal for medium- to long-term trend trading. The strategy can also be enhanced through parameter tuning, better filters, stop loss, and other quantitative optimizations to make it more robust. Easy to implement and optimize, it is a recommended trend trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.95|diffMinimum|
|v_input_2|13|Small EMA|
|v_input_3|26|Long EMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-08-23 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("2-EMA Strategy", overlay=true, initial_capital=100, currency="USD", default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.075)

diffMinimum = input(0.95, step=0.01)

small_ema = input(13, title="Small EMA")
long_ema = input(26, title="Long EMA")

ema1 = ema(close, small_ema)
ema2 = ema(close, long_ema)


orderCondition = ema1 > ema2?((ema1/ema2)*100)-100 > diffMinimum:((ema2/ema1)*100)-100 > diffMinimum

longCondition = close > ema1 and ema1 > ema2
if (longCondition and orderCondition)
    strategy.entry("Long", strategy.long)

shortCondition = close < ema1 and ema1 < ema2
if (shortCondition and orderCondition)
    strategy.entry("Short", strategy.short)
    
strategy.close("Short", when=close > ema1)
strategy.close("Long", when=close < ema1)
    
plot(ema(close, small_ema), title="EMA 1", color=green, transp=0, linewidth=2)
plot(ema(close, long_ema), title="EMA 2", color=orange, transp=0, linewidth=2)
```

> Detail

https://www.fmz.com/strategy/427290

> Last Modified

2023-09-19 19:36:03
