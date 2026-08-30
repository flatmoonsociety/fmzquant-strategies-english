
> Name

Multi-Timeframe Trend Tracking Intraday Scalping StrategyMulti-Timeframe-Trend-Tracking-Intraday-Scalping-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13655b7dbfe36b176b9.png)
[trans]


## Overview
This strategy combines the moving average indicators of multiple time frames to achieve trend consistency judgment between multiple time frames, and adopts scalping operation strategies within the day to pursue the trend and obtain profits.
## Strategy Principle
This strategy uses 8-period and 20-period moving averages in four time frames of 5 minutes, 15 minutes, 30 minutes and 60 minutes to construct trading signals. A buy signal is generated when the shorter-term 8-day moving average crosses the 20-day moving average; a sell signal is generated when the 8-day moving average crosses below the 20-day moving average.
The strategy requires that the trading signals in the 5-minute, 15-minute, 30-minute and 60-minute time frames must be consistent before issuing a trading order. That is to say, only when the moving averages of these four time frames meet the buy signal or sell signal, the buy or sell operation will be carried out.
After entering the position, the strategy will set a take-profit order at a fixed profit point to achieve intraday scalping operations.
Specifically, the strategy obtains moving average data in different time frames by calling the security function. Calculate the difference between the 8-day and 20-day moving averages at 5 minutes, 15 minutes, 30 minutes and 60 minutes, and draw the difference curve.
The buy and sell signals are determined based on whether the difference curve crosses the zero axis. And set multiple flags islong and isshort to record trading signals in each time frame. Finally, entry and exit orders are issued when the status of islong and isshort meets the requirements.
After entering the market, the strategy sets a fixed point take-profit through the strategy.exit function to implement scaling operations.
## Advantage Analysis
This strategy has the following advantages:
1. Multi-time frame design, through comprehensive judgment of different cycle indicators, can effectively filter out false calls and reduce trading frequency.
2. Intraday scalping strategy and Profit optimization can continuously obtain small profit accumulation.
3. The code structure is clear, each part has clear functions, and is easy to understand and optimize.
4. Reasonable conditions can effectively control transaction risks.
## Risk Analysis
This strategy also has certain risks:
1. Although the multi-time frame design can filter some noise, it may also miss some details, resulting in insignificant trend changes.
2. Intraday scalping brings frequent transactions, and transaction cost control needs to be considered.
3. The setting of fixed take-profit points is not flexible enough and cannot be adjusted according to market changes.
4. If you rely on indicators to generate trading signals, you may be fooled.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add more indicator judgments in different cycle time frames to make signals more stable and reliable.
2. Optimize the profit-taking strategy and dynamically set the profit-taking point based on ATR.
3. Add additional conditions to filter entry opportunities, such as increased trading volume, breakthrough of historical extreme values, etc.
4. Optimize the period parameters of the moving average and find the best parameter combination.
5. Increase the reliability of the machine learning model’s judgment of indicator signals to avoid arbitrage.
## Summarize
Overall, this strategy is a typical multi-time frame trend following strategy, which uses scalping to make profits within the day. The strategy ideas are clear and the code structure is reasonable, which is worthy of further testing and optimization. With certain optimization and adjustments, this strategy can become a very practical intraday scalping strategy template.
||
## Overview

This strategy combines moving average indicators across multiple timeframes to determine trend consistency and takes scalping actions during the day to follow the trend and make profits.

## Strategy Logic

This strategy uses 8-period and 20-period moving averages on the 5-minute, 15-minute, 30-minute and 60-minute timeframes to generate trading signals. A buy signal is generated when the 8-period MA crosses above the 20-period MA. A sell signal is generated when the 8-period MA crosses below the 20-period MA.

The strategy requires consistent signals across the four timeframes before issuing a trade order. A buy or sell order is placed only when the moving averages align on all four timeframes. 

Once entered into a position, the strategy sets a fixed profit target to take profits intraday.

Specifically, the strategy uses the security() function to retrieve MA values from different timeframes. It calculates the difference between the 8-period and 20-period MAs on the 5-min, 15-min, 30-min and 60-min charts. 

Buy and sell signals are determined by whether the difference line crosses above/below the zero line. Multiple islong and isshort flags are used to record the signal on each timeframe. Orders are placed when the islong and isshort conditions are met.

After entering a trade, the strategy uses strategy.exit() to set a fixed profit target for scalping.

## Advantage Analysis

The advantages of this strategy include:

1. Multi-timeframe design filters noise and reduces trade frequency. 

2. Intraday scalping with profit optimization accumulates small gains consistently.

3. Clear code structure, easy to understand and optimize.

4. Reasonable conditions help control risk.

## Risk Analysis

Potential risks of this strategy:

1. Multi-timeframe may miss subtle trend changes.

2. Frequent scalping trades increase costs.

3. Fixed profit target lacks flexibility. 

4. Depends on indicators, risks being fooled.

## Optimization Directions

Possible optimizations:

1. Add more timeframes for more robust signals.

2. Dynamic profit target based on ATR.

3. Additional filters like volume increase or history extremes.

4. Optimize MA periods for best parameters. 

5. Add machine learning to judge signal reliability.

## Summary

