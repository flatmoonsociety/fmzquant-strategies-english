
> Name

Multiple-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ed79d67424b4a45cb4df7a776b1263f26f013ab9fc9121e1beb8ee90ee562415.png)
[trans]


## Overview
The multiple trend following strategy comprehensively uses the four indicators of MACD, RSI, ATR and DEMA to identify the long and short-term trends of stocks and conduct trend following transactions. This strategy combines the advantages of breakout trading and trend following trading. It can not only capture the longer-term trend, but also find better entry opportunities in the short-term.
## Strategy Principle
### MACD Trading Strategy
MACD, the moving average convergence and divergence indicator, is a trend-following indicator. MACD consists of a fast moving average and a slow moving average. Commonly used parameters are the fast 12-day EMA, the slow 26-day EMA, and the signal line is the 9-day EMA of MACD. When MACD crosses signal above, it is a buy signal, and when it crosses below, it is a sell signal. This strategy uses MACD's golden cross and dead cross to determine the trend direction.
### RSI overbought and oversold strategy
RSI is the Relative Strength Index, which reflects the overbought and oversold conditions of a stock. RSI is determined by comparing the average closing gain and the average closing decline over a period of time IndexError: list index out of range
## Advantage Analysis
This strategy comprehensively uses four indicators, MACD, RSI, ATR and DEMA, and takes into account trend tracking and breakout trading. It can find better entry opportunities in the trend and has the following advantages:
1. MACD can effectively identify the direction and turning point of the medium and long-term trend of stock prices.
2. RSI can determine whether a stock is overbought or oversold in the short term and avoid chasing highs and falling at trend reversal points.
3. ATR dynamically adjusts the position of the stop loss line, which can effectively control single losses.
4. As an auxiliary judgment indicator, DEMA can filter out some noise.
5. Multiple indicator combinations can improve the reliability of trading signals.
## Risk Analysis
This strategy also has certain risks:
1. Multiple indicator combinations may diverge, causing trading signal errors.
2. ATR, as a dynamic stop loss indicator, can easily be broken through during large fluctuations and lead to losses.
3. As a trend filter indicator, DEMA may filter out strong short-term trading opportunities.
4. Improper strategy parameters may lead to frequent transactions, increased transaction costs and slippage losses.
In order to control risks, indicator parameters can be appropriately adjusted, and other auxiliary judgment indicators can be added for confirmation. Developing quantitative trading strategies requires meticulous analysis of historical data, robust backtesting, and prudent risk management. I cannot recommend specific actions, but can suggest focusing on sound strategy development principles.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Test different parameter combinations to find optimal parameters.
2. Add stop loss strategies, such as trailing stop loss, average stop loss, etc., to further control risks.
3. Add more auxiliary judgment indicators, such as KDJ, Bollinger Bands, etc., to improve signal accuracy.
4. Optimize the timing of entry, such as combining breakthrough and other strategies to find better buying points.
5. Distinguish between long and short markets, using different parameters.
6. Classify modeling according to stock characteristics to make the strategy more adaptable.
## Summarize
The multiple trend following strategy comprehensively uses four indicators, MACD, RSI, ATR and DEMA, to achieve an organic combination of trend following and trend breakthrough. Compared with a single indicator strategy, this strategy can provide more reliable trading signals and avoid certain false signals. Through parameter optimization, stop loss strategies, auxiliary judgment, etc., the strategy effect can be further improved. This strategy is suitable for quantitative transactions that require high trend rotation capabilities, and is a strategic idea worthy of long-term tracking and optimization.
|| 

## Overview

The multiple trend tracking strategy comprehensively utilizes MACD, RSI, ATR and DEMA four indicators to identify the long and short term trends of stocks and conduct trend tracking trading. This strategy combines the advantages of breakout trading and trend tracking trading, which can capture longer-term trends while finding better entry points in the short term.

## Strategy Logic

### MACD Trading Strategy

MACD stands for Moving Average Convergence Divergence, which is a trend-following indicator. MACD consists of a fast moving average line and a slow moving average line, commonly using parameters of 12-day EMA for fast line, 26-day EMA for slow line, and signal line as 9-day EMA of MACD. When MACD crosses above signal line, it's a buy signal, and when crosses below, it's a sell signal. This strategy uses MACD golden cross and dead cross to determine the trend direction.

### RSI Overbought Oversold Strategy

RSI stands for Relative Strength Index, which reflects the overbought and oversold status of a stock. RSI determines whether a stock is overbought or oversold by comparing the average gain and average loss over a period of time. 

## Advantage Analysis

This strategy comprehensively utilizes MACD, RSI, ATR and DEMA four indicators, taking into account both trend tracking and breakout trading, which can find better entry points within the trend. The main advantages are:

1. MACD can effectively identify the direction and turning points of medium and long-term trends of stock prices.

2. RSI can judge whether a stock is overbought or oversold in the short term to avoid chasing highs and selling lows at trend reversal points.

3. ATR dynamically adjusts the stop loss position to effectively control single loss.

4. DEMA serves as an auxiliary judgment indicator to filter out some noise.

5. The combination of multiple indicators can improve the reliability of trading signals.

## Risk Analysis

There are also some risks in this strategy:

1. Divergence may occur with multiple indicators combination, leading to wrong trading signals.

2. ATR as a dynamic stop loss indicator is prone to be broken in large fluctuations resulting in losses. 

3. DEMA as a trend filter may filter some stronger short-term trading opportunities.  

4. Improper strategy parameters may lead to frequent trading, increasing transaction costs and slippage losses.

To control risks, indicators parameters can be adjusted accordingly. More auxiliary judgment indicators can also be introduced for confirmation. Developing quantitative trading strategies requires meticulous analysis of historical data, robust backtesting, and prudent risk management. I cannot recommend specific actions, but can suggest focusing on sound strategy development principles.

