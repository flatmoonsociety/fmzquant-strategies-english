
> Name

Crossing-the-Breakout-Strategy Crossing-the-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The moving average crossover strategy is a very common quantitative trading strategy. This strategy uses the golden cross of the moving average to determine the trend and make profits. When the short-term moving average crosses the long-term moving average, it indicates that the stock price has begun to rise, and you can go long; when the short-term moving average crosses below the long-term moving average, it indicates that the stock price has begun to fall, and you can go short.
## Strategy Principle
This strategy is based on the golden cross of the moving average to determine the timing of buying and selling. The code uses two Boolean input parameters `upOrDown` and `longOrShort` to determine long and short positions; uses the `percentInput` ​​input parameter to set the threshold percentage of stock price changes; uses the `closePositionDays` input parameter to set the number of days the position is held.
The core logic of the strategy is: calculate today's increase or decrease relative to yesterday's, and if the input threshold percentage is reached, a trading signal is issued. If it is bullish, go long when today's rise relative to yesterday exceeds the threshold; if it is bearish, go short when today's fall relative to yesterday exceeds the threshold.
After going long or short, this day and the next 4 days will be marked with different colors on the drawing. The position will be automatically closed after 4 days.
## Strategic Advantages
- Using moving averages to determine market trends is a mature and reliable method.
- The strategy logic is simple and clear, easy to understand and implement
- You can control the frequency of the strategy by adjusting parameters
- Automatic stop loss mechanism can effectively control risks
## Strategy Risk
- Moving averages are lagging and may miss the point of rapid price changes.
- Stock prices may fluctuate significantly in the short term, resulting in unnecessary cross signals
- Improper setting of ParameterSet parameters will also affect the effect of the strategy
- Unable to effectively respond to the impact of emergencies
Risk control measures:
1. Optimize moving average parameters and appropriately extend the period to help filter noise
2. Increase the threshold percentage of stock price change and reduce unnecessary transactions
3. Test different holding days and control single loss
4. Combine with other indicators to further confirm trend signals
## Strategy optimization direction
- You can consider changing the moving average to an exponential moving average such as EMA, DMA, etc. to make it more sensitive to price changes.
- Add a stop loss mechanism, such as stopping loss immediately when the moving average is exceeded
- Add other technical indicators for combination, such as MACD, KDJ, etc., to improve the strategy winning rate
- You can try machine learning methods to automatically optimize parameters
- Optimize the timing of entry and exit, such as breakout entrada, etc.
## Summarize
The moving average crossover strategy is a very simple and practical quantitative trading strategy. It makes profits by judging the relationship between short-term and long-term trends and using the trend of stock prices. This strategy is easy to implement and has clear logic. It is the basis of many quantitative trading strategies. Through parameter adjustment and optimization, better strategy effects can be obtained. But we also need to pay attention to controlling risks and preventing misinterpretation of its ideas and blind use.
||


## Overview

The moving average crossover strategy is a very common quantitative trading strategy. It uses the golden cross and death cross of moving averages to determine trends and profit. When the short-term moving average crosses above the long-term moving average, it signals an uptrend, and a long position can be taken. When the short-term moving average crosses below the long-term moving average, it signals a downtrend, and a short position can be taken.

## Strategy Logic

This strategy is based on the golden cross and death cross of moving averages to determine entry and exit points. The code uses two boolean input parameters `upOrDown` and `longOrShort` to determine long or short; `percentInput` to set the threshold percentage of price change; `closePositionDays` to set the number of days to hold the position. 

The core logic is: calculate the increase/decrease of today relative to yesterday. If it reaches the input threshold percentage, a trading signal is triggered. If it's a long signal, when today's price increases more than threshold relative to yesterday, go long. If it's a short signal, when today's price decreases more than threshold relative to yesterday, go short.

After going long/short, the entry day and next 4 days will be marked with colors on the chart. The position will be closed automatically after 4 days.

## Advantages

