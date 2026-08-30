
> Name

Smooth-Volatility-Band-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14acc3eb3c3ec846c56.png)
[trans]
## Overview
This strategy generates a price target band based on the smoothed volatility of the price. When the price breaks through the target band, a trading signal is generated.
## Strategy Principle
This strategy first calculates the average price fluctuation range within a certain period, and then smoothes the fluctuation range through an exponential moving average to generate smoothed volatility. The range of the target band is obtained by multiplying the smoothed volatility by a coefficient. When the price breaks through the upper band of the target band, a buy signal is generated; when the price breaks through the lower band of the target band, a sell signal is generated.
Specifically, in the strategy, the smoothed volatility smrng is calculated through the smoothrng function, and then the upper and lower rails hband and lband of the target band are calculated based on the smrng value. On this basis, set the long condition longCondition and the short condition shortCondition. When the long position conditions are met, a buy signal is generated; when the short position conditions are met, a sell signal is generated.
## Advantage Analysis
This strategy has the following advantages:
1. Use price volatility to construct trading signals, which can effectively track market changes.
2. Smoothing volatility through exponential moving averages can filter noise and generate more reliable trading signals.
3. The target band range can be adjusted through the volatility coefficient, making the strategy more flexible.
4. Combined with price breakthrough judgment, trading opportunities can be captured in time when the trend turns.
## Risk Analysis
There are also some risks with this strategy:
1. When the market experiences abnormal fluctuations, the smoothed volatility may not accurately reflect the true fluctuations, resulting in false signals. The model can be optimized by adjusting parameters.
2. If the target band range is set improperly, it may lead to excessive trading frequency or insufficient signals. Different parameters can be tested to find the optimal range.
3. There is a time lag in the judgment of breakthrough signals, which may lead to early or late entry. Can be combined with other indicators for confirmation.
## Optimization direction
This strategy can be optimized from the following directions:
1. Test different price data periods and find the most suitable period parameters for calculating volatility.
2. Try different moving average algorithms, such as linear weighted moving average, etc.
3. Introduce trading volume or other indicators to confirm breakout signals.
4. Set a stop loss level or trailing stop to control a single stop loss.
5. Optimize the value of volatility coefficient mult to determine the best target band range.
## Summarize
The overall idea of ​​this strategy is clear. It constructs a target band through price volatility and uses price breakthroughs to generate trading signals, which can effectively track market trends. However, there is also some room for improvement. Through parameter optimization and the introduction of confirmation indicators, the strategy can be made more robust and reliable.
||

## Overview

This strategy generates price bands based on the smoothed volatility of price, and produces trading signals when price breaks through the bands.

## Strategy Logic

The strategy first calculates the average volatility range of price over a certain period, then smoothes the volatility range using an exponential moving average to generate smoothed volatility. The smoothed volatility multiplied by a coefficient gives the range of the bands. When price breaks above the upper band, a buy signal is generated. When price breaks below the lower band, a sell signal is generated.  

Specifically, the smoothed volatility smrng is calculated by the smoothrng function. The upper band hband and lower band lband of the price bands are then calculated based on smrng. The long condition longCondition and short condition shortCondition are set up based on that. When longCondition is met, a buy signal is generated. When shortCondition is met, a sell signal is generated.

## Advantage Analysis  

The advantages of this strategy are:

1. Using price volatility to construct trading signals can effectively track market changes.  

2. Smoothing volatility with exponential moving average can filter noise and generate more reliable trading signals.

3. The range of bands can be adjusted through the volatility coefficient, making the strategy more flexible.  

4. Combined with breakout judgment, it can capture trading opportunities timely when trend reversal occurs.

## Risk Analysis   

There are also some risks in this strategy:

1. In abnormal market volatility, the smoothed volatility may fail to accurately reflect the actual volatility, leading to wrong signals. Parameters can be optimized to improve the model.

2. Improper band range setting may lead to overtrading or insufficient signals. Different parameters can be tested to find the optimal range.  

3. There is time lag in breakout signals, which may cause premature entry or late entry. Other indicators can be introduced for confirmation.

## Optimization Directions

The strategy can be optimized through:  

1. Testing different price data cycles to find the most appropriate period for calculating volatility.

2. Trying different moving average algorithms like weighted moving average.  

3. Introducing trading volume or other indicators to confirm breakout signals.  

4. Setting stop loss or trailing stop to control losses per trade.

5. Optimizing the volatility coefficient mult to determine optimal band range.

## Summary  

The overall logic of this strategy is clear, using price volatility to construct bands and price breakouts to generate trading signals, which can effectively track market trend changes. But there is room for improvement via parameter optimization, signal confirmation etc to make strategy more robust.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|100|Sampling Period|
|v_input_3|3|Range Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-22 00:00:00
end: 2024-01-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("1SmSm1 Strategy", shorttitle="1SmSm1", overlay=true)

// Source
src = input(defval=close, title="Source")

// Sampling Period
per = input(defval=100, minval=1, title="Sampling Period")

// Range Multiplier
mult = input(defval=3.0, minval=0.1, title="Range Multiplier")

// Smooth Average Range
smoothrng(x, t, m) =>
    wper = (t * 2) - 1
    avrng = ema(abs(x - x[1]), t)
    smoothrng = ema(avrng, wper) * m
    smoothrng

smrng = smoothrng(src, per, mult)

// Range Filter
rngfilt(x, r) =>
    rngfilt = x
    rngfilt := x > nz(rngfilt[1]) ? ((x - r) < nz(rngfilt[1]) ? nz(rngfilt[1]) : (x - r)) : ((x + r) > nz(rngfilt[1]) ? nz(rngfilt[1]) : (x + r))
    rngfilt

filt = rngfilt(src, smrng)

// Filter Direction
upward = 0.0
upward := filt > filt[1] ? nz(upward[1]) + 1 : filt < filt[1] ? 0 : nz(upward[1])

downward = 0.0
downward := filt < filt[1] ? nz(downward[1]) + 1 : filt > filt[1] ? 0 : nz(downward[1])

// Target Bands
hband = filt + smrng
lband = filt - smrng

// Breakouts
longCondition = (src > filt) and (src > src[1]) and (upward > 0)
shortCondition = (src < filt) and (src < src[1]) and (downward > 0)

strategy.entry("Buy", strategy.long, when = longCondition)
strategy.entry("Sell", strategy.short, when = shortCondition)

// Plotting
plot(filt, color=upward > 0 ? color.lime : downward > 0 ? color.red : color.orange, linewidth=3, title="Range Filter")
hbandplot = plot(hband, color=color.aqua, transp=100, title="High Target")
lbandplot = plot(lband, color=color.fuchsia, transp=100, title="Low Target")

// Fills
fill(hbandplot, lbandplot, color=color.aqua, title="Target Range")

// Bar Color
barcolor(longCondition ? color.green : shortCondition ? color.red : na)

// Alerts
alertcondition(longCondition, title="Buy Alert", message="BUY")
alertcondition(shortCondition, title="Sell Alert", message="SELL")
```

> Detail

https://www.fmz.com/strategy/440367

> Last Modified

2024-01-29 16:22:14
