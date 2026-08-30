
> Name

Adaptive-ATR-and-RSI-Trend-Following-Strategy-with-Trailing-Stop-Loss Based on ATR and RSI
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11d7fb5966e67391076.png)
 [trans]

## Overview
This strategy uses a combination of average true range (ATR), relative strength index (RSI), and trailing stops to achieve adaptive trend following. Use ATR to calculate the dynamic stop loss level, use RSI to determine the market trend direction, and use the moving stop loss to track price fluctuations to maximize profits. This is a very typical trend following strategy.
## Strategy Principle
1. Calculate ATR. ATR reflects the volatility and risk level of the market. This strategy uses ATR to calculate dynamic stop loss levels and implement adaptive stop loss.
2. Calculate RSI. RSI can determine whether the market is overbought or oversold. When the RSI is greater than 50, it is bullish, and when it is less than 50, it is bearish. This strategy uses RSI to determine the direction of price trends.
3. Trailing stop loss. Based on the stop loss level calculated by ATR and the trend direction judged by RSI, this strategy realizes the moving stop loss and continuously tracks the price fluctuations, while ensuring the stop loss and gradually increasing the take profit level to maximize profits.
4. Specifically, when the RSI is greater than 50, open a long position and when it is less than 50, open a short position. Then use the stop loss price calculated by ATR to move the stop loss and track the price fluctuation.
## Advantage Analysis
1. Use ATR to implement adaptive stop loss, which can dynamically adjust the stop loss range according to market volatility to avoid the shortcomings of too large or too small stop loss.
2. RSI determines the trend direction accurately and reliably to avoid trading being trapped in a volatile market.
3. Trailing stop loss tracks price fluctuations, can increase the take profit level, and fully follow the trend to make profits.
## Risk Analysis
1. ATR and RSI parameter settings need to be optimized through backtesting, otherwise the strategy effect will be affected.
2. Although there is stop loss protection, a large gap cannot avoid the risk of the stop loss being breached. Positions can be appropriately reduced to control risks.
3. The strategy is highly dependent on the optimization of trading product parameters, and parameters need to be adjusted for different products.
## Optimization direction
1. You can consider adding machine learning algorithms to achieve adaptive optimization of parameters.
2. Add a position control module, which can dynamically adjust the position size according to market conditions and reduce the probability of breaking through the stop loss.
3. Add trend judgment indicators to avoid losses caused by missing the top and bottom reversal points.
## Summary
This strategy integrates the use of ATR, RSI and moving stop modules to form a typical adaptive trend following strategy. Through parameter optimization, it can be very flexibly adapted to different trading varieties, and it is a recommended universal trend following strategy. After adding more indicator judgments and machine learning algorithm optimization, the effect of this strategy can be further improved.
||

## Overview

This strategy combines Average True Range (ATR), Relative Strength Index (RSI) and trailing stop loss to achieve adaptive trend following. Dynamic stop loss is calculated by ATR to reflect market volatility, RSI identifies the trend direction, and trailing stop loss tracks price fluctuation to maximize profit. It is a very typical trend following strategy.  

## Principles

1. Calculate ATR. ATR shows market volatility and risk level. This strategy uses ATR to compute dynamic stop loss for adaptive risk control.  

2. Calculate RSI. RSI judges overbought/oversold status. When RSI is above 50 it signals bullish outlook, when below 50 bearish outlook. This strategy utilizes RSI to determine trend direction.

3. Trailing stop loss tracking. According to stop loss level calculated by ATR and trend direction by RSI, this strategy keeps moving stop loss to track price fluctuation, to maximize profit while ensuring effective stop loss.  

4. Specifically, long when RSI goes above 50, short when goes below 50. Then moving stop loss based on ATR to lock in profit along the trend.

## Advantage Analysis 

1. ATR adaptive stop loss considers market volatility, avoids too wide or too tight stop loss.

2. RSI reliably identifies trend, avoids whipsaws.  

3. Trailing stop loss tracks trend to expand profit target.

## Risk Analysis

1. ATR and RSI parameters need backtest optimization, otherwise impact strategy performance.  

2. Although with stop loss protection, risk still exists for sudden price jump to penetrate stop loss. Can consider position sizing to control risk.

3. Strategy performance relies much on parameter tuning for different products.

## Enhancement 

1. Consider machine learning algorithms for adaptive parameter optimization.  

2. Add position sizing control for dynamic adjustment based on market condition, to reduce stop loss penetration probability.  

3. Add more trend indicators to avoid missing major trend reversal points.