- Using moving average crossovers to determine trend is a mature and reliable method
- Simple and clear strategy logic, easy to understand and implement
- The frequency can be controlled by adjusting parameters
- The automatic stop loss mechanism effectively controls risks

## Risks

- Moving averages have lagging effects, may miss best timing of rapid price changes
- Significant price swings may happen in short term, generating unnecessary signals
- Inappropriate parameter settings may affect strategy performance 
- Unable to respond effectively to impacts of unexpected events

Risk management:

1. Optimize moving average parameters, longer periods help filter noise
2. Increase threshold percentage to reduce unnecessary trades
3. Test different holding periods to control single loss
4. Combine with other indicators to further confirm signals

## Optimization Directions

- Consider using EMA, DMA instead of SMA to make it more sensitive 
- Add stop loss mechanisms, e.g. stop loss when breaking the average
- Add other technical indicators like MACD, KDJ for combination, improving win rate
- Try machine learning methods to auto optimize parameters
- Optimize entry and exit timing, such as breakout, etc.

## Summary

The moving average crossover strategy is a very simple and practical quantitative trading strategy. By judging the relationship between short-term and long-term trends, it profits from the trending nature of asset prices. This strategy is easy to implement with clear logic, and forms the foundation of many quantitative trading strategies. We can obtain better performance through parameter tuning and optimizations. But we also need to manage risks and avoid misuse.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long=Checked Short=Unchecked|
|v_input_2|true|Direction of Today vs. Previous day: Up=Checked Down=Unchecked|
|v_input_3|4.5|Percent|
|v_input_4|4|How Many Days to Close Position|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-10-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//  Created by Leon Ross

strategy(title = "DaysAfterCertainPercentChangev1", shorttitle = "DACPCv1", overlay = true, 
  pyramiding = 0, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, 
  calc_on_every_tick=true, initial_capital=100000)
  
//Inputs
longOrShort = input(title="Long=Checked Short=Unchecked", type=bool, defval=true) //long=true, down=false
upOrDown = input(title="Direction of Today vs. Previous day: Up=Checked Down=Unchecked", type=bool, defval=true) //up=true, down=false: this is the direction of days vs previous day
percentInput = input(title="Percent", type=float, defval=4.5)
closePositionDays = input(title="How Many Days to Close Position", defval=4)

//Conditions
//percentUpValue = (close / close[1]) - 1
//percentUp = percentUpValue >= (percentInput/100.0)
//upConditions = percentUp
//percentDownValue = 1- (close / close[1])
//percentDown = percentDownValue >= (percentInput/100.0)
//downConditions = percentDown
upValue = (close / close[1]) - 1
downValue = 1 - (close / close[1])
allConditions = if(upOrDown)
    upValue >= (percentInput/100.0)
else
    downValue >= (percentInput/100.0)
    
//Plots
bgcolor(allConditions ? (upOrDown ? green : red) : na, transp=70)
bgcolor(allConditions ? silver : na, transp=70, offset=1)
bgcolor(allConditions ? silver : na, transp=70, offset=2)
bgcolor(allConditions ? silver : na, transp=70, offset=3)
bgcolor(allConditions ? silver : na, transp=70, offset=4)
//bgcolor(downConditions == 1 ? red : na, transp=70)
//bgcolor(downConditions == 1 ? silver : na, transp=70, offset=1)
//bgcolor(downConditions == 1 ? silver : na, transp=70, offset=2)
//bgcolor(downConditions == 1 ? silver : na, transp=70, offset=3)
//bgcolor(downConditions == 1 ? silver : na, transp=70, offset=4)

//Entires
if(longOrShort)
    strategy.entry(id = "Long", long = true, when = allConditions) 
else
    strategy.entry(id = "Short", long = false, when = allConditions)

//Exits
if (barssince(allConditions) == closePositionDays)
    if(longOrShort)
        strategy.close("Long")
    else
        strategy.close("Short")



```

> Detail

https://www.fmz.com/strategy/429081

> Last Modified

2023-10-12 16:47:55
