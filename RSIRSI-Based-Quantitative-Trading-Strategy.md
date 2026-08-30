
> Name

RSI-Based-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/f94365433c1f14e0a74a9eb19da71445e160b39eae06c1ba7b2097224d6f6b2b.png)
[trans]

## Overview
The name of this strategy is "Dual Timeline RSI Reversal", which is a quantitative trading strategy based on the Relative Strength Index (RSI). This strategy uses two different periods of RSI as buy and sell signals to achieve buying low and selling high, and obtain trading opportunities brought about by stock price reversals.
## Strategy Principle
This strategy uses fast period (default 55 days) RSI and slow period (default 126 days) RSI to construct trading signals. A buy signal is generated when the fast period RSI crosses above the slow period RSI, and a sell signal is generated when the fast period RSI crosses below the slow period RSI. In this way, short-term and long-term trend reversal opportunities are discovered by comparing the relative strength of price momentum in two different time intervals.
After entering the signal, the strategy will set take profit and stop loss points. The default take-profit point is 0.9 times the entry price, and the default stop-loss point is 3% of the entry price. At the same time, when the reverse signal reappears, the current position will also be closed.
## Strategic Advantages
- Use double RSI comparison to find the changing points of short-term and long-term price trends and capture reversal opportunities
- Double RSI filters out noise trading caused by false breakthroughs
- Configure take-profit and stop-loss points to limit single losses
## Strategy Risk
- During periods of severe stock price fluctuations, RSI signals may frequently reverse
- The stop loss point is too small, which may cause the loss to be stopped after a small fluctuation.
- Improper setting of double RSI parameters may miss a big reversal trend
## Strategy optimization
- RSI parameters can test more combinations and find the best parameters
- Can be combined with other indicators to filter out false breakout signals
- Dynamically adjust the take-profit and stop-loss ratios to make take-profit more flexible
## Summarize
This strategy "Dual Timeline RSI Reversal" uses the intersection of the two RSIs of the fast cycle and the slow cycle as a trading signal, aiming to capture short-term price reversal opportunities. At the same time, set up stop-profit and stop-loss rules to avoid risks. This is a typical strategy that uses indicators to compare multiple timelines to achieve price reversal trading. The room for optimization lies in parameter adjustment and optimization of risk control rules.
||


## Overview

The strategy is named "Dual Timeframe RSI Reversal". It is a quantitative trading strategy based on Relative Strength Index (RSI). The strategy uses two RSI with different periods to generate buy and sell signals, aiming to buy low and sell high by capturing price reversal opportunities.

## Strategy Logic

The strategy constructs trading signals by comparing a fast period RSI (default 55 days) and a slow period RSI (default 126 days). When the fast RSI crosses above the slow RSI, a buy signal is generated. When the fast RSI falls below the slow RSI, a sell signal is triggered. By comparing the relative strength between two different timeframes, it detects opportunities when short-term and long-term trends reversing.

After entering a position, profit target and stop loss will be set. Default profit target is 0.9 times the entry price. Default stop loss is 3% below the entry price. Positions will also be closed if a reverse signal is triggered.

## Advantages

- Catch short-term price reversals by comparing dual RSIs  
- Filter out false signals using dual confirmation
- Limit loss on single bet with stop loss

## Risks

- Frequent reverse signals during high volatility
- Stop loss too tight, easily knocked out by small fluctuations 
- Miss major reversals with poorly configured parameters

## Enhancement

- Test more RSI parameter combinations to find optimum
- Add other indicators to filter false signals
- Dynamic stop loss and take profit ratio for better profitability

## Summary

The "Dual Timeframe RSI Reversal" strategy generates trading signals by comparing crossovers between fast and slow RSI periods. It aims to capture short-term price reversals. Profit and stop loss rules are set to limit risks. This is a typical strategy of using multi-timeframe indicator comparisons to trade reversals. Enhancement areas include parameter tuning and risk control rules.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|55|Short length|
|v_input_2|126|Long length|
|v_input_3|55|Overbought|
|v_input_4|45|Oversold|
|v_input_5|0.9|Take profit level %|
|v_input_6|3|Stoploss level %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-29 00:00:00
end: 2023-12-05 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title="Relative Strength Index", shorttitle="RSI")
slen    = input(55, title="Short length")
llen    = input(126, title="Long length")
sup     = ema(max(change(close), 0), slen)
sdown   = ema(-min(change(close), 0), slen)
rsi1    = sdown == 0 ? 100 : sup == 0 ? 0 : 100 - (100 / (1 + sup / sdown))
lup     = ema(max(change(close), 0), llen)
ldown   = ema(-min(change(close), 0), llen)
rsi2    = ldown == 0 ? 100 : lup == 0 ? 0 : 100 - (100 / (1 + lup / ldown))
ob      = input(55, title="Overbought")
os      = input(45, title="Oversold")
tp      = input(.9, title="Take profit level %")*.01
sl      = input(3, title="Stoploss level %")*.01
mid     = avg(ob,os)
plot    (mid, color=#4f4f4f, transp=0)
hline   (ob, color=#4f4f4f)
hline   (os, color=#4f4f4f)
long    = crossover(rsi1,rsi2)
short   = crossunder(rsi1,rsi2)
vall    = valuewhen(long,close,0)
lexit1  = high>=(vall*tp)+vall
lexit2  = low<=vall-(vall*sl)
vals    = valuewhen(short,close,0)
sexit1  = low<=vals - (vals*tp)
sexit2  = high>=vals + (vals*sl)
bgcolor (color=long?lime:na,transp=50)
bgcolor (color=short?red:na, transp=50)
strategy.entry("Long", strategy.long, when=long)
strategy.close("Long", when=lexit1)
strategy.close("Long", when=lexit2)
strategy.close("Long", when=short)
strategy.entry("Short", strategy.short, when=short)
strategy.close("Short", when=sexit1)
strategy.close("Short", when=sexit2)
strategy.close("Short", when=long)
plot    (rsi1, color=orange, transp=0,linewidth=1, title="Short period RSI")
plot    (rsi2, color=aqua  , transp=0,linewidth=1, title="Long period RSI")

```

> Detail

https://www.fmz.com/strategy/434480

> Last Modified

2023-12-06 17:17:16
