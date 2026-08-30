
> Name

Trend following strategy based on CCI indicatorCCI-Dual-Timeframe-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/5604b8fba9dce37b2a.png)
[trans]


## Overview
This strategy is a trend following strategy based on the CCI indicator. It uses two CCI indicators with different periods for trading signal generation. Specifically, it will monitor whether a shorter-period CCI indicator breaks through a longer-period CCI indicator, and decide to go long or short based on the direction of the breakthrough.
## Strategy Principle
The core logic of this strategy is:
1. Define two CCI indicators, ci1 is 14 periods and ci2 is 56 periods.
2. When ci1 breaks through ci2 upward, go long
3. When ci1 breaks through ci2 downward, go short
4. After the trading signal is sent, the closing of the position is determined by the values ​​of ci1 and ci2.
The specific rules for going long are:
1. ci1 crosses above ci2, that is, short-period CCI crosses above long-period CCI
2. Stop loss conditions: ci1<-50 and change rate<0 or ci1 falls below -100
The specific rules for short selling are:
1. ci1 crosses below ci2, that is, the short-period CCI crosses below the long-period CCI
2. Stop loss conditions: ci1>100 and change rate>0 or ci2 crosses 100
It can be seen that this strategy utilizes the sensitivity of shorter-period CCI and the stability of longer-period CCI to achieve trend identification and tracking.
## Strategic Advantages
This strategy has the following advantages:
1. Take advantage of the CCI indicator to effectively identify trends
2. Double CCI design can filter out some noise transactions
3. Through the combination of long and short period CCI indicators, risks can be controlled while tracking trends
4. The policy rules are simple and clear, easy to understand and implement
5. Strong configurability, CCI cycle and stop loss conditions can be customized
## Strategy Risk
There are also some risks with this strategy:
1. The CCI indicator has weak ability to identify sideways and oscillating market conditions.
2. Long-term and short-term CCI may divergence, resulting in incorrect trading signals.
3. Improper setting of stop loss conditions may result in larger losses.
4. Improper parameter settings will also have a greater impact on strategy returns.
Solutions corresponding to risks:
1. You can combine other indicators to judge the market and avoid trading in volatile market conditions.
2. Add filtering conditions to avoid false signals caused by long and short period CCI divergence
3. Optimize and test different stop loss conditions
4. Select appropriate parameter combinations through backtesting and parameter optimization
## Strategy optimization direction
Areas where this strategy can be further optimized include:
1. Add other indicator judgments to form a more SYSTEM trading system
2. Test the difference in income between different weekdays and sessions
3. Combine machine learning methods to find better parameters
4. Adjust parameters according to the characteristics of different varieties
5. Optimize the conditions for opening and closing positions
## Summarize
Overall, this strategy is a simple trend following strategy based on the breakthrough of the long and short cycle CCI indicator. It can effectively identify trend direction and track trends. At the same time, risks are controlled through stop loss and other means. This strategy is simple and practical, with flexible parameter adjustment. It can be used as an introductory strategy for quantitative trading. Through further optimization and combination, a more powerful trading system can be formed.
|| 

## Overview

This strategy is a trend following strategy based on the CCI indicator. It generates trading signals by monitoring the crossover between two CCIs of different timeframes. Specifically, it will detect if a shorter period CCI breaks through a longer period CCI and determine long or short positions based on the breakthrough direction.

## Strategy Logic   

The core logic of this strategy is:  

1. Define two CCIs, ci1 as 14 periods, ci2 as 56 periods  
2. When ci1 breaks above ci2, go long
3. When ci1 breaks below ci2, go short  
4. Use the values of ci1 and ci2 to determine exits after signals triggered  

Specific long rules:  

1. ci1 breaks above ci2, the shorter period CCI above longer period CCI
2. Stop loss condition: ci1 <-50 and change rate < 0 or ci1 breaks below -100   

Specific short rules:

1. ci1 breaks below ci2, the shorter period CCI below longer period CCI   
2. Stop loss condition: ci1 > 100 and change rate > 0 or ci2 breaks above 100  

As we can see, this strategy takes advantage of the sensitivity of shorter period CCI and the stability of longer period CCI to identify and follow trends.  

## Advantages

The advantages of this strategy:   

1. Effectively identifies trends using the strength of CCI indicator  
2. Dual CCI design filters some noise trades  
3. The combination of long and short period CCIs controls risk while following trends  
4. Simple and clear strategy rules, easy to understand and implement
5. Highly configurable, both CCI periods and stop loss conditions are customizable   

## Risks  

There are also some risks:  

