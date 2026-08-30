
> Name

Trend following strategy Ichimoku-Trend-Following-Strategy based on Ichimoku Balance Table
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10083a8ec23e2fd4c55.png)
[trans]

## Overview
This strategy is based on the design of Ichimoku technical indicators and adopts trend tracking and balanced breakthrough trading methods, aiming to capture medium and long-term price trends and achieve stable profits.
## Strategy Principle
The strategy uses the five lines of the Ichimoku Balance Sheet - turning line, base line, front line, leader line and delay line to determine price trends and support and resistance. The specific judgment rules are as follows:
1. When the closing price crosses the baseline and the trend of the baseline is uneven, a buy signal is generated.
2. When the closing price crosses the baseline and the trend of the baseline is uneven, a sell signal is generated.
3. When the closing price is higher than Yunluan, the liquidity is better and positions are allowed to be opened.
4. When the closing price is lower than Yunluan, the liquidity is poor and it is prohibited to open a position.
5. The delay line crosses the closing price to generate a buy signal.
6. The delay line crosses below the closing price to generate a sell signal.
The final entry time is determined after comprehensive judgment of the above trading signals.
## Advantage Analysis
This strategy has the following advantages:
1. Use the Ichimoku Balance Sheet to determine trends, which can filter out market noise and lock in mid- to long-term trends.
2. Combined with Yunluan to judge the liquidity situation, the risk of opening a position can be avoided.
3. The delay line serves as a confirmation signal to avoid false breakthroughs.
4. The rules are simple, clear and easy to implement.
## Risk Analysis
This strategy also has the following risks:
1. Improper parameter settings may lead to missed trading opportunities.
2. When the trend mutates, the judgment lags behind and the loss cannot be stopped in time.
3. There is a greater risk of loss for long positions.
The above risks can be solved by optimizing parameter settings, combining other indicators to judge trend changes, and strictly stopping losses.
## Optimization direction
Strategies can also be optimized from the following aspects:
1. Optimize the parameters of the Ichimoku balance table and find the best combination.
2. Add volume and price indicator filtering to avoid trend misalignment.
3. Combine with volatility indicators to determine reversal points.
4. Add a machine learning model to determine the trend status.
## Summarize
This strategy uses the Ichimoku Balance Sheet to determine price trends and liquidity conditions, and adopts trend tracking mode, which can effectively filter out noise and capture mid- and long-term trends. The risk of retracement is small, and it is suitable for mid- and long-term positions. By further optimizing parameter settings, adding auxiliary filtering indicators, and mining trend turning signals, the strategy Profit Factor can be improved.
|| 

## Overview

This strategy is designed based on the Ichimoku indicator for trend following and equilibrium breakout trading, aiming to capture medium-to-long term price trends for steady profits.  

## Strategy Logic

The strategy utilizes the five lines of Ichimoku - Tenkan-sen, Kijun-sen, Senkou Span A, Senkou Span B and Chikou Span to determine price trend and support/resistance levels. The specific entry rules are:

1. When the close crosses over Kijun-sen and Kijun-sen is not flat, a buy signal is triggered.  
2. When the close crosses under Kijun-sen and Kijun-sen is not flat, a sell signal is triggered.
3. When the close is above the cloud, the liquidity is good for taking positions.  
4. When the close is below the cloud, the liquidity is low and taking positions should be avoided.
5. When Chikou Span crosses over the close, a buy signal is triggered.
6. When Chikou Span crosses under the close, a sell signal is triggered.

The above trading signals are combined to determine the final entry timing.  

## Advantage Analysis 

The advantages of this strategy include:

1. Using Ichimoku to determine trend can filter out market noise and capture medium-to-long term trends.
2. Incorporating cloud condition avoids taking positions in poor liquidity.  
3. Chikou Span acts as confirmation to avoid false breakout. 
4. The rules are simple and clear for implementation.  

## Risk Analysis

The risks of this strategy involve:

1. Inappropriate parameter settings may lead to missing trading opportunities.
2. Trend judgment may lag when trend mutates, unable to cut loss in time.
3. Higher loss risk for long positions.

These risks can be addressed by optimizing parameters, combining with other indicators to determine trend change, and strict stop loss.

## Optimization Directions 

The strategy can be further optimized from the following aspects:

1. Optimize Ichimoku parameters to find the best combination.  
2. Add price & volume filters to avoid trend deviation.
3. Incorporate volatility indicators to identify reversal points.  
4. Add machine learning models to determine trend status.

## Summary

