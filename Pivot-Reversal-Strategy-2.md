
> Name

Pivot-Reversal-Strategy Pivot-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The pivot support pressure reversal strategy is a breakout trading strategy that combines the concept of pivot support and pressure levels and performs reverse operations when the price breaks through the pivot level. This strategy is simple to understand and easy to implement. It is a short-term breakthrough trading strategy.
## Strategy Principle
This strategy first calculates the highest price and lowest price of the specified period (such as 4 K lines) as the axis support level and axis pressure level. Then monitor the price trend in real time to determine whether the price breaks through the axis level. Specifically:
1. Use pivothigh() function to calculate the highest price and obtain the axis pressure level swh
2. Use pivotlow() function to calculate the lowest price and obtain the pivot support level swl
3. When the price rises and breaks through the axis pressure level swh, do a short trade (strategy.short)
4. When the price falls and breaks through the pivot support level swl, do a long trade (strategy.long)
The logic of this strategy is simple and clear, and the main purpose is to judge when the price breaks through the axis level and carry out reverse operations. At the same time, the strategy adds trading time control logic and only trades within the specified time range, thereby avoiding overnight risks.
## Advantage Analysis
This pivot reversal strategy has the following advantages:
1. The strategy idea is simple, easy to understand and implement, and is suitable for beginners to learn;
2. Use the pivot position to determine the trend reversal point and be less susceptible to short-term market noise;
3. Only trade when the pivot level is broken to avoid unnecessary trading frequency;
4. Added trading time control to help avoid risks caused by overnight;
5. The amount of code is small, the resource usage is low, and it is easy to optimize strategies.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. The pivot position cannot 100% predict the price trend, and there is a possibility of false breakthrough;
2. Only relying on the axis position to judge the trend reversal may easily lead to premature entry, and other indicators should be used to determine trading signals;
3. Failure to consider the trend of the market and the characteristics of individual stocks, and there are systemic risks;
4. When the support pressure level is close, the breakthrough effect may not be obvious, and the stop loss range should be appropriately relaxed.
In order to control risks, it is recommended that you consider adding a trailing stop loss when optimizing, grasp the general trend direction, and cooperate with stock and market selection to reduce the false breakthrough rate.
## Optimization direction
Considering the risks of this strategy, optimization can be carried out in the following directions in the future:
1. Optimize the axis position parameters, such as increasing the calculation period length, to see if the breakthrough success rate can be improved;
2. Add a trailing stop loss mechanism to track the general trend and reduce the risk of reversal;
3. Combine with other indicators such as MACD to judge the trend and avoid the risks caused by false breakthroughs;
4. Classify stocks, distinguish different characteristics, and set different parameters;
5. Optimize the trading time period and consider the trading hours of different time zones such as US stocks and Hong Kong stocks;
6. Consider the overall trend of the market and trade selectively.
## Summarize
Overall, the pivot support pressure reversal strategy is a simple breakout strategy that is very suitable for beginners to learn. It uses the axis position to judge the reversal timing, and the strategic ideas are clear and easy to understand. At the same time, there are also some risks, and parameters, stop losses, trading times, etc. need to be optimized, and supplemented by other technical indicators. If the risk can be controlled, it can become a very practical short-term trading strategy.
|| 

## Overview 

The Pivot Reversal Strategy is a breakout trading strategy that combines the concept of pivot support and resistance levels. It takes reverse positions when the price breaks through the pivot levels. The strategy is simple and easy to implement, making it a short-term breakout trading strategy.

## Strategy Logic

The strategy first calculates the highest and lowest prices over a specified period (e.g. 4 bars) as the pivot resistance and support levels. It then monitors price action in real-time and determines if the price breaks through the pivot levels. Specifically:

1. Use the pivothigh() function to calculate the highest price for the pivot resistance swh
2. Use the pivotlow() function to calculate the lowest price for the pivot support swl  
3. Go short (strategy.short) when prices break above the pivot resistance swh
4. Go long (strategy.long) when prices break below the pivot support swl

The strategy logic is simple and clear - take reverse positions when prices break pivotal levels. It also incorporates trading hour control to avoid overnight risks.

## Advantage Analysis

The pivot reversal strategy has several advantages:

1. The strategy idea is simple and easy to understand for beginners.
2. Using pivot levels to determine trend reversal is robust against short-term market noise.
3. Only trading on pivotal breakouts avoids excessive trade frequencies. 
4. Trading hour control helps avoid overnight risks.
5. The concise code is easy to optimize.

## Risk Analysis

There are also some risks to note:

1. Pivot levels do not guarantee perfect trend prediction and false breakouts are possible.
2. Pivotal signals alone may cause premature entry. Other indicators should confirm the trading signal.
3. It does not consider market regime and individual stock traits, leading to systemic risks. 
4. Blurred support and resistance increase the chance of failure in breakouts.

To control risks, recommended optimizations include using moving stop loss to follow the major trend, pairing stocks with market conditions, and reducing false breakout rates.

## Optimization Directions

Considering the risks, future optimizations can focus on:

1. Optimizing pivot parameters like increasing calculation period to improve success rate.

2. Adding moving stop loss to follow the major trend and reduce reversal risks.

3. Incorporating other indicators like MACD to confirm trend and avoid false breakouts.

4. Classifying stocks by traits and setting unique parameters.

5. Optimizing trading hours for different markets like US and HK stocks. 

6. Considering overall market trend for selective trading.

## Conclusion

Overall, the Pivot Reversal Strategy is a great simple breakout strategy for beginners to learn. It identifies reversal levels cleanly using pivot points. While risks exist, optimizing parameters, stop loss, trading hours and incorporating indicators can turn it into a robust short-term trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|From Month|
|v_input_2|true|From Day|
|v_input_3|2018|From Year|
|v_input_4|true|To Month|
|v_input_5|true|To Day|
|v_input_6|9999|To Year|
|v_input_7|4|leftBars|
|v_input_8|2|rightBars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-18 00:00:00
end: 2023-09-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Pivot Reversal Strategy", overlay=true)

// === BACKTEST RANGE ===
FromMonth = input(defval = 2, title = "From Month", minval = 1)
FromDay   = input(defval = 1, title = "From Day", minval = 1)
FromYear  = input(defval = 2018, title = "From Year", minval = 2014)
ToMonth   = input(defval = 1, title = "To Month", minval = 1)
ToDay     = input(defval = 1, title = "To Day", minval = 1)
ToYear    = input(defval = 9999, title = "To Year", minval = 2014)


leftBars = input(4)
rightBars = input(2)

swh = pivothigh(leftBars, rightBars)
swl = pivotlow(leftBars, rightBars)

swh_cond = not na(swh)

hprice = 0.0
hprice := swh_cond ? swh : hprice[1]

le = false
le := swh_cond ? true : (le[1] and high > hprice ? false : le[1])

if (le)
    strategy.entry("PivRevLE", strategy.long, comment="PivRevLE", stop=hprice + syminfo.mintick)

swl_cond = not na(swl)

lprice = 0.0
lprice := swl_cond ? swl : lprice[1]


se = false
se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])

if (se)
    strategy.entry("PivRevSE", strategy.short, comment="PivRevSE", stop=lprice - syminfo.mintick)

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/427907

> Last Modified

2023-09-26 17:38:56
