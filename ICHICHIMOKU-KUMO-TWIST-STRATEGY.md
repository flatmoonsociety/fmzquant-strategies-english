
> Name

ICH Cloud Belt Twist StrategyICHIMOKU-KUMO-TWIST-STRATEGY
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1b3b73ee751e86013d4.png)

[trans]

## Overview
The Ichimoku Kumo Twist strategy uses the conversion line, base line and traverse line of the Ichimoku indicator to construct trading signals and is a trend following strategy. It looks for short-term and medium-term trend reversal points through the reversal of the Ichimoku cloud band to obtain lower-risk breakthrough points and overbought and oversold opportunities. This strategy can be used for both intraday trading and medium and long-term trading where positions are held for several weeks.
## Strategy Principle
This strategy mainly uses the three moving averages of the Ichimoku indicator - the conversion line, the base line and the traverse line 1, as well as the highest and lowest prices of the K line to calculate the upper and lower bounds of the cloud band. The conversion line calculates the midpoints of the highest and lowest prices of the past 9 K lines, representing the short-term moving average of the Ichimoku balance chart; the baseline line calculates the midpoints of the highest and lowest prices of the past 26 K lines, representing the long-term moving average. Wire 1 is the average line of the conversion line and the base line, and Wire 2 is the midpoint price of the past 52 K lines.
When wire 1 crosses wire 2, a buy signal is generated, and when wire 1 crosses wire 2, a sell signal is generated. This trading strategy is to track the golden cross of the short-term and medium-term moving averages to capture changes in trends.
## Advantage Analysis
- The Ichimoku cloud band reversal strategy combines both short-term and medium-term trends and can effectively identify trend reversal points.
- The strategy based on moving average has a certain hysteresis and can filter out some noise.
- Use cloud bands to determine the obviousness of strong and weak trends and achieve better entries and exits.
- No parameter optimization is required, just use Ichimoku standard parameters.
## Risk Analysis
- The Ichimoku principle is relatively complex, insensitive to parameter adjustment, and difficult to over-optimize.
- In a consolidating market, multiple false signals may appear.
- When the short-term and medium-term trends diverge, the strategy will fail.
- Stop loss must be used to control risks, otherwise it may cause larger losses.
## Optimization direction
- You can test different parameter combinations of conversion lines and baselines to find the best balance point.
- Combine with other indicators to filter entry signals to avoid opening positions in obviously unfavorable patterns.
- Add stop loss strategy and set dynamic stop loss or trailing stop loss.
- Optimize position management and adjust position size according to market conditions.
- Add transaction fees to the backtest to make the backtest results more accurate.
## Summarize
The Ichimoku cloud band reversal strategy is overall a moderate trend strategy. It can effectively identify trend turning points and open positions in the direction of the trend. However, this strategy also has certain monitoring costs and must be combined with strict risk management measures before it can be used for a long time. By continuously optimizing parameter settings, entry filters, stop loss methods, etc., the stability and profitability of this strategy can be continued to be improved.
||


## Overview

The Ichimoku Kumo Twist strategy utilizes the conversion line, baseline, and leading span lines of the Ichimoku indicator to construct trading signals as a trend following strategy. It identifies short-term and medium-term trend reversal points by watching for twists in the Ichimoku clouds to find lower risk breakout points and overbought/oversold opportunities. The strategy can be used for intraday trading as well as multi-week intermediate-term trading.

## Strategy Logic

The strategy primarily uses three Ichimoku lines – the conversion line, baseline, and leading span 1, along with the high and low prices of the candlesticks to calculate the upper and lower cloud boundaries. The conversion line calculates the midpoint of the high and low over the past 9 candles, representing the short-term mean. The baseline calculates the midpoint of the high and low over the past 26 candles as the long-term mean. Leading span 1 is the average of the conversion and baseline lines. Leading span 2 is the midpoint price of the past 52 candles. 

Buy signals are generated when the leading span 1 crosses over leading span 2, while sell signals are generated when leading span 1 crosses under leading span 2. The trading strategy simply tracks the bullish and bearish crosses of the short and medium-term means to capture trend changes.

## Advantage Analysis

- The Ichimoku cloud twist strategy combines both short-term and medium-term trends, which can effectively identify trend reversal points.

- Mean reversion based strategies have some lag built in to filter out noise.

- Using the clouds to gauge trend strength allows for improved entries and exits.

- No parameter optimization needed - the standard Ichimoku parameters work well.

## Risk Analysis

- Ichimoku has fairly complex internals and is not very sensitive to parameter tweaks making overoptimization difficult.

- There can be multiple false signals during range-bound markets. 

- Divergence between short and medium-term trends can cause strategy breakdowns.

