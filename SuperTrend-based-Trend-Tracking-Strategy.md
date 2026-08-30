
> Name

SuperTrend-based-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11a6b4451a355e17d87.png)
[trans]

## Overview
This strategy is a super trend line constructed based on the Average True Range (ATR) indicator. It is a trend following strategy used to determine the direction of the market trend and give trading signals. This strategy has the dual functions of trend judgment and trend tracking, and can be used in fields such as stock index futures, foreign exchange, and digital currencies.
## Strategy Principle
This strategy determines whether the price is in an upward trend channel by calculating the ATR indicator within a certain period and comparing it with the price. Specifically, the strategy first calculates the ATR indicator, and then constructs the upper and lower rails based on the ATR value multiplied by the coefficient. When the price is higher than the upper track, it is judged to be an upward trend; when the price is lower than the lower track, it is judged to be a downward trend. During an upward trend, if the price changes from a downward trend to an upward trend, a buy signal is generated; during a downward trend, if the price changes from an upward trend to a downward trend, a sell signal is generated.
The key to this strategy is to construct the trend judgment standard-the super trend line. The super trend line is based on the dynamic change of the ATR indicator, which can effectively filter market noise and determine the main trend direction. At the same time, the super trend line has a certain hysteresis, which helps to confirm the turning point of the trend and avoid generating false trading signals.
## Strategic Advantages
The biggest advantage of this strategy is the ability to combine trend judgment and trend following. Specifically, the main advantages are:
1. The super trend line constructed using ATR can effectively identify market trends and filter out noise.
2. Super trend lines have a certain hysteresis, which helps reduce false signals.  
3. It can provide trend judgment and trading signals at the same time, and the operation is simple.
4. Parameterization parameters can be optimized to adapt to a wider market.
5. Visual indicators to intuitively judge the current trend status.
## Risk Analysis
This strategy mainly involves the following risks:
1. Improper setting of ATR parameters may cause the super trend line to be too sensitive or lagging.
2. The influence of noise cannot be completely avoided, and erroneous signals may be generated in individual cases.  
3. When the market fluctuates violently, the accuracy of judging the trend line will decrease.
4. It is impossible to predict the trend reversal point and can only track the trend that has already occurred.
In terms of countermeasures, it can be optimized by adjusting parameters such as the ATR cycle and the super-trend line coefficient, or it can be verified in combination with other indicators to reduce the probability of false signals. In addition, stop loss points can be set to control single losses.
## Optimization direction
There is room for further optimization of this strategy:
1. Combined with machine learning algorithms to achieve automatic optimization of parameters.
2. Add indicator judgment and verification such as exponential smoothing moving average.  
3. Set up stop-loss and stop-profit strategies to optimize fund management.
4. Combine sentiment indicators, news analysis and other methods to predict potential trend reversals.
5. Use deep learning technology to analyze a larger amount of historical data and improve the accuracy of judgment.
Through in-depth optimization, it is expected to further improve the stability, adaptability and profitability of the strategy.
## Summarize
This strategy is generally stable, reliable and has good returns. Constructing a super trend line to determine the main trend and giving trading signals at the same time is the biggest highlight of the strategy. But there is also a certain degree of lag and risk of misjudgment. Through parameter and model optimization, it is expected to obtain better strategy performance. Generally speaking, this strategy is a typical representative based on trends and is worthy of real-time verification and application.
||


## Overview

This strategy is constructed based on the Average True Range (ATR) indicator to build a SuperTrend line for judging market trend direction and generating trading signals. It has both trend judgment and trend tracking capabilities, applicable to indices futures, forex, and cryptocurrencies.  

## Strategy Logic

The strategy calculates the ATR over a certain period and compares it with price to determine if the price is within an uptrend channel. Specifically, it first computes the ATR, then uses the ATR value multiplied by a factor to plot the upper and lower bands. When the price is higher than the upper band, an uptrend is identified. When the price is below the lower band, a downtrend is identified. In an uptrend, if the price changes from downtrend to uptrend, a buy signal is generated. In a downtrend, if the price changes from uptrend to downtrend, a sell signal is triggered.  

The key lies in constructing the trend judgment benchmark - SuperTrend line. The SuperTrend line is based on the dynamically changing ATR, which can effectively filter out market noise and determine the major trend direction. Meanwhile, the SuperTrend line has a certain lagging effect, which helps confirm trend reversal points and avoid generating incorrect trading signals.

## Advantages

The biggest advantage of this strategy is the combination of trend identification and tracking abilities:  

1. The ATR-based SuperTrend line can effectively identify market trends and filter out noise.
2. The lagging effect of the SuperTrend line helps reduce incorrect signals.
3. It can give both trend judgment and trading signals for easy operation.  
4. The parameters can be optimized for fitting more diverse markets.
5. Visual indicators allow intuitive trend judgments.

