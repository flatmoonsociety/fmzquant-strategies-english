
> Name

Volatility-Force-Breakthrough-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fe91028c2cc78aaa45.png)

[trans]

## Overview
This strategy is based on moving averages, ATR indicators, and Bollinger Bands to make long and short judgments, and at the same time combines strength indicators to achieve breakthrough transactions. It is a breakthrough strategy.
## Strategy Principle
1. Calculate the middle line, upper line, and lower line in Bollinger Bands. The middle line is the close SMA moving average, and the upper and lower lines are the positive and negative stdDev standard deviation of the middle line.
2. Calculate fast ATR and slow ATR. The fast ATR parameter is 20, and the slow ATR parameter is 50.
3. Calculate the force index XFORCE, which is the accumulation of volume*(close-previous close). Calculate XFORCE's fast EMA and slow EMA.
4. Determine the long signal: fast XFORCE crosses slow XFORCE, and fast ATR>slow ATR, and closing price>opening price.
5. Determine the short signal: fast XFORCE crosses slow XFORCE, and fast ATR > slow ATR, and the closing price < opening price.
6. Go long when the long signal is triggered, and go short when the short signal is triggered.
## Strategic advantage analysis
1. The moving average provides trend judgment, and the Bollinger Bands provide breakthrough buying and selling points.
2. The ATR indicator determines market volatility and enables volatility trading.
3. Strength indicators determine the direction of strength and achieve strength breakthroughs.
4. Multi-index combination provides more comprehensive judgment.
5. The rules are clear and simple, easy to understand and implement.
6. The backtest performance is good and the income is stable.
## Strategy risk analysis
1. If the upper and lower Bollinger Bands are too wide or too narrow, they will produce false signals.
2. The ATR parameters are set improperly and cannot capture market fluctuations.
3. The power indicator has limited effect and cannot determine the true trend reversal.
4. Multi-index combination, parameter adjustment and weight distribution are difficult.
5. It is easy to misjudge the timing of breakthrough signals, and there is a divergence phenomenon.
6. The retracement may be large and can be controlled by stop loss.
## Strategy optimization direction
1. Optimize Bollinger Band parameters to adapt to different cycles and stock characteristics.
2. Optimize ATR parameters to better capture market volatility.
3. Add trend indicators such as MACD to provide trend verification.
4. Add stop loss strategies, such as trailing stop loss to control retracements.
5. Add machine learning algorithms and use AI to determine reversal signals.
6. Combining multiple cycles and comprehensively judging different cycles reduces the misjudgment rate.
## Summarize
This strategy integrates moving average, ATR, Bollinger Bands and power indicators to form a relatively complete breakthrough trading system. Through parameter optimization, the introduction of trend judgment indicators for confirmation, the addition of stop loss strategies, and the addition of AI judgment, the stability of the strategy and the level of income can be further enhanced. However, no strategy can be perfect and needs to be continuously optimized and adjusted based on backtest results to adapt to market changes.
||

## Overview

This strategy uses moving average, ATR, Bollinger Bands for trend judgment and breakout trading, combined with force index for timing, belongs to breakout trading strategy.

## Strategy Logic

1. Calculate middle, upper and lower lines of Bollinger Bands. Middle line is sma of close price, upper and lower are middle line ± stdDev.

2. Calculate fast and slow ATR. Fast ATR has period of 20, slow ATR has period of 50.

3. Calculate force index XFORCE, which is cumulative of volume * (close - previous close). And calculate fast and slow EMA of XFORCE.

4. Judge long signal: fast XFORCE cross above slow XFORCE, and fast ATR > slow ATR, and close > open. 

5. Judge short signal: fast XFORCE cross below slow XFORCE, and fast ATR > slow ATR, and close < open.

6. Go long when long signal triggered, go short when short signal triggered.

## Advantage Analysis

1. Moving average provides trend, Bollinger Bands provides breakout points.

2. ATR judges volatility, implements volatility trading.

3. Force index determines force direction, implements force breakout. 

4. Combination of multiple indicators provides comprehensive judgment.

5. Clear and simple rules, easy to understand and implement.

6. Good backtest results, stable profit.

## Risk Analysis

1. Bollinger Bands may generate wrong signals if width is improper.

2. Wrong ATR parameters cannot catch market volatility.

3. Force index has limited effect, cannot determine real trend reversal.

4. Difficult to adjust parameters and weights for multiple indicators.

5. Breakout signals may be inaccurate, divergence may happen. 

6. Drawdown may be large, can use stop loss to control it.

## Optimization Directions

1. Optimize Bollinger Bands parameters for different periods and instruments.

2. Optimize ATR parameters to better capture volatility.

3. Add trend indicators like MACD for trend validation. 

4. Add stop loss strategies like trailing stop to control drawdown.

5. Utilize AI algorithms to judge reversal signals.

6. Combine multiple timeframes for comprehensive judgment and lower false signals.

## Summary

This strategy integrates moving average, ATR, Bollinger Bands and Force Index to form a complete breakout trading system. Further improvements on parameters optimization, adding trend filter, stop loss strategy and AI algorithms can enhance stability and profitability. But no strategy is perfect, continuous optimizations against backtest results are needed to adapt to changing market conditions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|Fast|
|v_input_2|20|Slow|
|v_input_3|20|ATR Fast|
|v_input_4|50|ATR Slow|
|v_input_5|20|Length|
|v_input_6|2|multiplier|
|v_input_7_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-25 00:00:00
end: 2023-10-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("yuthavithi volatility based force trade scalper strategy", overlay=true)

fast = input(3, minval= 1, title="Fast")
slow = input(20, minval = 1, title = "Slow")
atrFast = input(20, minval = 1, title = "ATR Fast")
atrSlow = input(50, minval = 1, title = "ATR Slow")

len = input(20, minval=1, title="Length")
multiplier = input(2, minval=1, title="multiplier")
src = input(close, title="Source")
bbMid = sma(src, len)
plot(bbMid, color=blue)

atrFastVal = atr(atrFast)
atrSlowVal = atr(atrSlow)
stdOut = stdev(close, len)
bbUpper = bbMid + stdOut * multiplier
bbLower = bbMid - stdOut * multiplier
plot(bbUpper, color = (atrFastVal > atrSlowVal ? red : silver))
plot(bbLower, color = (atrFastVal > atrSlowVal ? red : silver))


force = volume * (close -  nz(close[1]))
xforce = cum(force)
xforceFast = ema(xforce, fast)
xforceSlow = ema(xforce, slow)

bearish = ((xforceFast < xforceSlow) and (atrFastVal > atrSlowVal)) and ((xforceFast[1] > xforceSlow[1]) or (atrFastVal[1] < atrSlowVal[1])) and (close < open)
bullish = ((xforceFast > xforceSlow) and (atrFastVal > atrSlowVal)) and ((xforceFast[1] < xforceSlow[1]) or (atrFastVal[1] < atrSlowVal[1])) and (close > open)


if (bullish)
    strategy.entry("Buy", strategy.long)

if (bearish)
    strategy.entry("Sell", strategy.short)
```

> Detail

https://www.fmz.com/strategy/430261

> Last Modified

2023-10-26 16:17:17