## Conclusion
This strategy integrates ATR, RSI and trailing stop loss for a typical adaptive trend following system. Through parameter tuning it can be flexibly adapted to different trading products, a recommended universal trend following strategy. With more judgements and machine learning optimization it can achieve even better performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2019|BACKTEST START YEAR|
|v_input_2|true|BACKTEST START MONTH|
|v_input_3|true|BACKTEST START DAY|
|v_input_4|2222|BACKTEST STOP YEAR|
|v_input_5|12|BACKTEST STOP MONTH|
|v_input_6|31|BACKTEST STOP DAY|
|v_input_7_hlc3|0|SOURCE: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_8|14|RSI LENGTH|
|v_input_9|52|RSI CENTER LINE|
|v_input_10|7|MACD FAST LENGTH|
|v_input_11|12|MACD SLOW LENGTH|
|v_input_12|12|MACD SIGNAL SMOOTHING|
|v_input_13|10|Key Vaule. 'This changes the sensitivity'|
|v_input_14|3|SmoothK|
|v_input_15|3|SmoothD|
|v_input_16|14|LengthRSI|
|v_input_17|14|LengthStoch|
|v_input_18_close|0|RSISource: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_19|10|ATR Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-19 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title="UTBot Strategy", overlay = true )
   
// CREDITS to @HPotter for the orginal code. 
// CREDITS to @Yo_adriiiiaan for recently publishing the UT Bot study based on the original code -
// CREDITS to @TradersAITradingPlans for making this Strategy. 
// Strategy fixed with Time period by Kirk65.
// I am using this UT bot with 2 hours time frame with god resultss. Alert with "Once per bar" and stoploss 1.5%. If Alerts triggered and price goes against Alert. Stoploss will catch it. Wait until next Alert.
// While @Yo_adriiiiaan mentions it works best on a 4-hour timeframe or above, witch is a lot less risky, but less profitable. 

testStartYear = input(2019, "BACKTEST START YEAR", minval = 1980, maxval = 2222) 
testStartMonth = input(01, "BACKTEST START MONTH", minval = 1, maxval = 12)
testStartDay = input(01, "BACKTEST START DAY", minval = 1, maxval = 31)
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)
testStopYear = input(2222, "BACKTEST STOP YEAR", minval=1980, maxval = 2222)
testStopMonth = input(12, "BACKTEST STOP MONTH", minval=1, maxval=12)
testStopDay = input(31, "BACKTEST STOP DAY", minval=1, maxval=31)
testPeriodStop = timestamp(testStopYear, testStopMonth, testStopDay, 0, 0)

testPeriod = true

SOURCE = input(hlc3)
RSILENGTH = input(14, title = "RSI LENGTH")
RSICENTERLINE = input(52, title = "RSI CENTER LINE")
MACDFASTLENGTH = input(7, title = "MACD FAST LENGTH")
MACDSLOWLENGTH = input(12, title = "MACD SLOW LENGTH")
MACDSIGNALSMOOTHING = input(12, title = "MACD SIGNAL SMOOTHING")
a = input(10, title = "Key Vaule. 'This changes the sensitivity'") 
SmoothK = input(3)
SmoothD = input(3)
LengthRSI = input(14)
LengthStoch = input(14)
RSISource = input(close) 
c = input(10, title="ATR Period")
xATR = atr(c)
nLoss = a * xATR
xATRTrailingStop = iff(close > nz(xATRTrailingStop[1], 0) and close[1] > nz(xATRTrailingStop[1], 0), max(nz(xATRTrailingStop[1]), close - nLoss),
     iff(close < nz(xATRTrailingStop[1], 0) and close[1] < nz(xATRTrailingStop[1], 0), min(nz(xATRTrailingStop[1]), close + nLoss), 
     iff(close > nz(xATRTrailingStop[1], 0), close - nLoss, close + nLoss)))
pos =	iff(close[1] < nz(xATRTrailingStop[1], 0) and close > nz(xATRTrailingStop[1], 0), 1,
     iff(close[1] > nz(xATRTrailingStop[1], 0) and close < nz(xATRTrailingStop[1], 0), -1, nz(pos[1], 0))) 
color = pos == -1 ? red: pos == 1 ? green : blue 
ema= ema(close,1)
above = crossover(ema,xATRTrailingStop )
below = crossover(xATRTrailingStop,ema)
buy = close > xATRTrailingStop and above 
sell = close < xATRTrailingStop and below
barbuy = close > xATRTrailingStop 
barsell = close < xATRTrailingStop 
plotshape(buy, title = "Buy", text = 'Buy', style = shape.labelup, location = location.belowbar, color= green,textcolor = white, transp = 0, size = size.tiny)
plotshape(sell, title = "Sell", text = 'Sell', style = shape.labeldown, location = location.abovebar, color= red,textcolor = white, transp = 0, size = size.tiny)
barcolor(barbuy? green:na)
barcolor(barsell? red:na)
//alertcondition(buy, title='Buy', message='Buy')
//alertcondition(sell, title='Sell', message='Sell')

if (buy)
    strategy.entry("UTBotBuy",strategy.long, when=testPeriod)
if (sell)
    strategy.entry("UTBotSell",strategy.short, when=testPeriod)
```

> Detail

https://www.fmz.com/strategy/439710

> Last Modified

2024-01-23 11:31:14
