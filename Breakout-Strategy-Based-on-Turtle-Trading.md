
> Name

Breakout-Strategy-Based-on-Turtle-Trading
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d619974a7a857d1495.png)

[trans]


## Overview
This strategy is based on the famous turtle trading method, uses the Donchian channel indicator to determine price breakthroughs, and combines the ATR indicator to set stop loss levels to achieve trend tracking. The advantage of the strategy is strong retracement control ability, which can effectively control single stop loss and reduce the probability of continuous losses. However, this strategy has weak adaptability to trading varieties and needs to optimize channel parameters. Generally speaking, as an introductory version of the turtle trading method, this strategy can be used to verify the effectiveness of the turtle trading method, and can also be used as one of the basic strategies for quantitative trading.
## Principle
This strategy is mainly based on two indicators: Donchian Channel and ATR.
The Donchian channel is calculated from the highest price and the lowest price. By default, the strategy sets the channel length to 20 days, and draws the channel based on the highest and lowest prices within 20 days. When the price breaks through the upper edge of the channel, a buy signal is generated; when the price breaks through the lower edge of the channel, a sell signal is generated.
The ATR indicator is used to measure market volatility and set stop losses. The default ATR period is set to 20 days. The strategy uses twice the ATR as the stop loss level.
The specific transaction logic is:
1. When the price breaks through the upper edge of the channel, enter the market long.
2. The stop loss point is the low point at the time of entry minus twice the ATR.
3. When the price breaks through the lower edge of the channel, close the long position.
4. When the price breaks through the lower edge of the channel, enter the market short.
5. The stop loss point is the high point of entry plus twice the ATR.
6. When the price breaks through the upper edge of the channel, close the short position.
In summary, this strategy relies on the Donchian channel to determine the trend direction and entry timing, and uses ATR to set stop losses to control risks and track the trend.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Strong retracement control ability. Using the ATR indicator to set stop loss can effectively control single losses.
2. Realized trend tracking. The Donchian channel can effectively determine price breakthroughs and indicate trend transitions.
3. Suitable for high volatility varieties. The ATR indicator takes into account market volatility, and setting stop loss is more in line with the characteristics of different varieties.
4. The strategic ideas are simple and clear, easy to understand and implement.
5. Python language can be used to flexibly write and optimize strategies.
## Risk Analysis
This strategy also has some risks that need attention:
1. Channel parameters need to be optimized. Under different varieties and time periods, channel parameters need to be adjusted to adapt to market characteristics.
2. Continuous stop loss risk. Under abnormal market conditions, multiple stop losses may be triggered in the short term, resulting in larger losses.
3. ATR parameters need to be tested. The ATR parameter directly affects the stop loss effect and needs to be adjusted under different varieties and volatile environments.
4. Transaction frequency may be too high. In a volatile market where the trend is not obvious, too many cross signals may be generated.
5. Profits may be limited. The strategy is mainly based on stop loss and cannot effectively capture the entire increase of the trend market.
6. Stop loss may be insufficient under exaggerated market conditions. Under some abnormal market conditions, price gaps may directly trigger stop losses.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize channel parameters and test the adaptability of different parameters to different varieties.
2. Add filtering conditions to avoid generating too many signals in volatile market conditions. Consider breakout amplitude or volume filters.
3. Optimize the ATR cycle parameters and test the impact of different parameters on the stop loss effect.
4. Add the pyramid entry strategy, add positions in the trending market, and expand profit margins.
5. Combine with other indicators to improve filtering effect. For example, indicators such as MACD and KD can determine the trend and avoid reverse trading.
6. Optimize stop loss points based on transaction costs such as slippage and handling fees. Prevent your stop loss from being too close.
7. Test the adaptability of different varieties and adjust parameters to target specific varieties.
## Summarize
This strategy is an introductory version of the turtle trading method. Generally speaking, the strategy idea is simple and clear, and the retracement control ability is strong. It can effectively verify the principle of the turtle trading method. However, the adaptability of this strategy to trading varieties is weak, and parameters need to be optimized according to different varieties in order to achieve the strategy effect. With improvements such as parameter optimization and filtering conditions, this strategy can become one of the basic trend tracking strategies for quantitative trading.
|| 

## Overview

This strategy is based on the famous Turtle Trading system, using Donchian Channel to identify breakouts and ATR to set stop loss for trend following. The advantage is strong drawdown control ability by effectively limiting single trade loss. However, adaptiveness across different trading instruments is weak and needs parameter tuning. Overall, as an introductory version of Turtle Trading system, this strategy can be used to validate the effectiveness of Turtle Trading rules and also serve as a basic quantitative trading strategy.

## Principles 

The strategy is mainly based on two indicators: Donchian Channel and ATR.

Donchian Channel is constructed by highest high and lowest low. The default channel length is 20 days, plotted with 20-day highest high and lowest low. Buy signal is generated when price breaks out above the upper band, and sell signal when price breaks below the lower band.

ATR measures volatility of the market and is used for stop loss setting. The default ATR period is 20 days. The strategy uses 2N ATR as the stop loss level.

The specific trading logic is:

1. Go long when price breaks out above the upper band. 