- Stop losses are essential to control risk, otherwise large drawdowns are possible.

## Improvement Opportunities

- Test different combinations of conversion and baseline periods to find optimal balance.

- Add filters with other indicators to avoid taking signals in unfavorable formations. 

- Incorporate stop loss strategies like dynamic or trailing stops.

- Optimize position sizing based on market conditions.

- Add trading commissions in backtests for more realistic results.

## Summary

Overall, the Ichimoku cloud twist strategy is a moderate trend following strategy. It can effectively identify turns in trend and take positions in alignment with the trend direction. But monitoring is required and strict risk controls are necessary for long-term use. Continued improvements in parameter tuning, entry filters, stop loss mechanics, and more can further enhance this strategy's stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Scaling: Linear|Log|
|v_input_2|0|Presets: Crypto Doubled|Crypto Singled|Standard Doubled|Standard Singled|
|v_input_3|true|Drop first N candles|
|v_input_4|false|Show Clouds|
|v_input_5|true|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-20 00:00:00
end: 2023-10-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="Ichimoku Kumo Twist Strategy (Presets)", shorttitle="Kumo Twist Strategy", overlay=true)

xlowest_(src, len) =>
    x = src
    for i = 1 to len - 1
        v = src[i]
        if (na(v))
            break
        x := min(x, v)
    x

xlowest(src, len) =>
    na(src[len]) ? xlowest_(src, len) : lowest(src, len)

xhighest_(src, len) =>
    x = src
    for i = 1 to len - 1
        v = src[i]
        if (na(v))
            break
        x := max(x, v)
    x

xhighest(src, len) =>
    na(src[len]) ? xhighest_(src, len) : highest(src, len)

dropn(src, n) =>
    na(src[n]) ? na : src

ichiConversionPeriods(presets) =>
    if presets == "Crypto Doubled"
        20
    else
        if presets == "Crypto Singled"
            10
        else
            if presets == "Standard Doubled"
                18
            else
                9

ichiBasePeriods(presets) =>
    if presets == "Crypto Doubled"
        60
    else
        if presets == "Crypto Singled"
            30
        else
            if presets == "Standard Doubled"
                52
            else
                26

ichiLaggingSpan2Periods(presets) =>
    if presets == "Crypto Doubled"
        120
    else
        if presets == "Crypto Singled"
            60
        else
            if presets == "Standard Doubled"
                104
            else
                52

ichiDisplacement(presets) =>
    if presets == "Crypto Doubled"
        30
    else
        if presets == "Crypto Singled"
            30
        else
            if presets == "Standard Doubled"
                26
            else
                26

scaling = input(title="Scaling", options=["Linear", "Log"], defval="Linear")
presets = input(title="Presets",  options=["Crypto Doubled", "Crypto Singled", "Standard Doubled", "Standard Singled"], defval="Crypto Doubled")
dropCandles = input(1, minval=0, title="Drop first N candles")
showClouds = input(false, "Show Clouds")
stoploss = input(true, title="Stop Loss")

conversionPeriods = ichiConversionPeriods(presets)
basePeriods = ichiBasePeriods(presets)
laggingSpan2Periods = ichiLaggingSpan2Periods(presets)
displacement = ichiDisplacement(presets)
logScaling = scaling == "Log"

lows = dropn(low, dropCandles)
highs = dropn(high, dropCandles)

lowsp = logScaling ? log(lows) : lows
highsp = logScaling ? log(highs) : highs

donchian(len) =>
    avg(xlowest(lowsp, len), xhighest(highsp, len))

conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)

golong = crossover(leadLine1, leadLine2)
goshort = crossunder(leadLine1, leadLine2)

strategy.entry("Buy", strategy.long, when=golong, stop=(stoploss ? high+syminfo.mintick : na))
strategy.entry("Sell", strategy.short, when=goshort, stop=(stoploss ? low-syminfo.mintick : na))

conversionLinep = logScaling ? exp(conversionLine) : conversionLine
baseLinep = logScaling ? exp(baseLine) : baseLine
leadLine1p = logScaling ? exp(leadLine1) : leadLine1
leadLine2p = logScaling ? exp(leadLine2) : leadLine2

plot(showClouds ? conversionLinep : na, color=#0496ff, title="Conversion Line")
plot(showClouds ? baseLinep : na, color=#991515, title="Base Line")

p1 = plot(showClouds ? leadLine1p : na, offset = displacement, color=green, title="Lead 1")
p2 = plot(showClouds ? leadLine2p : na, offset = displacement, color=red, title="Lead 2")
fill(p1, p2, color = showClouds ? (leadLine1p > leadLine2p ? green : red) : na)

```

> Detail

https://www.fmz.com/strategy/430375

> Last Modified

2023-10-27 16:36:59