## Risk Analysis   

The main risks of this strategy include:

1. Improper ATR parameter setting may cause too sensitive or lagging SuperTrend lines.  
2. It cannot completely avoid the impact of noise, which may occasionally trigger incorrect signals.
3. The accuracy decreases during violent market fluctuations.  
4. It cannot predict trend reversal points but can only track existing trends.

Possible solutions include optimizing parameters like ATR period and SuperTrend factor, combining with other indicators for verification, and reducing incorrect signal probabilities. Also, stop losses can control single trade loss.

## Optimization Directions

Further optimization space exists in areas like:

1. Adopting machine learning for automatic parameter optimization.  
2. Adding indicators like exponential moving averages for verification.
3. Setting up stop loss/profit taking strategies for refined money management. 
4. Combining sentiment indicators and news analytics to predict potential trend reversals.
5. Leveraging deep learning to analyze more historical data and improve accuracy.

In-depth optimization promises to further lift stability, adaptiveness and profitability of the strategy.  

## Conclusion  

The strategy demonstrates great stability, reliability and profitability overall. Constructing the SuperTrend line for major trend judgment and trading signals is its biggest highlight. But certain degree of lagging effect and misjudgment risks do exist. Parameter and model optimization promises better strategy performance. In summary, as a typical trend-based strategy, it is worthwhile to verify and utilize it in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|ATR Period|
|v_input_2_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_3|3|ATR Multiplier|
|v_input_4|true|Change ATR Calculation Method?|
|v_input_5|true|Show Buy/Sell Signals?|
|v_input_6|true|Highlighter On/Off?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-01 00:00:00
end: 2023-12-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Supertrend Strategy", overlay = true)

Periods = input(10, title="ATR Period")
src = input(hl2, title="Source")
Multiplier = input(3.0, title="ATR Multiplier", step=0.1)
changeATR = input(true, title="Change ATR Calculation Method?")
showsignals = input(true, title="Show Buy/Sell Signals?")
highlighting = input(true, title="Highlighter On/Off?")

atr2 = sma(tr, Periods)
atr = changeATR ? atr(Periods) : atr2

up = src - (Multiplier * atr)
up1 = nz(up[1], up)
up := close[1] > up1 ? max(up, up1) : up

dn = src + (Multiplier * atr)
dn1 = nz(dn[1], dn)
dn := close[1] < dn1 ? min(dn, dn1) : dn

trend = 1
trend := nz(trend[1], trend)
trend := trend == -1 and close > dn1 ? 1 : trend == 1 and close < up1 ? -1 : trend

upPlot = plot(trend == 1 ? up : na, title="Up Trend", style=plot.style_linebr, linewidth=2, color=color.green)
buySignal = trend == 1 and trend[1] == -1
plotshape(buySignal ? up : na, title="UpTrend Begins", location=location.absolute, style=shape.circle, size=size.tiny, color=color.green, transp=0)
plotshape(buySignal and showsignals ? up : na, title="Buy", text="Buy", location=location.absolute, style=shape.labelup, size=size.tiny, color=color.green, textcolor=color.white, transp=0)

dnPlot = plot(trend == 1 ? na : dn, title="Down Trend", style=plot.style_linebr, linewidth=2, color=color.red)
sellSignal = trend == -1 and trend[1] == 1
plotshape(sellSignal ? dn : na, title="DownTrend Begins", location=location.absolute, style=shape.circle, size=size.tiny, color=color.red, transp=0)
plotshape(sellSignal and showsignals ? dn : na, title="Sell", text="Sell", location=location.absolute, style=shape.labeldown, size=size.tiny, color=color.red, textcolor=color.white, transp=0)

mPlot = plot(ohlc4, title="", style=plot.style_circles, linewidth=0)

longFillColor = highlighting ? (trend == 1 ? color.green : color.white) : color.white
shortFillColor = highlighting ? (trend == -1 ? color.red : color.white) : color.white

fill(mPlot, upPlot, title="UpTrend Highlighter", color=longFillColor)
fill(mPlot, dnPlot, title="DownTrend Highlighter", color=shortFillColor)

strategy.entry("Buy", strategy.long, when=buySignal)
strategy.entry("Sell", strategy.short, when=sellSignal)

alertcondition(buySignal, title="SuperTrend Buy", message="SuperTrend Buy!")
alertcondition(sellSignal, title="SuperTrend Sell", message="SuperTrend Sell!")
changeCond = trend != trend[1]
alertcondition(changeCond, title="SuperTrend Direction Change", message="SuperTrend has changed direction!")

```

> Detail

https://www.fmz.com/strategy/434718

> Last Modified

2023-12-08 17:07:53
