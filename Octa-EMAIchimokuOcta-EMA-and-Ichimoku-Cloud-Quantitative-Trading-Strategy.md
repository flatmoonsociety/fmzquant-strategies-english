
> Name

Octa-EMA-and-Ichimoku-Cloud-Quantitative-Trading-Strategy Octa-EMA-and-Ichimoku-Cloud-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10b53f3c8a203d05490.png)

[trans]

## Overview
This strategy uses 8 exponential moving averages with different periods and the Ichimoku cloud chart as the main trading signals, and can run effectively on the 1 hour, 4 hour or daily time frame.
## Strategy Principle
The core principles of this strategy are based on the following two parts:
1. 8 Exponential Moving Average (Octa-EMA)
This strategy uses 8 EMAs of different periods, namely the 5-day line, the 11-day line, the 15-day line, the 18-day line, the 21-day line, the 24-day line, the 28-day line and the 34-day line. These 8 EMAs are called "Octa-EMA". When the shorter period EMA is above the longer period EMA, it indicates a bullish trend, and vice versa, it indicates a bearish trend.
2. Ichimoku cloud indicator
The Ichimoku cloud chart contains conversion lines, base lines, delay lines and leading lines A/B. The cloud chart mainly determines the trend direction and provides support and resistance. When the price is above the cloud chart, it is a bullish trend, and when the price is below the cloud chart, it is a bearish trend.
The trading signals of this strategy come from the above two components. A buy signal is generated when all 8 EMAs are in a long arrangement (short EMA is above the long EMA) and the price is higher than Ichimoku's cloud chart. A sell signal is generated when the EMA alignment turns bearish (short EMA crosses below the long EMA).
## Strategic advantage analysis
This strategy mainly has the following advantages:
1. Use dual indicator filtering to reduce false signals
2. Ichimoku cloud chart can determine the trend direction and avoid contrarian trading.
3. 8 EMA cross combinations to determine trends and improve accuracy
4. Can operate in various time periods
5. There is a large space for parameter optimization and can be customized for different varieties.
## Strategy risk analysis
This strategy also has certain risks:
1. More short signals may be generated in a volatile market
2. The buying conditions are strict and you may miss some buying points.
3. It may fail when the short-term and mid- to long-term trends are inconsistent.
4. Improper EMA parameter settings may cause signal lag
In view of the above risks, the risk can be reduced by adjusting EMA parameters or optimizing entry conditions, or it can be combined with other indicators as assistance.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Adjust EMA parameters and optimize the corresponding period
2. Add moving average long and short judgment indicators to ensure the accuracy of trend judgment.
3. Combine MACD, KDJ and other indicators to optimize entry timing
4. Add stop-loss and take-profit strategies to control single profit and loss
5. Test the parameter effects of different varieties and find the best parameter combination
6. Use machine learning algorithms to automatically optimize parameters
## Summarize
Octa-EMA and Ichimoku cloud chart quantitative trading strategies are generally a relatively stable and reliable trend following strategy. It uses EMA combination to judge the trend and Ichimoku to filter signals at the same time, and can obtain a lower misjudgment rate after parameter optimization. This strategy can be widely used in stock indexes, foreign exchange, precious metals and other varieties, and can also be run in multiple time periods. If stop-loss, take-profit and auxiliary indicators can be combined, the winning rate and profitability of the strategy can be further improved.
||

## Overview

This strategy uses 8 exponential moving averages (EMAs) of different periods and the Ichimoku cloud as the main trading signals, which can run effectively in hourly, 4-hour or daily timeframes.

## Strategy Principles 

The core principles of this strategy are based on the following two parts:

1. 8 Exponential Moving Averages (Octa-EMA)

   This strategy uses 8 EMAs with different periods, specifically 5-day, 11-day, 15-day, 18-day, 21-day, 24-day, 28-day and 34-day. These 8 EMAs are referred to as "Octa-EMA". When shorter period EMAs are above longer period EMAs, it indicates an uptrend, and vice versa for a downtrend.  

2. Ichimoku Cloud

   The Ichimoku cloud contains the conversion line, base line, lagging span and leading spans A/B. The cloud mainly judges trend direction and provides support/resistance. When price is above the cloud, it indicates an uptrend, and when below the cloud, it indicates a downtrend.

The trading signals for this strategy come from the combination of the above two components. A buy signal is generated when all 8 EMAs are in an uptrend arrangement (shorter EMA above longer EMA) and the price is above the Ichimoku cloud. A sell signal is generated when the EMA arrangement flips to a downtrend (shorter EMA crossing below longer EMA).

