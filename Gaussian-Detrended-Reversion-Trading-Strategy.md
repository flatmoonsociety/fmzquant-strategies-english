
> Name

Gaussian-Detrended-Reversion-Trading-Strategy based on Gaussian smoothing
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1589d8a90757cc94093.png)
[trans]

### Overview
This is a strategy that utilizes a custom detrended price oscillator based on Gaussian smoothing to identify potential price reversals. This strategy combines a detrending price oscillator and a Gaussian smoothed moving average of the price cycle, setting specific entry and exit conditions to capture price reversal opportunities.
### Strategy Principles
The strategy first calculates the Detrended Price Oscillator (GDPO) by comparing the closing price to an exponential moving average over a period to identify price cycles in the short term. The GDPO is then Gaussian smoothed using the Arnaud Legoux Moving Average (ALMA) to apply the Gaussian smoothing technique to filter out the noise and give a clearer picture of the price trend.
The strategy uses the intersection of the smoothed GDPO and its lagged version to determine the specific entry and exit conditions for long and short positions. When the smoothed GDPO crosses the lagged version above and is negative, enter the long position; when the smoothed GDPO crosses the lagged version or the zero axis below, close the long position. Similarly, when the smoothed GDPO crosses the lagged version below and is positive, enter the market short; when the smoothed GDPO crosses the lagged version or the zero axis above, close the short position.
On the chart, the smoothed GDPO and its lagged version are plotted in different colors to visually show their crossover. Also draw the zero axis as a reference. Set the background color to change as a reminder when the strategy enters the market. And draw a cross mark at the intersection of GDPO to indicate the exit point.
### Advantage Analysis
This strategy combines detrending techniques with Gaussian smoothing to filter noise to more clearly identify price reversal opportunities. Compared with other oscillators, GDPO cooperates with cyclical analysis by detrending, which can improve accuracy. Gaussian smoothing filters out a lot of noise and makes the indicator signal clearer. Specific entry and exit conditions can effectively control losses.
### Risk Analysis
This strategy is sensitive to parameter adjustments, such as period length, smoothing parameters, etc., and requires sufficient backtesting to determine the appropriate parameter combination, otherwise too many false signals may occur. In trending markets, this strategy may result in continuous losses. Stop loss strategies need to be used together to control single losses. In addition, reversal failure is the main risk of this strategy, and it is necessary to pay attention to morphological characteristics and trend strength to determine the reversal probability.
The robustness of the strategy can be improved by dynamically adjusting parameters and combining trend judgment indicators for optimization. Dynamic stop loss can also be set to control risk.
### Optimization direction
This strategy can be optimized from the following directions:
1. Dynamically adjust smoothing parameters to increase smoothing intensity and reduce false signals in trending markets.
2. Combine with trend judgment indicators, such as ADX, to avoid reversal strategies from continuing losses in trending markets.
3. Add a stop-loss strategy, such as adjusting the stop-loss point with price fluctuations or moving the stop-loss after making a profit.
4. Optimize entry conditions and can be combined with other indicators or patterns as confirmation to improve entry accuracy.
5. Optimize fund management and adjust positions and stop loss points according to market conditions.
6. Test different price data, such as daily, weekly, etc., to evaluate the strategy effects under different cycles.
### Summarize
Based on the Gaussian smoothing detrend reversal strategy, the GDPO indicator is used to identify short-term price cyclicality, and Gaussian filtering technology is applied to extract signals to capture reversal opportunities under clear entry and exit conditions. This strategy effectively controls the risk of reversal trading, but attention needs to be paid to parameter optimization and trend judgment. Through dynamic adjustment, confirmation indicators and stop-loss strategies, the stability of the strategy can be further improved.
||


### Overview

This is a strategy that identifies potential price reversals using a customized Gaussian Detrended Price Oscillator (GDPO) combined with smoothed price cycles. It uses the detrended oscillator with Gaussian smoothing and sets specific entry and exit rules to capture reversal opportunities.

### Strategy Logic

The strategy first calculates the Detrended Price Oscillator (DPO) by comparing the close price to an Exponential Moving Average (EMA) over a specified period to identify short-term price cycles. The DPO values are then smoothed using the Arnaud Legoux Moving Average (ALMA) with Gaussian smoothing technique to filter out noise.

