
> Name

Trend-Following-Strategy-Based-on-Dual-EMA
> Author

ChaoZhang

> Strategy Description



[trans]
The name of this strategy is "Trend following strategy based on double EMA". This strategy calculates two EMA moving averages of different periods and determines the market trend direction based on the relationship between the moving averages to perform trend following operations.
Specifically, the trading logic of this strategy is as follows:
1. Calculate the 50-day EMA and the 200-day EMA.
2. When the 50-day EMA crosses the 200-day EMA from below, it means that the market has entered an upward trend, so go long at this time.
3. When the 50-day EMA crosses the 200-day EMA from above, it means that the market has turned into a downward trend, and you can go short at this time.
4. When the trend reverses, close the original position and switch to the new trend direction.
The advantage of this strategy is to use the "golden cross and dead cross" of the EMA moving average to determine the direction of the main trend. However, due to the hysteresis of the moving average itself, parameter settings need to be optimized and combined with stop loss to prevent risks.
Generally speaking, the double EMA moving average strategy is suitable for medium and long-term positioning, and carries out trend following transactions by capturing the main trend turning point in time. However, traders still need to pay attention to more indicators and maintain flexible adjustments to trading strategies.


||



This strategy is named “Trend Following Strategy Based on Dual EMA”. It calculates two EMA lines of different periods and judges trend direction based on their relationship, to follow trends.

Specifically, the trading logic is:

1. Calculate the 50-day EMA and 200-day EMA.  

2. When the 50-day EMA crosses above the 200-day EMA, it signals an uptrend, thus going long.

3. When the 50-day EMA crosses below the 200-day EMA, it flags a downtrend, thus going short. 

4. When trend reversal happens, existing positions are closed and direction is switched to the new trend.

The advantage of this strategy is using EMA “golden cross” and “dead cross” to determine the main trend direction. But EMA lagging requires parameter optimization, plus stop loss to manage risks.

In general, the dual EMA strategy suits mid-to-long term positioning by timely capturing major trend reversals for trend following. But traders still need to watch more indicators and maintain flexibility in strategy adjustment.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-13 00:00:00
end: 2023-09-12 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Sonu1997

//@version=4
//@version=5
strategy('moving average strategy', overlay=true)

ema50 =ema(close, 50)
ema200 =ema(close, 200)



long = ema50 > ema200
short = ema50 < ema200

strategy.entry('long', strategy.long,  0, when=long)
strategy.entry('short', strategy.short,  0, when=short)

strategy.close('long', when=short)
strategy.close('short', when=long)

```

> Detail

https://www.fmz.com/strategy/426625

> Last Modified

2023-09-13 18:04:52
