
> Name

Heikin-Ashi-Smoothed-Buy-and-Sell-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is based on a single indicator - Smoothed Sea Line, to achieve simple trend following buying and selling operations. The strategy uses the smoothed sea line indicator to identify the trend direction, and combines the historical K-line patterns to determine the entry opportunity to exit at a profit.
## Strategy Principle
This strategy builds a smoothed sea level line by calculating moving averages. Specifically, it calculates the moving average of the opening price, the highest price, the lowest price, and the closing price, and then calculates the opening price, the highest price, the lowest price, and the closing price of the smoothed sea line.
Determine the buying conditions: the closing price of the current K line is greater than the closing price of the previous K line, the closing price of the previous K line is greater than the closing price of the previous two K lines, and the last three K lines are all positive lines.
Determine the conditions for selling: the closing price of the current K line is lower than the closing price of the previous K line, the closing price of the previous K line is lower than the closing price of the previous two K lines, and the last three K lines are all negative lines.
The conditions for buying and selling must meet the requirement that the latest signal is 0 or the opposite signal to avoid continuous repeated transactions.
## Advantage Analysis
- Using a single indicator, the strategy logic is simple and clear
- Take advantage of the trend following capabilities of the Hygienic Line indicator
- Combined with the K-line pattern, you can avoid missing the trend or performing reverse operations
- Reduce unnecessary transactions by filtering duplicate signals
## Risk Analysis
- The Haijian line has hysteresis and may miss the turning point of the trend.
- Only consider the recent three K-line patterns, lacking long-term trend judgment
- Failure to set a stop loss may lead to increased losses
- Failure to consider the market environment and vulnerable to systemic risks
Improvements can be made by combining other indicators to determine long-term trends, optimizing stop loss strategies, paying attention to the market environment, etc.
## Optimization direction
- Add other indicators to judge and determine the long-term trend direction
- Optimize stop loss strategy and set trailing stop loss or percentage stop loss
- Consider the broader market index and avoid trading in volatile markets
- Optimize parameter settings, adjust moving average period and other parameters
- Add volume energy indicators to ensure there is trading volume support
## Summarize
This strategy uses the trend tracking function of the Haijian line indicator, cooperates with the K-line pattern to determine the entry timing, and controls the trading frequency by filtering repeated signals. The strategy logic is simple, clear and easy to implement. However, it can be improved by combining multiple indicators, optimizing stop losses, paying attention to the market, etc. to make the strategy more robust and reliable.
||


## Overview

This strategy is based on a single indicator - Smoothed Heikin-Ashi, to implement simple trend following buy and sell operations. It identifies trend direction via Smoothed Heikin-Ashi indicator and determines entry timing combined with historical candlestick patterns, in order to take profit exit.

## Strategy Logic  

The strategy calculates moving average of open, high, low and close prices to construct Smoothed Heikin-Ashi. 

Buy condition: Current bar's close > previous bar's close, previous bar's close > 2 bars ago's close, latest 3 bars are bullish.

Sell condition: Current bar's close < previous bar's close, previous bar's close < 2 bars ago's close, latest 3 bars are bearish.

Both buy and sell conditions require the latest signal to be 0 or opposite signal, to avoid consecutive same direction trading.

## Advantage Analysis

- Simple logic with single indicator
- Utilize Heikin-Ashi's trend following ability 
- Avoid missing trends or trading reversely via candlestick patterns
- Reduce unnecessary trades by filtering duplicate signals

## Risk Analysis

- Heikin-Ashi has lagging effect, may miss trend turning points
- Only consider latest 3 bars, lack of long term trend judgment
- No stop loss set, risks enlarging losses
- Ignore overall market conditions, vulnerable to systematic risks

Improvements can be made by combining other indicators for long term trend, optimizing stop loss strategy, paying attention to overall market etc.

## Optimization Directions

- Add other indicators to determine long term trend
- Optimize stop loss such as trailing stop or percentage based stop loss
- Consider overall market index to avoid trading in range bound market
- Optimize parameters like moving average period
- Add volume indicators for ensuring trading volume support

## Summary 

This strategy utilizes Heikin-Ashi's trend following ability and combines candlestick patterns to determine entry timing, while controlling trade frequency via filtering duplicate signals. The logic is simple and easy to implement. But it can be enhanced to be more robust by using multiple indicators combo, optimizing stop loss, considering overall market conditions etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|65|Moving Average Period?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-30 00:00:00
end: 2023-10-06 00:00:00
period: 2d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Masoud Abdoli
//Heikin Ashi Smoothed Buy & Sell Strategy Rev.4
//Date: 01-Oct-2021
//@version=4

strategy(title="Abdoli's Heikin Ashi Smoothed Buy & Sell Strategy Rev.4", shorttitle="Heikin-Ashi Smoothed Rev.4", overlay=true,
 initial_capital=1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

MaPeriod = input (title="Moving Average Period?", type=input.integer, defval=65, minval=5, maxval=100, step=5)

maOpen  = ema(open , MaPeriod)
maHigh  = ema(high , MaPeriod)
maLow   = ema(low  , MaPeriod)
maClose = ema(close, MaPeriod)

haClose = (maOpen+maHigh+maLow+maClose)/4
haOpen = 0.0
haOpen:= na(haOpen[1]) ? (maOpen[1]+maClose[1])/2 : (haOpen[1]+haClose[1])/2
haHigh = max(maHigh, max(haClose, haOpen))
haLow  = min(maLow , max(haClose, haOpen))

plotcandle(haOpen, haHigh, haLow, haClose, title="heikin-Ashi smoothed", color=haOpen>haClose ? color.orange : color.blue)

B0 = haClose    - haOpen
B1 = haClose[1] - haOpen[1]
B2 = haClose[2] - haOpen[2]
BuyCondition = B0 > 0.0 and B1 > 0.0 and B2 > 0.0 and haClose > haClose[1] and haClose[1] > haClose[2]
SellCondition= B0 < 0.0 and B1 < 0.0 and B2 < 0.0 and haClose < haClose[1] and haClose[1] < haClose[2]

last_signal = 0
Buy_final  = BuyCondition  and (nz(last_signal[1]) == 0 or nz(last_signal[1]) ==-1)
Sell_final = SellCondition and (nz(last_signal[1]) == 0 or nz(last_signal[1]) == 1)
last_signal := Buy_final ? 1 : Sell_final ? -1 : last_signal[1]

plotshape(Buy_final , style=shape.labelup  , location=location.belowbar, color=color.blue, title="Buy label" , text="BUY" , textcolor=color.white)
plotshape(Sell_final, style=shape.labeldown, location=location.abovebar, color=color.red , title="Sell label", text="SELL", textcolor=color.white)

strategy.entry("Buy", strategy.long, when=Buy_final)
strategy.close("Buy", when=Sell_final)
```

> Detail

https://www.fmz.com/strategy/428608

> Last Modified

2023-10-07 15:01:06
