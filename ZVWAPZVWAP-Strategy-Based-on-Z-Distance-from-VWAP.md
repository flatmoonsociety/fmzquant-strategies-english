
> Name

ZVWAP-Strategy-Based-on-Z-Distance-from-VWAP
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14fb2a3f84dccd3bb75.png)
[trans]


## Overview
This strategy is based on LazyBear's Z distance VWAP indicator. It calculates the Z distance between the price and VWAP to determine whether it is overbought or oversold, and to make entries and exits. The strategy adds the EMA moving average and the judgment of Z distance returning to the 0 axis, which can filter out some noise signals.
## Strategy Principle
1. Calculate the value of VWAP
2. Calculate the Z distance between price and VWAP
3. Set the overbought line (2.5) and oversold line (-0.5)
4. When the fast line is greater than the slow line, the Z distance is lower than the oversold line, and the Z distance crosses the 0 axis, go long
5. Close the position when the Z distance exceeds the overbought line
6. Add stop loss logic
Key functions:
- calc_zvwap: Calculate the Z distance between price and VWAP
- VWAP value: vwap(hlc3)
- Fast line: ema(close,fastEma)
- Slow line: ema(close,slowEma)
## Advantage Analysis
1. Use Z distance to more intuitively determine overbought and oversold
2. Combine with EMA to filter out false breakthroughs to avoid being trapped
3. Adding positions is allowed and you can make profits by taking advantage of the trend
4. There is stop loss logic to control risks
## Risk Analysis
1. It is necessary to ensure that the parameter settings are reasonable, such as overbought and oversold line positions, EMA period, etc.
2. The Z distance indicator lags behind and may miss key buying and selling points.
3. Allowing additional positions will increase the risk of loss
4. The stop loss position needs to be set appropriately
Solution:
1. Optimize parameter settings through backtesting
2. Filter signals by combining additional indicators
3. Set up reasonable conditions for adding positions
4. Dynamically adjust stop loss position
## Optimization direction
1. Optimize EMA cycle parameters
2. Test different overbought and oversold judgment criteria
3. Add other indicators to filter signal noise
4. Test different stop loss methods
5. Optimize entry, position addition and stop loss logic
## Summarize
This strategy uses Z distance to determine the relationship between price and VWAP, and combines it with EMA to filter noise signals to capture trend opportunities. The strategy allows you to add positions to track the trend, while setting stop losses to control risk. The stability of the strategy can be improved by optimizing parameters and adding other indicators. However, the Z distance index has a lag problem, which needs to be considered during optimization. Generally speaking, this strategy captures trends with simple and clear logic, and can become an efficient trend following strategy after being fully optimized.
||


## Overview

This strategy is based on the Z-distance from VWAP indicator by LazyBear. It uses the Z-distance between price and VWAP to determine overbought and oversold conditions, as well as entries and exits. The strategy incorporates EMA lines and Z-distance crossing 0 level to filter out some noise.

## Strategy Logic

1. Calculate VWAP value
2. Calculate Z-distance between price and VWAP  
3. Set overbought line (2.5) and oversold line (-0.5)
4. Go long when fast EMA > slow EMA, Z-distance < oversold line and Z-distance crosses above 0
5. Close position when Z-distance > overbought line
6. Incorporate stop loss logic

Key Functions:

- calc_zvwap: Calculate Z-distance between price and VWAP
- VWAP value: vwap(hlc3)  
- Fast EMA: ema(close,fastEma)
- Slow EMA: ema(close,slowEma)

## Advantage Analysis  

1. Z-distance intuitively shows overbought/oversold levels
2. EMA filters out false breakouts 
3. Allows pyramiding to capitalize on trends
4. Has stop loss logic to control risk

## Risk Analysis

1. Need to ensure parameters like lines, EMA periods are set properly
2. Z-distance indicator lags, may miss key turning points
3. Pyramiding can increase loss if trend reverses
4. Stop loss needs to be set reasonably