1. Weak ability to identify range-bound and volatile markets using CCI
2. Divergence may happen between long and short period CCIs, causing wrong signals
3. Improper stop loss setting may lead to huge loss  
4. Inappropriate parameter tuning also largely impacts strategy profitability   

Solutions:  

1. Incorporate other indicators to determine market condition, avoid trading in volatile period   
2. Add filters to avoid errors from CCI divergence  
3. Optimize and test different stop loss levels  
4. Find suitable parameter sets through backtesting and tuning  

## Optimization Directions   

Areas that the strategy can be further optimized:

1. Add more indicators to build a more systematic trading system  
2. Test profitability difference between weekdays and sessions  
3. Search for better parameters using machine learning  
4. Tune parameters for different products  
5. Optimize entry and exit rules  

## Conclusion  

In conclusion, this is a simple trend following strategy based on CCI crossover. It can effectively identify trend direction and follow trends. Meanwhile it controls risk via stop loss. This strategy is simple, practical, flexible in parameter tuning, and can serve as a starter quant strategy. It can be enhanced into more powerful system via further optimization and combination.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|shortlength|
|v_input_2|56|longlength|
|v_input_3|2|aa|
|v_input_4|75|Ss|
|v_input_5|10|len|
|v_input_6|9|lenTurn|
|v_input_7|26|lenStd|
|v_input_8|true|from day|
|v_input_9|true|from month|
|v_input_10|2019|from yr|
|v_input_11|13|to day|
|v_input_12|12|to month|
|v_input_13|2019|to yr|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-24 00:00:00
end: 2023-11-23 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title="my work",calc_on_order_fills=true,currency=currency.USD, default_qty_type=strategy.percent_of_equity,commission_type=strategy.commission.percent)


source = close
shortlength=input(14)
longlength=input(56)
aa=input(2)
Ss=input(75)

//Cci part
ci1=cci(source,shortlength)   //4시간봉의 기본 cci
ci2=cci(source,longlength)   //4시간봉에서 12시봉의 cci 무빙측정

//오린간 선생님의 WT + ichimoku
len = input(10)
lenTurn = input(9)
lenStd = input(26)

wtm_e(so, l) =>
    esa = ema(so, l)
    d = ema(abs(so - esa), l)
    ci = (so - esa) / (0.015 * d)
    ema(ci, l*2+1)

alh(len) => avg(lowest(len), highest(len))
alh_src(src, len) => avg(lowest(src, len), highest(src, len))

wt = wtm_e(close,len)
turn = alh_src(wt, lenTurn)
std = alh_src(wt, lenStd)

cnt = 0
if wt > turn
    cnt:=cnt+1
if wt > std
    cnt:=cnt+1


//100,-100선
h0 = hline(100)
h1 = hline(-100)

//plot(ci,color=green)
// plot(k,color=green)
// plot(d,color=red)
plot(ci1,color=green)
plot(ci2,color=red)

plot(0,color=black)
plot(100,color=black)
plot(-100,color=black)

fill(h0,h1,color=purple,transp=95)

bgcolor(cnt==0 ? red : cnt==1 ? blue : cnt == 2 ? green : na, transp = Ss)

//기간조정

Fromday = input(defval=1, title="from day", minval=1, maxval=31)
FromMonth = input(defval=1, title="from month", minval=1, maxval=12)
FromYr = input(defval=2019, title="from yr", minval=1970)

Today = input(defval=13, title="to day", minval=1, maxval=31)
ToMonth = input(defval=12, title="to month", minval=1, maxval=12)
ToYr = input(defval=2019, title="to yr", minval=1970)

startDate = timestamp(FromYr, FromMonth, Fromday, 00, 00)
finishDate = timestamp(ToYr, ToMonth, Today, 00, 00)
Time_cond = true


/////롱

if  crossover(ci1,ci2) and change(ci2)>0 and Time_cond
    strategy.entry("go", strategy.long, comment="go")
    
strategy.close("go", (ci2<0 and ci1 <-50 and change(ci1)<0) or (crossunder(ci1,-100) and strategy.openprofit<0) and change(cnt)<0)



/////숏

if  (crossunder(ci1,ci2) and change(ci2)<0 and falling(ci1,aa)) and Time_cond
    strategy.entry("die", strategy.short, comment="die")
    
strategy.close("die", (ci2>0 and ci1 > 100 and change(ci1)>0) or (crossover(ci2,100) and strategy.openprofit<0) and change(cnt)>0)
```

> Detail

https://www.fmz.com/strategy/433076

> Last Modified

2023-11-24 10:53:07
