
> Name

Multi-time moving average trading strategyFour-Exponential-Moving-Averages-and-Volume-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy combines a variety of EMA moving averages with different parameter settings and EOM energy indicators to realize trend judgment in multiple time periods and build a trading strategy that can jointly judge long-term and short-term. This strategy aims to use the multi-time period resonance of different period moving averages to explore longer-lasting trends.
## Strategy Principle
This strategy uses 4 sets of parameter EMA moving averages with different periods, namely 13-period, 21-period, 50-period and 180-period EMA. These four sets of EMA moving averages construct multiple time dimensions and are used to determine price trends and explore longer-term trend patterns.
The strategy uses the EOM Energy indicator to confirm trends. The EOM indicator combines trading volume and price fluctuations, and can effectively determine the strength of buying and selling. The strategy determines that when EOM is greater than 0, it is a long market, and when EOM is less than 0, it is a short market.
The strategy sets two options. Option 1 is to go long when the short-term EMA stands above the long-term EMA, and to close the position when the short-term EMA stands below the long-term EMA. Option 2 is to go long when the short-term EMA crosses above the mid-term EMA, and close the position when the short-term EMA crosses below the mid-term EMA. Two options can more comprehensively determine the confirmation of the trend.
## Strategic Advantages
- Use multi-time period EMA to determine trends and discover longer-term trend patterns
- The EOM volume energy indicator can effectively judge the trading strength and avoid being misled by temporary corrections.
- Two optional entry methods can confirm the trend more comprehensively
- Adopt layered hand-changing stop loss to reduce single loss
## Strategy Risk
- EMA moving average has hysteresis and may miss a quick reversal
- Energy indicators may give false signals
-Multiple condition judgments cause unclear entry
- Layered stop loss may be too mechanical
## Optimization direction
- You can test more combinations of parameter EMA periods to find optimal parameters
- You can add other indicators for entry confirmation, such as MACD, etc.
-Trailing stop loss can be used to track trend runs
- The proportion of positioning positions can be adjusted according to market conditions
## Summarize
This strategy integrates multi-time period EMA judgment and volume indicator filtering to achieve trend tracking and noise removal. There is still a lot of room for optimization, and the stability of the strategy can be further improved by testing different parameter combinations and adding more indicators. At the same time, the use of dynamic stop loss and position management can also greatly optimize strategy performance.
|| 

## Overview

This strategy combines multiple EMAs with different parameter settings and the EOM volume indicator to determine trends across multiple timeframes and build a trading strategy with both long-term and short-term judgments. It aims to leverage the multi-timeframe resonance of different period moving averages to uncover longer-lasting trend patterns.

## Strategy Logic

The strategy uses 4 groups of EMAs with different period parameters - 13, 21, 50 and 180. These 4 EMAs establish multiple time dimensions to determine price trends and uncover longer-term trend patterns.

The strategy uses the EOM volume indicator to confirm trends. The EOM combines trading volume and price volatility range to effectively gauge buying and selling pressure. The strategy determines long conditions when EOM is above 0 and short conditions when EOM is below 0.

The strategy has two options. Option 1 goes long when shorter EMA crosses above longer EMA and closes long when shorter EMA crosses below longer EMA. Option 2 goes long when shorter EMA crosses above intermediate EMA and closes long when shorter EMA crosses below intermediate EMA. The two options allow more comprehensive trend confirmation.

## Advantages

- Using multi-timeframe EMAs to determine trends can uncover longer-term trend patterns
- EOM volume indicator effectively gauges buying/selling pressure, avoiding false signals from temporary pullbacks  
- Two optional entry methods enable more comprehensive trend confirmation
- Scaling out with layered exits reduces single exit exposure

## Risks

- EMAs have lag and may miss fast reversals
- Volume indicators can give false signals 
- Multiple condition criteria creates unclear entry
- Layered exits may be too mechanistic 

## Enhancement Opportunities

- Test more EMA period combinations to find optimal parameters
- Add other indicators like MACD for entry confirmation
- Adopt dynamic trailing stop loss to follow trends
- Adjust position sizing based on market conditions

## Summary

This strategy integrates multi-timeframe EMA trend determination and volume indicator filtering to achieve trend following and noise removal. There is still large room for optimization by testing different parameter combinations and adding more indicators to further improve robustness. Meanwhile, dynamic stop loss and position sizing can also significantly optimize performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|13|ema1l|
|v_input_2|21|ema2l|
|v_input_3|50|ema3l|
|v_input_4|180|ema4l|
|v_input_5|14|length|
|v_input_6|10000|Divisor|
|v_input_7|true|option1|
|v_input_8|false|option2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-02 00:00:00
end: 2023-10-08 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SoftKill21

//@version=4
strategy("4x ema + volume", overlay=true,initial_capital = 1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent , commission_value=0.1 )

//ema x 4
ema1l=input(13)
ema2l=input(21)
ema3l=input(50)
ema4l=input(180)

ema1=ema(close,ema1l)
ema2=ema(close,ema2l)
ema3=ema(close,ema3l)
ema4=ema(close,ema4l)

long1 = close > ema1 and ema1 > ema2 and ema2> ema3 and ema3 > ema4
long2 = crossover(ema1,ema2) and crossover(ema1,ema3)

short1 = close < ema1 and ema1 < ema2 and ema2< ema3 and ema3 < ema4
short2= crossunder(ema1,ema2) and crossunder(ema1,ema3)


//eom
length = input(14, minval=1)
div = input(10000, title="Divisor", minval=1)
eom = sma(div * change(hl2) * (high - low) / volume, length)


option1=input(true)
option2=input(false)

if(option1)
    strategy.entry("long",1,when=long1 and eom>0)
    strategy.close("long",when=short1 and eom<0)
 
if(option2)
    strategy.entry("long",1,when=long2 and eom>0)
    strategy.close("long",when=short2 and eom<0)   
```

> Detail

https://www.fmz.com/strategy/428787

> Last Modified

2023-10-09 15:05:47