Solutions:
1. Optimize parameters via backtesting
2. Add other indicators to filter signals
3. Set proper conditions for pyramiding
4. Use dynamic stop loss 

## Optimization Directions

1. Optimize EMA periods
2. Test different overbought/oversold criteria 
3. Add other indicators to filter noise
4. Test different stop loss techniques
5. Optimize entry, pyramiding and stop loss logic

## Summary

The strategy uses Z-distance to determine price-VWAP relationship and adds EMA to filter signals, aiming to capture trend opportunities. It allows pyramiding to follow trends and has a stop loss to control risk. Optimization and adding other indicators can improve robustness. However, lagging issue of Z-distance should be considered during optimization. Overall, this is a trend-following strategy with simple, clear logic. When fully optimized, it can be an efficient tool to trade trends.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|13|length|
|v_input_2|-0.5|OverSold Line|
|v_input_3|2|OverBought Line|
|v_input_4|13|Fast EMA|
|v_input_5|55|Slow EMA|
|v_input_6|5|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-03 00:00:00
end: 2023-11-09 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mohanee

//@version=4
//This is based on Z distance from VWAP by Lazybear
strategy(title="ZVWAP[LB] strategy", overlay=false,pyramiding=2, default_qty_type=strategy.fixed, default_qty_value=3,    initial_capital=10000, currency=currency.USD)
length=input(13,"length")

calc_zvwap(pds, source1) =>
	mean = sum(volume*source1,pds)/sum(volume,pds)
	vwapsd = sqrt(sma(pow(source1-mean, 2), pds) )
	(close-mean)/vwapsd


upperTop=2.5  //input(2.5)
upperBottom=2.0  //input(2.0)
lowerTop=-0.5  //input(-0.5)
lowerBottom=-2.0 //input(-2.0)

buyLine=input(-0.5, title="OverSold Line",minval=-2, maxval=3)
sellLine=input(2.0, title="OverBought Line",minval=-2, maxval=3)

fastEma=input(13, title="Fast EMA",minval=1, maxval=50)
slowEma=input(55, title="Slow EMA",minval=10, maxval=200)

stopLoss =input(5, title="Stop Loss",minval=1) 

hline(0, title="Middle Line", linestyle=hline.style_dotted, color=color.green)

ul1=plot(upperTop, "OB High")
ul2=plot(upperBottom, "OB Low")
fill(ul1,ul2, color=color.red)
ll1=plot(lowerTop, "OS High")
ll2=plot(lowerBottom, "OS Low")
fill(ll1,ll2, color=color.green)
zvwapVal=calc_zvwap(length,close)
plot(zvwapVal,title="ZVWAP",color=color.purple, linewidth=2)


longEmaVal=ema(close,slowEma)
shortEmaVal=ema(close,fastEma)  

vwapVal=vwap(hlc3)


zvwapDipped=false

for i = 1 to 10
    zvwapDipped := zvwapDipped or zvwapVal[i]<=buyLine

longCondition=  shortEmaVal > longEmaVal  and zvwapDipped and  crossover(zvwapVal,0)

barcolor(longCondition ? color.yellow: na)

strategy.entry(id="ZVWAPLE", long=true,  when= longCondition  and strategy.position_size<1) 


//Add
strategy.entry(id="ZVWAPLE", comment="Add", long=true,  when= strategy.position_size>1 and close<strategy.position_avg_price and crossover(zvwapVal,0)) 


//calculate stop Loss
stopLossVal =  strategy.position_avg_price -  (strategy.position_avg_price*stopLoss*0.01)

strategy.close(id="ZVWAPLE",comment="SL Exit",    when=close<stopLossVal)   //close all on stop loss

strategy.close(id="ZVWAPLE",comment="TPExitAll",    qty=strategy.position_size ,   when= crossunder(zvwapVal,sellLine))   //close all      zvwapVal>sellLine
```

> Detail

https://www.fmz.com/strategy/431669

> Last Modified

2023-11-10 12:02:19