2. Set stop loss at the low price at entry minus 2N ATR.

3. Close long position when price breaks below the lower band.

4. Go short when price breaks out below the lower band.

5. Set stop loss at the high price at entry plus 2N ATR. 

6. Close short position when price breaks above the upper band.

In summary, the strategy identifies trend direction and entry signals with Donchian Channel, and controls risk with ATR based stop loss, to follow trends.

## Advantage Analysis

The main advantages of this strategy are:

1. Strong drawdown control ability. ATR stop loss can effectively limit single trade loss.

2. Ability to follow trends. Donchian Channel can effectively identify breakouts and trend changes.

3. Applicable for high volatility instruments. ATR considers market volatility in stop loss setting.

4. Simple and clear logic, easy to understand and implement. 

5. Flexibility to optimize with Python language.

## Risk Analysis

Some risks of this strategy to note:

1. Channel parameters need optimization for different instruments and timeframes.

2. Consecutive stop loss risk. Multiple stop loss triggers may occur under volatile market conditions.

3. ATR parameter needs backtesting. ATR directly affects stop loss and should be adjusted based on volatility.

4. Potentially too high trading frequency. Too many whipsaw signals may occur under range-bound market.

5. Limited profit potential. The strategy focuses on stop loss and cannot fully capture trend gains. 

6. Insufficient stop loss during volatile moves. Price gaps may directly trigger stop loss.

## Optimization Directions

The strategy can be improved in the following aspects:

1. Optimize channel parameters for different instruments.

2. Add filters to avoid too many signals under range-bound market. Consider breakout magnitude or volume filters.

3. Optimize ATR period parameter and test impact on stop loss.

4. Add pyramid entry to increase position size to maximize trend gains.

5. Incorporate other indicators such as MACD, KD to avoid false signals.

6. Adjust stop loss based on slippage and commission costs.

7. Test adaptiveness across different instruments and optimize parameters.

## Summary

As an introductory version of Turtle Trading system, this strategy has simple and clear logic, strong drawdown control ability, and can effectively validate the principles of Turtle Trading. But adaptiveness across instruments is weak and parameters need to be tuned based on specific instruments. With optimizations like parameter tuning, adding filters, this can serve as a basic trend following strategy for quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Enter Channel|
|v_input_2|10|Exit Channel|
|v_input_3|false|Offset Bars|
|v_input_4|0|Direction: Long|Short|
|v_input_5|2|ATR multiplier (Stop Loss)|
|v_input_6|20|ATR Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-10 00:00:00
end: 2023-10-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Based on Turtle traders strategy: buy/sell on Donchian breakouts and stop loss on ATR 2x
// initial version considerations :
//// 1. Does not consider filter for avoiding new entries after winning trades (filtering rule from Turtle Strategy on 20 day breakout strategy) 
//// 2. Does not consider pyramiding (aditional entries after 1N price movements)

strategy("Turtle trading strategy (Donchian/ATR)", overlay=true)

enter_period = input(20, minval=1, title="Enter Channel")
exit_period = input(10, minval=1, title="Exit Channel")
offset_bar = input(0,minval=0, title ="Offset Bars")
direction = input("Long",options=["Long","Short"],title="Direction")
max_length = max(enter_period,exit_period)
atrmult = input(2,title="ATR multiplier (Stop Loss)")
atrperiod = input(20,title="ATR Period")

closed_pos = false
dir_long = direction == "Long"? true : false
atr = atr(atrperiod)
upper = dir_long ? highest(enter_period): highest(exit_period)
lower = dir_long ? lowest(exit_period): lowest(enter_period)
atrupper = close + atr
atrlower = close - atr
plotted_atr = dir_long ? atrlower : atrupper

//basis = avg(upper, lower)

l = plot(lower, style=line, linewidth=3, color=lime, offset=1)
u = plot(upper, style=line, linewidth=3, color=lime, offset=1)
a = plot(plotted_atr, style=line,linewidth=2,color=red,offset=1)
//plot(basis, color=yellow, style=line, linewidth=1, title="Mid-Line Average")
//break upper Donchian (with 1 candle offset) (buy signal)
break_up = (close >= upper[1])
//break lower Donchian (with 1 candle offset) (sell signal)
break_down = (close <= lower[1])
stop_loss = dir_long ? (close<=plotted_atr[1]) : (close>=plotted_atr[1])

if break_up and dir_long
    strategy.entry("buy", strategy.long, 1)
    closed_pos :=false
if (break_down or stop_loss) and dir_long
    strategy.close("buy")
    
if break_down and not dir_long
    strategy.entry("sell", strategy.short, 1)
    closed_pos :=false
if (break_up or stop_loss) and not dir_long
    strategy.close("sell")
    closed_pos :=true
    
losing_trade = strategy.equity[0]<strategy.equity[1]
//plotshape(losing_trade,text="Losing!")    
plotshape(stop_loss,style=dir_long?shape.labeldown:shape.labelup,text="Stop!")
//plot(strategy.equity)


    


```

> Detail

https://www.fmz.com/strategy/429512

> Last Modified

2023-10-17 17:22:34
