
> Name

Dual-EMA-Golden-Cross-Profit-Taking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/7318f9bbbffe47a533.png)
[trans]

## Overview
This strategy achieves an efficient short-term trading strategy by calculating two sets of EMA indicators with different parameters, setting the buy signal when the two sets of EMA indicators occur a golden cross, and setting the sell signal when the other two sets of EMA indicators occur a death cross.
## Strategy Principle
This strategy uses 4 EMA indicators, namely 9-period EMA1, 26-period EMA2, 100-period EMA3 and 55-period EMA4. When the buy signal is set to EMA1 crossing above EMA2, it means that the short-term EMA crosses above the long-term EMA, which is a typical golden cross signal. When the sell signal is set to EMA3 and crosses EMA4, it is a death cross signal. In this way, you can quickly enter the market when the short-term EMA indicator reaches a golden cross, and quickly stop loss and profit when the long-term EMA indicator reaches a death cross, achieving efficient short-term trading.
## Strategic Advantages
1. Use double EMA crossover to achieve fast in and fast out, which can quickly lock in short-term profits.
2. The trading signals are simple, clear and easy to implement.
3. The parameters are adjustable and can be adjusted according to different markets.
4. Large profit potential, suitable for short-term scalping transactions
## Risk Analysis
1. Double EMA crossover may cause false signals, and it needs to be filtered in combination with other indicators.
2. Improper setting of EMA parameters may lead to over sensitivity or slowness
3. You need to pay close attention to large-level rotations and stop profits in a timely manner
## Optimization direction
1. You can add other indicators such as MACD and KDJ to filter signals to improve signal accuracy.
2. You can test more combinations and find the optimal EMA parameters
3. You can set a trailing stop to lock in profits
## Summarize
Overall, this strategy is a very typical and effective short-term trading strategy. The advantage is that it is fast in and out, suitable for scalping, and has a large profit potential. At the same time, there are also some risks that need to be taken care of. If the parameters are adjusted properly and other indicators are assisted in signal filtering, it can become a very practical short-term trading strategy.
||

## Overview

This strategy calculates two groups of EMA indicators with different parameters and sets the buy signal when the two groups of EMA indicators have a golden cross and the sell signal when another two groups of EMA indicators have a death cross, so as to achieve an efficient short-term trading strategy.

## Strategy Principle  

The strategy uses 4 EMA indicators, EMA1 with a period of 9, EMA2 with a period of 26, EMA3 with a period of 100, and EMA4 with a period of 55. The buy signal is set when EMA1 crosses over EMA2, indicating that the short-term EMA crosses over the long-term EMA, which is a typical golden cross signal. The sell signal is set when EMA3 crosses below EMA4, which is a death cross signal. This allows fast entry when the short-term EMA indicator has a golden cross and fast stop loss when the long-term EMA indicator has a death cross to achieve efficient short-term trading.

## Advantage Analysis

1. Use dual EMA cross for fast entry and exit to quickly lock short-term profits 
2. Clear and simple trading signals, easy to implement
3. Adjustable parameters to suit different markets
4. Large profit range, suitable for short-term scalping trading

## Risk Analysis  

1. Dual EMA cross may have false signals, needs to be filtered with other indicators
2. Improper EMA parameter settings may cause too sensitive or dull
3. Need to closely monitor larger cycles for timely profit-taking

## Optimization Direction

1. Can add MACD, KDJ and other indicators for signal filtering to improve signal accuracy
2. Can test more combinations to find the optimal EMA parameters  
3. Can set moving stop loss to lock in profits

## Summary

Overall, this is a very typical and effective short-term trading strategy. The advantages are fast entry and exit, suitable for scalping and large profit range. There are also some risks that need attention and prevention. With proper parameter adjustment and assistance of other indicators for signal filtering, it can become a very practical short-term trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|EMA_L|
|v_input_int_2|26|EMA_L2|
|v_input_int_3|100|EMA_S|
|v_input_int_4|55|EMA_S2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-05 00:00:00
end: 2024-01-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © YukalMoon

//@version=5
strategy(title="EMA SCALPEUR", overlay=true, initial_capital = 1000)


//// input controls

EMA_L = input.int (title = "EMA_L", defval = 9, minval = 1, maxval = 100, step =1)
EMA_L2 = input.int (title = "EMA_L2", defval = 26, minval = 1, maxval = 100, step =1)
EMA_S = input.int (title = "EMA_S", defval = 100, minval = 1, maxval = 100, step =1)
EMA_S2 = input.int (title = "EMA_S2", defval = 55, minval = 1, maxval = 100, step =1)


/// mise en place de ema

shortest = ta.ema(close, 9)
short = ta.ema(close, 26)
longer = ta.ema(close, 100)
longest = ta.ema(close, 55)

plot(shortest, color = color.red)
plot(short, color = color.orange)
plot(longer, color = color.aqua)
plot(longest, color = color.yellow)

plot(close)

//// trading indicators

EMA1 = ta.ema (close,EMA_L)
EMA2 = ta.ema (close,EMA_L2)
EMA3 = ta.ema (close, EMA_S)
EMA4 = ta.ema (close, EMA_S2)


buy = ta.crossover(EMA1, EMA2)
//sell = ta.crossunder(EMA1, EMA2)

buyexit = ta.crossunder(EMA3, EMA4)
//sellexit = ta.crossover(EMA3, EMA4)

/////strategy

strategy.entry ("long", strategy.long, when = buy, comment = "EXIT-LONG")
//strategy.entry ("short", strategy.short, when = sell, comment = "ENTER-SHORT")


///// market exit

strategy.close ("long", when = buyexit, comment = "ENTER-LONG")
//strategy.close ("short",  when = sellexit, comment = "EXIT-SHORT")

```

> Detail

https://www.fmz.com/strategy/438484

> Last Modified

2024-01-12 14:02:22