## Optimization Directions

The strategy can also be optimized in the following aspects:

1. Test different parameter combinations to find the optimal parameters.

2. Add stop loss strategies like moving stop loss, average stop loss etc. to further control risks.

3. Introduce more auxiliary judgment indicators like KDJ, Bollinger Bands etc. to improve signal accuracy.

4. Optimize entry timing selections by combining breakout strategies to find better entry points. 

5. Differentiate parameters for bull and bear markets.

6. Build models by stock characteristics to improve adaptability.

## Summary

The multiple trend tracking strategy integrates MACD, RSI, ATR and DEMA four indicators, achieving organic combination of trend tracking and trend breakout. Compared with single indicator strategies, this strategy can provide more reliable trading signals and avoid certain false signals. Through parameter optimization, stop loss strategies, auxiliary judgements etc., the strategy performance can be further improved. This strategy is suitable for quantitative trading requiring higher trend switching capabilities and is a promising strategy idea worth long-term tracking and optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|fastLength|
|v_input_2|26|slowlength|
|v_input_3|9|MACDLength|
|v_input_4|18|length|
|v_input_5|30|overSold|
|v_input_6|70|overBought|
|v_input_7|10|ATR Period|
|v_input_8_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_9|3|ATR Multiplier|
|v_input_10|true|Change ATR Calculation Method ?|
|v_input_11|false|Show Buy/Sell Signals ?|
|v_input_12|false|Highlighter On/Off ?|
|v_input_13|25|length1|
|v_input_14_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-10 00:00:00
end: 2023-11-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © prim722

// © OTS Music

//@version=4
strategy("Atrend by OTS", overlay=true)
fastLength = input(12)
slowlength = input(26)
MACDLength = input(9)
MACD = ema(close, fastLength) - ema(close, slowlength)
aMACD = ema(MACD, MACDLength)
delta = MACD - aMACD
if (crossover(delta, 0))
	strategy.entry("MACD buy", strategy.long, comment="MACD buy")
if (crossunder(delta, 0))
	strategy.entry("MACD sell", strategy.short, comment="MACD sell")
//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)
length = input( 18 )
overSold = input( 30 )
overBought = input( 70 )
price = close
vrsi = rsi(price, length)
co = crossover(vrsi, overSold)
cu = crossunder(vrsi, overBought)
if (not na(vrsi))
	if (co)
		strategy.entry("RSI buy", strategy.long, comment="RSI buy")
	if (cu)
		strategy.entry("RSI sell", strategy.short, comment="RSI sell")
//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)


Periods = input(title="ATR Period", type=input.integer, defval=10)
src = input(hl2, title="Source")
Multiplier = input(title="ATR Multiplier", type=input.float, step=0.1, defval=3.0)
changeATR= input(title="Change ATR Calculation Method ?", type=input.bool, defval=true)
showsignals = input(title="Show Buy/Sell Signals ?", type=input.bool, defval=false)
highlighting = input(title="Highlighter On/Off ?", type=input.bool, defval=false)
atr2 = sma(tr, Periods)
atr= changeATR ? atr(Periods) : atr2
up=src-(Multiplier*atr)
up1 = nz(up[1],up)
up := close[1] > up1 ? max(up,up1) : up
dn=src+(Multiplier*atr)
dn1 = nz(dn[1], dn)
dn := close[1] < dn1 ? min(dn, dn1) : dn
trend = 1
trend := nz(trend[1], trend)
trend := trend == -1 and close > dn1 ? 1 : trend == 1 and close < up1 ? -1 : trend
upPlot = plot(trend == 1 ? up : na, title="Up Trend", style=plot.style_line, linewidth=2, color=color.white)
buySignal = trend == 1 and trend[1] == -1
plotshape(buySignal ? up : na, title="UpTrend Begins", location=location.absolute, style=shape.circle, size=size.tiny, color=color.green, transp=0)
plotshape(buySignal and showsignals ? up : na, title="", text="", location=location.absolute, style=shape.labelup, size=size.tiny, color=color.white, textcolor=color.white, transp=0)
dnPlot = plot(trend == 1 ? na : dn, title="Down Trend", style=plot.style_line, linewidth=2, color=color.gray)
sellSignal = trend == -1 and trend[1] == 1
plotshape(sellSignal ? dn : na, title="DownTrend Begins", location=location.absolute, style=shape.circle, size=size.tiny, color=color.red, transp=0)
plotshape(sellSignal and showsignals ? dn : na, title="", text="", location=location.absolute, style=shape.labeldown, size=size.tiny, color=color.red, textcolor=color.white, transp=0)
mPlot = plot(ohlc4, title="", style=plot.style_circles, linewidth=0)
longFillColor = highlighting ? (trend == 1 ? color.white : color.white) : color.white
shortFillColor = highlighting ? (trend == -1 ? color.gray : color.white) : color.white
fill(mPlot, upPlot, title="UpTrend Highligter", color=longFillColor)
fill(mPlot, dnPlot, title="DownTrend Highligter", color=shortFillColor)
alertcondition(buySignal, title="ATrend Buy", message="ATrend Buy!")
alertcondition(sellSignal, title="ATrend Sell", message="ATrend Sell!")
changeCond = trend != trend[1]
alertcondition(changeCond, title="ATrend Direction Change", message="ATrend has changed direction!")

length1 = input(25, minval=1)
srcb = input(close, title="Source")
e1 = ema(srcb, length1)
e2 = ema(e1, length)
dema = 2 * e1 - e2
plot(dema, "DEMA", color.red)
```

> Detail

https://www.fmz.com/strategy/432423

> Last Modified

2023-11-17 17:19:37