## Advantage Analysis  

The main advantages of this strategy are:

1. Reduces false signals through double indicator filtering  
2. Ichimoku cloud judges trend direction, avoiding counter-trend trading
3. 8 EMA crossovers combine to determine trends with higher accuracy  
4. Can run on multiple timeframes  
5. Large parameter tuning space, can customize for different products

## Risk Analysis   

This strategy also has some risks:

1. May generate more false sell signals during range-bound markets
2. Strict buy conditions may miss some buying opportunities 
3. May fail when short-term and mid-term trends conflict
4. Poor EMA parameter tuning can cause signal lag

To address these risks, parameters can be adjusted or entry conditions optimized to reduce risk. Other indicators can also be incorporated for confirmation.  

## Optimization Directions

This strategy can be optimized in several aspects:

1. Adjust EMA parameters to find optimal periods
2. Add trend-determining indicators to ensure accurate trend judgement 
3. Incorporate additional indicators like MACD, KDJ to improve entry timing
4. Add stop loss/take profit to control per trade risk
5. Test parameters across different products to find best fit  
6. Use machine learning to auto-optimize parameters

## Conclusion  

Overall, the Octa-EMA and Ichimoku cloud strategy is a relatively stable and reliable trend following system. It uses EMA crossovers to determine trends and Ichimoku to filter signals, providing low false signals when optimized. This strategy can be widely applied on indices, forex, metals etc. at multiple timeframes. By incorporating stop loss/take profit and confirming indicators, win rate and profitability can be further improved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Ribbon (EMA)|
|v_input_2|5|EMA 1 Length|
|v_input_3|11|EMA 2 Length|
|v_input_4|15|EMA 3 Length|
|v_input_5|18|EMA 4 Length|
|v_input_6|21|EMA 5 Length|
|v_input_7|24|EMA 6 Length|
|v_input_8|28|EMA 7 Length|
|v_input_9|34|EMA 8 Length|
|v_input_10|false|Chikou|
|v_input_11|false|Tenkan|
|v_input_12|false|Kijun|
|v_input_int_1|9|conversionPeriods|
|v_input_int_2|26|basePeriods|
|v_input_int_3|52|laggingSpan2Periods|
|v_input_int_4|26|displacement|
|v_input_int_5|2017|Start Year|
|v_input_int_6|true|Start Month|
|v_input_int_7|true|Start Day|
|v_input_int_8|2023|End Year|
|v_input_int_9|12|End Month|
|v_input_int_10|31|End Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-04 00:00:00
end: 2023-12-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
//Fukuiz

strategy(title='Fukuiz Octa-EMA + Ichimoku', shorttitle='Fuku octa strategy', overlay=true, process_orders_on_close=true, 
     default_qty_type= strategy.cash , default_qty_value=1000, currency=currency.USD, initial_capital=10000 ,commission_type = strategy.commission.percent,commission_value=0.25)


//OCTA EMA ##################################################


// Functions
f_emaRibbon(_src, _e1, _e2, _e3, _e4, _e5, _e6, _e7, _e8) =>
    _ema1 = ta.ema(_src, _e1)
    _ema2 = ta.ema(_src, _e2)
    _ema3 = ta.ema(_src, _e3)
    _ema4 = ta.ema(_src, _e4)
    _ema5 = ta.ema(_src, _e5)
    _ema6 = ta.ema(_src, _e6)
    _ema7 = ta.ema(_src, _e7)
    _ema8 = ta.ema(_src, _e8)
    [_ema1, _ema2, _ema3, _ema4, _ema5, _ema6, _ema7, _ema8]

showRibbon = input(true, 'Show Ribbon (EMA)')
ema1Len = input(5, title='EMA 1 Length')
ema2Len = input(11, title='EMA 2 Length')
ema3Len = input(15, title='EMA 3 Length')
ema4Len = input(18, title='EMA 4 Length')
ema5Len = input(21, title='EMA 5 Length')
ema6Len = input(24, title='EMA 6 Length')
ema7Len = input(28, title='EMA 7 Length')
ema8Len = input(34, title='EMA 8 Length')

[ema1, ema2, ema3, ema4, ema5, ema6, ema7, ema8] = f_emaRibbon(close, ema1Len, ema2Len, ema3Len, ema4Len, ema5Len, ema6Len, ema7Len, ema8Len)

//Plot

