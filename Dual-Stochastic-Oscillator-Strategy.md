
> Name

Dual-Stochastic-Oscillator-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses two sets of stochastic indicators with different parameter settings to realize long and short condition judgments, and is a typical moving average crossover system. Use fast indicators to determine short-term trends and entry opportunities, and slow indicators to determine the direction of the general trend. The two are combined to form trading signals.
## Strategy Principle
1. The K value of the fast stochastic indicator indicates the short-term trend direction. The K line crosses its moving average SM1 to form an entry signal.
2. The K value of the slow stochastic indicator reflects the general trend. When the fast indicator shows a reversal signal, look at the slow indicator to determine the rationality of the general direction.
3. When K quickly crosses SM1, it is regarded as a bullish signal; when the slow K is greater than 50, it means that the general trend is upward and the long conditions are met.
4. When K quickly crosses SM1, it is regarded as a bearish signal; when the slow K is less than 50, it means that the general trend is downward, and short selling conditions are met.
5. Set take profit and stop loss points, and take profit and stop loss at a fixed ratio.
## Advantage Analysis
1. Double random indicators filter noise and improve the success rate. Use speed and slowness to reduce the risk of being trapped.
2. The SM1 parameter is small and the K indicator is sensitive, suitable for capturing short-term opportunities.
3. Large cycles determine the general trend, and small cycles capture reversals. The long-short strategy is consistent with most market conditions.
4. Fixed take-profit and stop-loss points, controllable risk and return, and not prone to excessive fluctuations.
## Risk Analysis
1. When there is a divergence between indicators, trading opportunities will be missed or false signals will be generated.
2. Fixed take-profit and stop-loss points are not flexible enough and cannot be adjusted according to market changes.
3. The lbl indicator parameters need to be optimized and tested repeatedly. If they are not appropriate, they will become invalid.
4. Short-cycle transactions require higher transaction frequency, which increases transaction costs.
## Optimization direction
1. Add other indicators or filtering conditions to ensure the quality of indicator signals.
2. Test different parameter combinations to find the best parameter configuration.
3. Combined with volatility indicators, etc., the stop-profit and stop-loss levels can be dynamically adjusted.
4. Use time period filtering to avoid key events and control irrational fluctuations.
5. Optimize the fund management strategy, add or reduce positions at the right time, and improve the efficiency of fund use.
## Summarize
This strategy integrates fast and slow stochastic indicators to form a long and short trading system. However, parameter settings need to be further optimized, and indicators such as trends and volatility need to be used as filtering conditions. Under strict risk control, this strategy can obtain relatively stable excess returns.
|| 

## Overview

This strategy uses two stochastic oscillators with different parameters to determine bull/bear conditions. It is a typical moving average crossover system. The faster oscillator judges short-term trends and entry signals, while the slower one confirms overall trend direction. Signals are generated from the combination.

## Strategy Logic

1. Fast %K shows short-term trend direction. %K crossing over the smoothing line SM1 generates entry signals.

2. Slow %K reflects overall trend conditions. When fast oscillator gives reversal signal, check slow oscillator for trend validity.

3. %K fast crossover above SM1 indicates bullish signal. Slow %K above 50 means uptrend, satisfying long condition.

4. %K fast crossover below SM1 indicates bearish signal. Slow %K below 50 means downtrend, satisfying short condition. 

5. Set take profit and stop loss points at fixed percentages.

## Advantage Analysis

1. Dual stochastic filters noise and improves accuracy. Fast and slow combination reduces being trapped risks.

2. Smaller SM1 parameter makes %K sensitive for catching short-term opportunities.

3. Larger cycle judges overall trend, smaller cycle captures reversals. Dual long/short strategies fit most market environments.

4. Fixed profit taking and stop loss points make risk controllable without huge swings.

## Risk Analysis

1. Divergence between indicators can cause missed trades or wrong signals.

2. Fixed profit taking and stop loss points lack flexibility in adjusting to markets.

3. Stochastic parameters need repetitive optimization, improper settings lead to failure.

4. High trading frequency from short-term trading increases transaction costs.

## Optimization Directions

1. Add other indicators or filters to ensure signal quality.

2. Test different parameter combinations to find optimal settings.

3. Incorporate volatility measures to make profit taking and stop loss levels dynamic.

4. Use time filters to avoid key events and irrational price swings.  

5. Optimize capital management strategies like position sizing to improve capital efficiency.

## Summary

This strategy integrates fast and slow stochastic oscillators into a dual directional system. Further parameter optimization and adding filters like trend and volatility indicators can improve it. With proper risk control, this strategy can achieve relatively steady excess returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Leading K|
|v_input_2|2|Leading Smooth |
|v_input_3|97|Lagging K|
|v_input_4|3|Lagging D|
|v_input_5|true|Lagging Smooth|
|v_input_6|1.2|v_input_6|
|v_input_7|1.2|v_input_7|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-17 00:00:00
end: 2023-09-16 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Double Stochastic", overlay=true)

//-----------------------Stochastics------------------------//

c= security(syminfo.tickerid,timeframe.period , close)  
h= security(syminfo.tickerid, timeframe.period, high)  
l= security(syminfo.tickerid, timeframe.period, low)  

c1= security(syminfo.tickerid, timeframe.period, close)  
h2= security(syminfo.tickerid, timeframe.period, high)  
l1= security(syminfo.tickerid, timeframe.period, low)  

K1 = input(5, title="K", minval=1, title="Leading K")
SM1 = input(2, title="Smooth", minval=1, title="Leading Smooth ")
k = ema(stoch(c, h, l, K1), SM1)

K2 = input(97, title="K", minval=1, title="Lagging K")
D2 = input(3, title="D", minval=1, title="Lagging D")
SM2 = input(1, title="Smooth", minval=1, title="Lagging Smooth")
k1 = ema(stoch(c1, h2, l1, K2), SM2)

// buy ((k[2] < 40 and k > 40) and bars_up > 0 and k1 > 50) 
// sell (k[2] > 60 and k < 60) and bars_down > 0 and k1 < 50

//-----------------------Mechanics------------------------//

buy = k1 > 50 and k < 30 and k > k[1] ? 1 : 0
sell = k1 < 50 and k > 70 and k < k[1] ? 1 : 0

buy_val = valuewhen(buy == 1, close, 1)
sell_val = valuewhen(sell == 1, close, 1)

buy_close = buy_val * input(1.20, minval=0.1)
sell_close = sell_val / input(1.20, minval=0.1)

//------------------------Buy/Sell-------------------------//

longCondition = buy == 1
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

close_long = close >= buy_close
if (close_long)
    strategy.close("My Long Entry Id")
    
sellCondition = sell == 1
if (sellCondition)
    strategy.entry("My Short Entry Id", strategy.short)

close_short = close <= sell_close
if (close_short)
    strategy.close("My Short Entry Id")    
```

> Detail

https://www.fmz.com/strategy/427065

> Last Modified

2023-09-17 18:26:16