The entry and exit rules are defined based on crossover events between the smoothed GDPO and its lagged version. A long position is entered when the smoothed GDPO crosses above the lag and is negative. The long position is exited when the smoothed GDPO crosses below the lag or the zero line. A short position is entered when the smoothed GDPO crosses below the lag and is positive. The short position is exited when the smoothed GDPO crosses above the lag or the zero line.

The smoothed GDPO and its lag are plotted in distinct colors. The zero line is also displayed as a reference. The chart background color changes when the strategy enters a position. Cross markers are plotted at the crossover points as exit signals.

### Advantage Analysis 

The strategy combines detrending techniques and Gaussian smoothing to more clearly identify reversal opportunities compared to other oscillators. The GDPO improves accuracy by incorporating cycle analysis with detrending. Gaussian smoothing eliminates noise for clearer signals. The specific entry and exit rules effectively control losses.

### Risk Analysis

The strategy is sensitive to parameter tuning like the period lengths and smoothing parameters. Extensive backtesting is required to determine optimal parameters, otherwise excessive false signals may occur. The strategy may produce consecutive losses in trending markets. Stop loss should be used to control single trade loss. Failed reversals are also a major risk. Reversal probability should be confirmed using chart patterns and trend strength. 

Optimization can be done by dynamically adjusting parameters and incorporating trend indicators to improve robustness. Dynamic stops can also control risks.

### Optimization Directions

The strategy can be optimized in several aspects:

1. Dynamically adjust smoothing parameters to increase smoothing in trends and reduce false signals.

2. Incorporate trend indicators like ADX to avoid losses in trending markets. 

3. Add stop loss mechanisms like dynamic or trailing stops.

4. Optimize entry conditions using additional indicators or patterns for higher entry accuracy.

5. Optimize capital management by adjusting position sizing and stops based on market conditions. 

6. Test the strategy across different timeframes like daily or weekly data.

### Summary

The Gaussian Detrended Reversion strategy identifies short-term cycles using the GDPO and extracts signals with Gaussian filtering to capture reversals under defined entry and exit rules. It effectively controls the risks of reversal trading but requires parameter optimization and trend validation. Further improvements in robustness can be made through dynamic adjustments, confirming indicators and stop loss strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|50|Price Length|
|v_input_1|50|Smoothing Length|
|v_input_2|25|Lag Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-31 00:00:00
end: 2023-11-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0
// © DraftVenture

//@version=5
strategy(title="Gaussian Detrended Reversion Strategy", overlay=false, default_qty_type=strategy.percent_of_equity, default_qty_value=15)

//Detrended Price Oscillator for price cycles
period_ = input.int(50, title="Price Length", minval=1)

barsback = period_/2 + 1
ma = ta.ema(close, period_)
dpo = close - ma[barsback]

// Rounded ALMA Calculations for gaussian smoothing
almaSource = dpo
almaWindowSize = input(title="Smoothing Length", defval=50)
lagLength = input(title="Lag Length", defval=25)
almaSmoothed = ta.alma(almaSource, almaWindowSize, 0.85, 6)
almaLag = almaSmoothed[lagLength]

// Reversion entry conditions
entryL = ta.crossover(almaSmoothed, almaLag) and almaSmoothed < 0
exitL = ta.crossunder(almaSmoothed, almaLag) or ta.crossunder(almaSmoothed, 0)
entryS = ta.crossunder(almaSmoothed, almaLag) and almaSmoothed > 0
exitS = ta.crossover(almaSmoothed, almaLag) or ta.crossover(almaSmoothed, 0)

// Long entry and exit
if entryL
    strategy.entry("Long", strategy.long)

if exitL
    strategy.close("Long")

// Short entry and exit
if entryS
    strategy.entry("Short", strategy.short)

if exitS
    strategy.close("Short")

// Plot the oscillator
plot(almaSmoothed, title="GDPO", color=color.green)
plot(almaLag, title="Lag", color=color.white)

hline(0, title="Zero Line", color=color.white)

bgcolor(entryL ? color.new(color.green, 40) : na)
bgcolor(entryS ? color.new(color.red, 40) : na)

plotshape(series=ta.crossunder(almaSmoothed, almaLag) or ta.crossunder(almaSmoothed, 0), style=shape.xcross, location=location.top, color=color.white, size=size.tiny)
plotshape(series=ta.crossover(almaSmoothed, almaLag) or ta.crossover(almaSmoothed, 0), style=shape.xcross, location=location.bottom, color=color.white, size=size.tiny)

//Strategy by KP
```

> Detail

https://www.fmz.com/strategy/431392

> Last Modified

2023-11-07 15:01:19