ribbonDir = ema8 < ema2
p1 = plot(ema1, color=showRibbon ? ribbonDir ? #1573d4 : color.new(#5d606b, 15) : na, linewidth=2, title='EMA 1')
p2 = plot(ema2, color=showRibbon ? ribbonDir ? #3096ff : color.new(#5d606b, 15) : na, linewidth=2, title='EMA 2')
plot(ema3, color=showRibbon ? ribbonDir ? #57abff : color.new(#5d606b, 15) : na, linewidth=2, title='EMA 3')
plot(ema4, color=showRibbon ? ribbonDir ? #85c2ff : color.new(#5d606b, 15) : na, linewidth=2, title='EMA 4')
plot(ema5, color=showRibbon ? ribbonDir ? #9bcdff : color.new(#5d606b, 30) : na, linewidth=2, title='EMA 5')
plot(ema6, color=showRibbon ? ribbonDir ? #b3d9ff : color.new(#5d606b, 30) : na, linewidth=2, title='EMA 6')
plot(ema7, color=showRibbon ? ribbonDir ? #c9e5ff : color.new(#5d606b, 30) : na, linewidth=2, title='EMA 7')
p8 = plot(ema8, color=showRibbon ? ribbonDir ? #dfecfb : color.new(#5d606b, 30) : na, linewidth=2, title='EMA 8')
fill(p1, p2, color.new(#1573d4, 85))
fill(p2, p8, color.new(#1573d4, 85))

//ichimoku##################################################

//color
colorblue = #3300CC
colorred = #993300
colorwhite = #FFFFFF
colorgreen = #CCCC33
colorpink = #CC6699
colorpurple = #6633FF

//switch
switch1 = input(false, title='Chikou')
switch2 = input(false, title='Tenkan')
switch3 = input(false, title='Kijun')

middleDonchian(Length) =>
    lower = ta.lowest(Length)
    upper = ta.highest(Length)
    math.avg(upper, lower)

//Functions
conversionPeriods = input.int(9, minval=1)
basePeriods = input.int(26, minval=1)
laggingSpan2Periods = input.int(52, minval=1)
displacement = input.int(26, minval=1)
Tenkan = middleDonchian(conversionPeriods)
Kijun = middleDonchian(basePeriods)
xChikou = close
SenkouA = middleDonchian(laggingSpan2Periods)
SenkouB = (Tenkan[basePeriods] + Kijun[basePeriods]) / 2

//Plot
A = plot(SenkouA[displacement], color=color.new(colorpurple, 0), title='SenkouA')
B = plot(SenkouB, color=color.new(colorgreen, 0), title='SenkouB')
plot(switch1 ? xChikou : na, color=color.new(colorpink, 0), title='Chikou', offset=-displacement)
plot(switch2 ? Tenkan : na, color=color.new(colorred, 0), title='Tenkan')
plot(switch3 ? Kijun : na, color=color.new(colorblue, 0), title='Kijun')
fill(A, B, color=color.new(colorgreen, 90), title='Ichimoku Cloud')

//Buy and Sell signals
fukuiz = math.avg(ema2, ema8)
white = ema2 > ema8
gray = ema2 < ema8
buycond = white and white[1] == 0
sellcond = gray and gray[1] == 0
bullish = ta.barssince(buycond) < ta.barssince(sellcond)
bearish = ta.barssince(sellcond) < ta.barssince(buycond)
buy = bearish[1] and buycond and fukuiz > SenkouA[displacement] and fukuiz > SenkouB
sell = bullish[1] and sellcond and fukuiz > SenkouA[displacement] and fukuiz > SenkouB
sell2=ema2 < ema8
buy2 = white and fukuiz > SenkouA[displacement] and fukuiz > SenkouB

//$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
//Back test

startYear = input.int(defval=2017, title='Start Year', minval=2000, maxval=3000)
startMonth = input.int(defval=1, title='Start Month', minval=1, maxval=12)
startDay = input.int(defval=1, title='Start Day', minval=1, maxval=31)
endYear = input.int(defval=2023, title='End Year', minval=2000 ,maxval=3000)
endMonth = input.int(defval=12, title='End Month', minval=1, maxval=12)
endDay = input.int(defval=31, title='End Day', minval=1, maxval=31)

start = timestamp(startYear, startMonth, startDay, 00, 00)
end = timestamp(endYear, endMonth, endDay, 23, 59)
period() => time >= start and time <= end ? true : false

if buy2 
    strategy.entry(id='long', direction=strategy.long, when=period(), comment='BUY')

if sell2
    strategy.close(id='long', when=period(), comment='SELL')




```

> Detail

https://www.fmz.com/strategy/434982

> Last Modified

2023-12-11 14:52:05
