
> Name

Dynamic-Channel-Moving-Average-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12472fbe51399e5028a.png)
[trans]
## Overview
This strategy is designed based on the trend following principles of dynamic channels and moving averages. It calculates the dynamic channel of price, determines the price trend direction through the upper and lower rails of the channel, and combines the moving average filter with price dispersion to generate trading signals. This strategy is suitable for short- to medium-term trend trading.
## Principle
This strategy is mainly based on the following principles:
1. Calculate dynamic price channels. The center line of the channel is calculated through the highest price and the lowest price. The upper track of the channel is the center line + the price dispersion moving average, and the lower track is the center line - the price dispersion moving average.
2. Determine the trend direction. When the price goes above the upper band, it is defined as bullish; when the price breaks below the lower band, it is defined as bearish.
3. Filter noise. Use a certain period of price dispersion moving average to filter the noise caused by random price fluctuations.
4. Generate trading signals. When bullish, a buy signal is generated when the closing price of the period is lower than the opening price; when bearish, a sell signal is generated when the closing price of the period is higher than the opening price.
## Advantages
This strategy has the following advantages:
1. Dynamic channels can capture price trends in real time;
2. Moving average filtering can reduce false signals;
3. Combine the trend direction and the K-line entity direction to generate trading signals to avoid being trapped.
## Risk
This strategy also has the following risks:
1. Improper selection of Params may lead to over-optimization;
2. It is easy to produce false signals during concussive consolidation;
3. Unable to predict violent price fluctuations.
Corresponding solutions:
1. Strict Params selection and testing;
2. Add filtering conditions to identify concussive consolidation;
3. Set stop loss and stop profit to control risks.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test the stability of different cycle parameters;
2. Increase the judgment strength of VOLUME or volatility indicators;
3. Determine entry and exit based on bands, channels, etc.
## Summarize
This strategy integrates the ideas of dynamic channels and moving average trend judgment, and performs well in capturing the trend direction in the short and medium term. However, there are also certain limitations, which require further testing and optimization to adapt to more market conditions.
||

## Overview

This strategy is designed based on the principle of dynamic channel and moving average trend tracking. It calculates the dynamic price channel, judges the trend direction through the upper and lower rails of the channel, and generates trading signals by combining the moving average to filter price volatility. This strategy is suitable for medium and short term trend trading.  

## Principle  

The main principles of this strategy are:

1. Calculate dynamic price channel. The channel middle line is calculated from highest price and lowest price. The upper rail is middle line + price volatility MA, and the lower rail is middle line - price volatility MA.

2. Judge trend direction. When price breaks through the upper rail, it is defined as bullish. When price breaks through the lower rail, it is defined as bearish.  

3. Filter noise. Use price volatility MA of a certain period to filter noise from random price fluctuations.

4. Generate trading signals. When bullish, a buy signal is generated when close price is lower than open price in that period. When bearish, a sell signal is generated when close price is higher than open price.

## Advantages

The advantages of this strategy are:  

1. Dynamic channel can capture price trend in real time.
2. MA filter can reduce false signals. 
3. Combining trend direction and K-line entity direction to generate trading signals avoids being trapped.

## Risks

The risks of this strategy are:

1. Improper Param selection may lead to overfitting.  
2. It is easy to generate wrong signals during sideways volatility.
3. It cannot predict extreme price fluctuations.

Solutions:

1. Strict Param selection and testing.
2. Add filter conditions to identify sideways. 
3. Set stop loss/profit to control risks.

## Optimization Directions

The strategy can be optimized in following aspects:

1. Test stability of different period Params.
2. Add VOLUME or volatility indicators to judge momentum. 
3. Combine bands, channels etc. to determine entry and exit.

## Summary  

This strategy integrates the ideas of dynamic channel and MA trend judgment, and performs well in capturing trend directions in medium and short term. But there are still some limitations, which need further testing and optimization to adapt more market situations.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|20|Period|
|v_input_4|true|Color|
|v_input_5|false|Show Bands|
|v_input_6|false|Show Background|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


//@version=2
strategy("Noro's Bands Strategy v1.0", shorttitle = "NoroBands str 1.0", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value=100.0, pyramiding=0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
len = input(20, defval = 20, minval = 2, maxval = 200, title = "Period")
color = input(true, "Color")
needbb = input(false, defval = false, title = "Show Bands")
needbg = input(false, defval = false, title = "Show Background")
src = close

//PriceChannel 1
lasthigh = highest(src, len)
lastlow = lowest(src, len)
center = (lasthigh + lastlow) / 2

//dist
dist = abs(src - center)
distsma = sma(dist, len)
hd = center + distsma
ld = center - distsma

//Trend
trend = close < ld and high < hd ? -1 : close > hd and low > ld ? 1 : trend[1]

//Lines
colo = needbb == false ? na : black
plot(hd, color = colo, linewidth = 1, transp = 0, title = "High band")
plot(center, color = colo, linewidth = 1, transp = 0, title = "center")
plot(ld, color = colo, linewidth = 1, transp = 0, title = "Low band")

//Background
col = needbg == false ? na : trend == 1 ? lime : red
bgcolor(col, transp = 90)

//up =  and trend == 1 ? 1 : 0
//dn =  and trend == -1 ? 1 : 0 

up = close < hd and trend == 1 and (close < open or color == false) ? 1 : 0
dn = close > ld and trend == -1 and (close > open or color == false) ? 1 : 0 

longCondition = up == 1
if (longCondition)
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na)

shortCondition = dn == 1
if (shortCondition)
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na)
```

> Detail

https://www.fmz.com/strategy/442523

> Last Modified

2024-02-22 15:51:48
