
> Name

Triple-Moving-Average-Crossover-System Triple-Moving-Average-Crossover-System
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The triple moving average crossover system is a classic trend-following stock trading strategy. It utilizes the crossover of three moving averages of different time lengths as buy and sell signals. A buy signal is generated when the short-term moving average crosses the medium-term moving average and the medium-term moving average crosses the long-term moving average; a sell signal is generated when the short-term moving average crosses below the medium-term moving average and the medium-term moving average crosses below the long-term moving average.
## Strategy Principle
This strategy is based on three moving averages: long-term moving average ma1, medium-term moving average ma2 and short-term moving average ma3. First calculate these three lines:
```pine
length1 = input(18,'长线') 
length2 = input(9,'中线')
length3 = input(4,'短线')

ma1 := sma(close,length1) 
ma2 := sma(close,length2)
ma3 := sma(close,length3)
```

Among them, length1, length2 and length3 respectively define the time length of the three moving averages. The sma function calculates the simple moving average of the close price over the corresponding length.
Then use the intersection of the three moving averages to determine when to buy and sell:
```pine
if ma2 > ma1 and ma3 > ma3[1] 
    strategy.entry("Long", strategy.long)

if ma2 < ma1 and ma3 < ma3[1]
    strategy.entry("Short", strategy.short) 
```

When the mid-term line ma2 crosses the long-term line ma1, and the short-term line ma3 crosses the ma3 of the previous period, a long signal is issued. When the mid-term line ma2 crosses the long-term line ma1, and the short-term line ma3 falls below the ma3 of the previous period, a short signal is issued.
## Strategic Advantages
- Using three moving averages, you can more clearly judge changes in trends.
- The combination of long and short lines can filter out some short-term market noise and lock in the longer-term trend.
- The rules are simple and easy to operate.
- The parameters of the three moving averages can be adjusted to adapt to different market environments.
## Strategy Risk
- Buying and selling points are confirmed afterwards, and losses cannot be completely avoided.
- When the stock price fluctuates near the moving average, multiple false signals will appear.
- If the long-term line is too long, the turning point of the trend will be missed. If the short-term line is too short, frequent trading will occur due to noise.
- Doesn't handle sideways markets well.
These risks can be reduced by appropriately optimizing parameters and combining other indicators as filter conditions.
## Strategy optimization direction
- You can test combinations of different length parameters to find the best parameters.
- Stop loss can be added to control losses.
- You can add other indicators to judge the strength and deviation to avoid misjudgment. For example, MACD, KD, etc.
- You can choose an appropriate take-profit strategy based on the actual situation.
## Summarize
The triple moving average crossover strategy is a simple and practical trend following strategy. It determines changes in market trends based on the intersection of three moving averages to generate trading signals. The advantage of this strategy is that it has simple rules, can effectively track trends, and is suitable for medium and long-term operations. But there is also a certain risk of false signals and retracement risks. It can be improved through parameter optimization, adding auxiliary indicators and other methods to adapt to different market environments. Generally speaking, the triple moving average crossover strategy is a basic introductory strategy for quantitative trading and a good start for learning algorithmic trading.

||


## Overview

The Triple Moving Average Crossover System is a typical trend-following stock trading strategy. It uses the crossover of three moving averages of different time lengths as buy and sell signals. When the short period moving average crosses above the medium period moving average, and the medium period moving average crosses above the long period moving average, a buy signal is generated. When the short period moving average crosses below the medium period moving average, and the medium period moving average crosses below the long period moving average, a sell signal is generated.

## Strategy Logic

The strategy is based on three moving averages: the long period moving average ma1, the medium period moving average ma2 and the short period moving average ma3. First it calculates these three lines:

```pine
length1 = input(18,'长线')  
length2 = input(9,'中线')
length3 = input(4,'短线')

ma1 := sma(close,length1)
ma2 := sma(close,length2) 
ma3 := sma(close,length3)
```

Where length1, length2 and length3 define the time lengths of the three moving averages. The sma function calculates the simple moving average of the close price over the corresponding length.

It then uses the crossover of the three moving averages to determine entries and exits:

```pine 
if ma2 > ma1 and ma3 > ma3[1]
    strategy.entry("Long", strategy.long)

if ma2 < ma1 and ma3 < ma3[1] 
    strategy.entry("Short", strategy.short)
```

When the medium term ma2 crosses above the long term ma1, and the short term ma3 crosses above the previous period's ma3, a long signal is triggered. When the medium term ma2 crosses below the long term ma1, and the short term ma3 crosses below the previous period's ma3, a short signal is triggered.

## Advantages of the Strategy

- Using three moving averages can clearly identify trend changes.
- The combination of long and short periods filters out some short term market noise and locks in longer term trends. 
- Simple rules make it easy to implement.
- Parameters can be adjusted to adapt to different market environments.

## Risks of the Strategy

- Entries and exits are identified in hindsight and cannot completely avoid losses.
- Whipsaws occur when the price oscillates around moving averages.
- Long period line that is too long may miss trend turning points. Short period line that is too short may trigger frequent trades due to noise.
- Does not handle ranging markets very well.

These risks can be reduced through appropriate parameter optimization, adding filters with other indicators etc.

## Improvement Directions

- Backtest different parameter combinations to find optimal values.
- Add stop loss to control losses.
- Add other indicators to judge momentum and divergence to avoid false signals. E.g. MACD, KD etc.
- Choose suitable profit taking strategy according to actual situation.

## Summary 

The Triple Moving Average Crossover strategy is a simple and practical trend following strategy. It identifies changes in trend direction based on the crossover of three moving averages to generate trading signals. The advantages of this strategy are its simple rules and effective tracking of trends, making it suitable for medium to long term trading. However, there are also risks of false signals and drawdowns. The strategy can be improved by optimizing parameters, adding supporting indicators etc. to adapt to different market environments. Overall, the Triple Moving Average Crossover is a foundational algorithmic trading strategy that provides a good starting point for learning quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|18|Long line|
|v_input_2|9|center line|
|v_input_3|4|Short line|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-28 00:00:00
end: 2023-09-27 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © dongyun

//@version=4
strategy("三重交叉修正模式系统", overlay=true)
//strategy.risk.allow_entry_in(strategy.direction.long)
length1 = input(18,'长线')
length2 = input(9,'中线')
length3 = input(4,'短线')

ma1 =0.0
ma2 = 0.0
ma3 = 0.0

ma1 := sma(close,length1)
ma2 := sma(close,length2)
ma3 := sma(close,length3)

plot(ma1)
plot(ma2)
plot(ma3)

if ma2 > ma1 and ma3 > ma3[1]
	strategy.entry("Long", strategy.long, when=strategy.position_size <= 0)

if ma2 < ma1 and ma3 < ma3[1]
	strategy.entry("Short", strategy.short, when=strategy.position_size > 0)
```

> Detail

https://www.fmz.com/strategy/428089

> Last Modified

2023-09-28 15:33:14