Overall this is a typical multi-timeframe trend tracking strategy using intraday scalping. The logic is clear and code well structured. With proper optimization it can become a very practical scalping strategy template.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Zeige alle (Show all) Candles/Bars?|
|v_input_2|52|Profit|
|v_input_3|2e-05|ATR|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-09 00:00:00
end: 2023-11-15 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title="PeBAS $JPY Scalper 15m ",overlay=true) 
zeigeallebars= input(false, title="Zeige alle (Show all) Candles/Bars?")
profitwert=input(52, title="Profit")
myatr=  input(title="ATR", type=float, defval=0.00002, minval=0.00001,step=0.00001)


//Plot  EMA-Differenz Aktueller Timeframe

dif=(ema(close,8)+ema(close,20))/2
mcolor=ema(close,8) > ema(close,20) ? green : red
bs = ema(close,8) > ema(close,20) ? true : false
ThisATR=atr(16)

//trans = zeigeallebars == true ? 00 : 100
//plot(dif,"dif",color=mcolor,linewidth=6,transp=trans)


//1M EMA
htf_ma1Mema8 = ema(close, 5)
htf_ma1Mema20 = ema(close, 20)
ema81m=request.security(syminfo.tickerid, "1", htf_ma1Mema8)
ema201m=request.security(syminfo.tickerid, "1", htf_ma1Mema20)
dif1M = (ema81m + ema201m) / 2
Close1M = request.security(syminfo.tickerid, "1", close)
color1=ema81m > ema201m ? green : red
//plot(dif1M,"dif",color1,linewidth=6)
//plotshape(1, style=shape.cross, color=color1,location=location.top)
ls1 = ema81m > ema201m ? 1 : 0



//5M EMA

htf_ma5Mema8 = ema(close, 8)
htf_ma5Mema20 = ema(close, 20)
ema85m=request.security(syminfo.tickerid, "5", htf_ma5Mema8)
ema205m=request.security(syminfo.tickerid, "5", htf_ma5Mema20)
dif5M = (ema85m + ema205m) / 2
 
color5=ema85m > ema205m ? green : red
plot(dif5M,"dif",color5,linewidth=5)
ls5 = ema85m > ema205m ? 1 : 0
alert1= ema85m > ema205m and ema85m[1] < ema205m[1] ? 1 : 0
islong5 = ema85m > ema205m ? 1 : 0
isshort5 = ema85m < ema205m ? 1 : 0

//15M EMA

htf_ma15Mema8 = ema(close, 8)
htf_ma15Mema20 = ema(close, 20)
ema815m=request.security(syminfo.tickerid, "15", htf_ma15Mema8)
ema2015m=request.security(syminfo.tickerid, "15", htf_ma15Mema20)
dif15M = (ema815m + ema2015m) / 2
 
color15=ema815m > ema2015m ? green : red
plot(dif15M,"dif",color15,linewidth=3)
ls15= ema815m > ema2015m ? 1 : 0
alert2= ema815m > ema2015m and ema815m[1] < ema2015m[1] ? 1 : 0
islong15 = ema815m > ema2015m ? 1 : 0
isshort15 = ema815m < ema2015m ? 1 : 0





//30M EMA
htf_ma30Mema8 = ema(close, 8)
htf_ma30Mema20 = ema(close, 20)
ema830m=request.security(syminfo.tickerid, "30", htf_ma30Mema8)
ema2030m=request.security(syminfo.tickerid, "30", htf_ma30Mema20)
dif30M = (ema830m + ema2030m) / 2
 
color30=ema830m > ema2030m ? green : red
ls30= ema830m > ema2030m ?1 : 0
islong30 = ema830m > ema2030m ? 1 : 0
isshort30 = ema830m < ema2030m ? 1 : 0



//60M EMA

htf_ma60Mema8 = ema(close, 8)
htf_ma60Mema20 = ema(close, 20)
ema860m=request.security(syminfo.tickerid, "60", htf_ma60Mema8)
ema2060m=request.security(syminfo.tickerid, "60", htf_ma60Mema20)
dif60M = (ema860m + ema2060m) / 2
 
color60=ema860m > ema2060m ? green : red
ls60= ema860m > ema2060m ?1 : 0

islong60 = ema860m > ema2060m ? 1 : 0
isshort60 = ema860m < ema2060m ? 1 : 0

plot(dif60M,"dif",color60,linewidth=3,transp=70)

islong = islong5 ==1 and islong15 ==1 and islong60 ==1 and year > 2017 ? 1 : 0
isshort = isshort5 ==1 and isshort15 ==1 and  isshort60 ==1 and year > 2017 ? 1 : 0


condition2l= 0 
condition2s = 0

c= alert1 == alert2  and alert1[1] != alert2[1] ? 1 : 0
alertcondition(c, title='Da tat sich was ', message='Da tat sich was!')

strategy.entry("enter long", strategy.long,1,when = islong ==1 and islong[1] == 0  ) 
strategy.entry("enter short", strategy.short,1,when = isshort == 1  and isshort [1] == 0) 
strategy.exit("close",profit=profitwert)
strategy.exit("close",profit=profitwert)




```

> Detail

https://www.fmz.com/strategy/432362

> Last Modified

2023-11-16 17:47:06