This strategy leverages Ichimoku to determine price trend and liquidity conditions for trend following, which can effectively filter out noise and capture medium-to-long term trends with smaller drawdowns. Further optimizations on parameter tuning, adding auxiliary filters, and identifying trend reversal signals can improve the strategy's Profit Factor.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|From Month|
|v_input_2|true|From Day|
|v_input_3|2017|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|6|KijunSen Lag|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-04 00:00:00
end: 2023-12-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("My Ichimoku Strat", overlay=true,default_qty_type=strategy.percent_of_equity, default_qty_value=100, initial_capital=1000, currency=currency.EUR)
// === BACKTEST RANGE ===
FromMonth = input(defval = 1, title = "From Month", minval = 1)
FromDay   = input(defval = 1, title = "From Day", minval = 1)
FromYear  = input(defval = 2017, title = "From Year", minval = 2014)
ToMonth   = input(defval = 1, title = "To Month", minval = 1)
ToDay     = input(defval = 1, title = "To Day", minval = 1)
ToYear    = input(defval = 9999, title = "To Year", minval = 2014)

// === SERIES SETUP ===
//**** Inputs *******
KijunSenLag = input(6,title="KijunSen Lag",minval=1)

//Kijun-sen
//Support resistance line, buy signal when price crosses it
KijunSen = sma((high+low)/2,26)
buy2 = crossover(close,KijunSen) and (rising(KijunSen,KijunSenLag) or falling(KijunSen,KijunSenLag))
sell2= crossunder(close,KijunSen) and (rising(KijunSen,KijunSenLag) or falling(KijunSen,KijunSenLag))


//Tenkan-Sen
TenkanSen = sma((high+low)/2,9)

//Senkou Span A 
SenkouSpanA = (KijunSen + TenkanSen)/2

//Senkou Span B 
SenkouSpanB = sma((high+low)/2,52)

//Cloud conditions : ignore buy if price is under the cloud
// Huge cloud means safe support and resistance. Little cloud means danger.
buy3 = close > SenkouSpanA and close > SenkouSpanB
sell3 = close < SenkouSpanA and close < SenkouSpanB


//Chikou Span
//Buy signal : crossover(ChikouSpan,close)
//Sell Signal : crossunder(ChikouSpan,close)
ChikouSpan = close
buy1=crossover(ChikouSpan,close[26])
sell1=crossunder(ChikouSpan,close[26])

plotshape(buy1,style=shape.diamond,color=lime,size=size.small)
plotshape(sell1,style=shape.diamond,color=orange,size=size.small)

//Alerts

buyCompteur = -1
buyCompteur := nz(buyCompteur[1],-1)
buyCompteur := buy2 or buy3 ? 1 : buyCompteur
buyCompteur := buyCompteur > 0 ? buyCompteur + 1 : buyCompteur
buyCompteur := sell2 or sell3 ? -1 : buyCompteur

sellCompteur = -1
sellCompteur := nz(sellCompteur[1],-1)
sellCompteur := sell2 or sell3 ? 1 : sellCompteur
sellCompteur := sellCompteur > 0 ? sellCompteur + 1 : sellCompteur
sellCompteur := buy2 or buy3 ? -1 : sellCompteur

sell= sell2 and sell3 or (sell1 and buyCompteur <= 8)
buy=buy2 and buy3 or (buy1 and sellCompteur <=8)
plotchar(buy,char='B',size=size.small,color=lime)
plotchar(sell,char='S',size=size.small,color=orange)

//plots
plot(KijunSen,title="Kijun-Sen",color=blue,linewidth=4)
plot(TenkanSen,title="Tenkan-Sen",color=red,linewidth=2)
cloudA = plot(SenkouSpanA,title="cloud A", color=lime,offset=26,linewidth=2)
cloudB = plot(SenkouSpanB,title="cloud B", color=orange,offset=26,linewidth=2)
plot(ChikouSpan,title="lag span",color=fuchsia, linewidth=2,offset=-26)
//plot()
fill(cloudA,cloudB,color=SenkouSpanA>SenkouSpanB?lime:orange)
//plot(close,color=silver,linewidth=4)

// === ALERTS ===
strategy.entry("L", strategy.long, when=(buy and (time > timestamp(FromYear, FromMonth, FromDay, 00, 00)) and (time < timestamp(ToYear, ToMonth, ToDay, 23, 59))))
strategy.close("L", when=(sell and (time < timestamp(ToYear, ToMonth, ToDay, 23, 59))))
```

> Detail

https://www.fmz.com/strategy/434984

> Last Modified

2023-12-11 15:00:29
