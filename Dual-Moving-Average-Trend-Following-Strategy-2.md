
> Name

Dual-Moving-Average-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The double moving average tracking strategy is a tracking strategy that uses double moving averages to determine price trends. This strategy uses the moving averages of two different periods to determine the trend direction and send out long and short signals. When the short-period and long-period moving averages move in the same direction, it means the trend is confirmed and you can choose to enter the market.
## Principle
This strategy uses two moving averages to determine price trends. The specific principles are as follows:
1. Calculate the midlines mid and mid_2 of the short period p1 and the long period p2.
2. Determine whether the price is above or below the midline, and get the rising and falling bool values.
3. Determine the trend direction trend and trend_2 of the short-term p1 and long-term p2 cycles through the bool values ​​of SMA smooth rising and falling.
4. When trend and trend_2 are in the same direction, a long or short signal is issued.
5. Fill the bar with different colors to indicate the trend direction.
6. The time to enter is when the short-term and long-term trends are in the same direction.
The above constitutes the core logic of the dual moving average tracking strategy. By judging by double moving averages, some false breakthroughs can be effectively filtered out. When the short-term and long-term trends are in the same direction, it means that the price trend is very clear, and the risk of entry trading is small.
## Advantage Analysis
The main advantages of the dual moving average tracking strategy are:
1. Using double moving average judgment can filter out false breakthroughs and make the entry timing more reliable.
2. Using moving averages of different periods can realize trend judgment in multiple time frames and make trading signals more accurate.
3. Combining short-period and long-period moving averages, you can grasp the general trend and capture some short-term callback opportunities.
4. The strategy logic is simple and clear, easy to understand and implement, and is suitable for traders of different levels.
5. The moving average cycle can be customized, and parameters can be adjusted according to the market to adapt to different varieties and market types.
6. Use histograms to visually display the trend direction to form more intuitive trading tips.
## Risk Analysis
There are also some risks that need to be noted in the dual moving average tracking strategy:
1. When the moving average cycle is improperly set, positions may be adjusted multiple times, increasing transaction frequency and slippage costs. You can adjust the cycle parameters appropriately or add filtering conditions for opening a position.
2. When the market is in a turbulent period and the moving average crosses, an error signal will appear. You can filter through the andere indicator, or add position management rules.
3. Breakout short-term callbacks may be missed. You can shorten the moving average period appropriately, or use other strategies to capture short-term opportunities.
4. When the general trend changes suddenly, improper stop loss setting may lead to large losses. The stop loss position should be adjusted in a timely manner to ensure that there is support below the stop loss point.
5. The strategy does not consider fundamental factors and only judges trends technically. Users need to use this strategy based on their own research and judgment.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add other indicator filters, such as trading volume, momentum indicators, etc., to avoid invalid transactions during shock periods.
2. Use adaptive moving average cycles to automatically adjust parameters according to market changes instead of static cycles.
3. Add a position management module to guide the specific increase in position through rules such as trend strength.
4. Add stop loss module, trailing stop or time stop loss to control single loss.
5. Consider combining machine learning and other technologies to determine the trend accuracy through training and dynamically adjust the entry and exit logic.
6. Consider adding fundamental factors, such as financial announcements, important events, etc., to avoid deviating from the larger-level situation.
## Summarize
To sum up, the double moving average tracking strategy is a simple and practical trend judgment strategy. It combines both short-term and long-term time dimensions to identify trends. The judgment of entry timing is very reliable and suitable for most traders who follow trend trading. Of course, there are also some risks that need to be paid attention to in this strategy. Users can make improvements from aspects such as parameter optimization and risk control to make the strategy more suitable for actual situations. Generally speaking, the double moving average strategy is a very classic and practical trend trading strategy.
||


## Overview

The Dual Moving Average Trend Following strategy is a trend following strategy that uses two moving averages to determine the price trend. It generates long and short signals when the short and long period moving averages align in the same direction. Entering when the short and long term trends agree provides increased confidence.

## Principle 

The strategy uses two moving averages to determine the trend direction. The logic is as follows:

1. Calculate the midline for short period p1 and long period p2. 

2. Determine if the price is above or below the midlines, generating up and down bool values.

3. Use SMA to smooth the up and down values, determining the trend direction trend and trend_2.

4. When trend and trend_2 agree, generate long or short signals.

5. Color-filled bars visually indicate the trend.

6. Enter trades when short and long term trends agree.

The dual moving average comparison creates the core logic. Trading with trend agreement on two timeframes reduces false breakouts. Agreeing trends indicate a high conviction move, lowering risk on entries.

## Advantages

The main advantages of this strategy are:

1. Dual moving average reduces false breakouts and provides reliable entry signals.

2. Using two timeframes provides better accuracy in trend determination. 

3. Captures longer trends while taking advantage of short-term pullbacks.

4. Simple and easy to understand logic suitable for all traders. 

5. Customizable moving average periods allows optimization for any market.

6. Visual bar coloring provides intuitive trend direction.

## Risks

Some risks to consider:

1. Incorrect period settings may cause excessive position changes increasing costs. Optimize parameters or add filters.

2. Whipsaws occur when markets oscillate across moving averages. Add filters or position sizing rules.

3. Short pullbacks can be missed. Consider shorter periods or additional strategies.

4. Incorrect stop loss placement can lead to large losses when trends suddenly reverse. Actively manage stops.

5. No fundamental analysis is considered. Use discretion when applying signals.

## Enhancements

Some ways to improve the strategy:

1. Add additional filters like volume or momentum to avoid whipsaws.

2. Employ adaptive periods that adjust based on market conditions.

3. Add position sizing rules based on trend strength for guidance. 

4. Implement stop loss modules like trailing stops or time exits to limit losses.

5. Consider machine learning to score trend accuracy and improve entry/exit logic.

6. Incorporate fundamental factors like earnings, events to avoid trading against larger trends.

## Conclusion

In summary, the Dual Moving Average Trend Following strategy provides a simple and practical approach to trend identification. By combining short and long-term perspectives, it generates high-confidence entry signals suitable for most trend traders. Risks exist and can be mitigated through optimization, risk management and discretion. Overall, the dual moving average strategy remains a robust, classic trend following approach.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|p1|
|v_input_2|21|p2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-01 00:00:00
end: 2023-10-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
// My Tradingview Scripts : https://bit.ly/2HKtr7k 
strategy("UniDir Strategy", overlay=true, initial_capital=50000, default_qty_value=50000, default_qty_type=strategy.cash, slippage=3, commission_type=strategy.commission.percent, commission_value=0.075, pyramiding=0)

p1=input(14)
p2=input(21)


Price = close
mid = (highest(high, p1)+lowest(low, p1)) / 2
mid_2 = (highest(high, p2)+lowest(low, p2)) / 2

//Trend
up = Price > mid ? 1 : 0
up_2 = Price > mid_2 ? 1 : 0
down = Price < mid ? 1 : 0
down_2 = Price < mid_2 ? 1 : 0
trend = sma(up, 2) == 1 ? 1 : sma(down, 2) == 1 ? -1 : nz(trend[1])
trend_2 = sma(up_2, 2) == 1 ? 1 : sma(down_2, 2) == 1 ? -1 : nz(trend_2[1])

dir1=trend==1 ? lime : red
dir2=trend_2==1 ? lime : red
dir_all=trend==1 and trend_2==1 ? lime : red

top_p=plot(1)
hi_p=plot(0.4)
mid_p=plot(0.2)
lo_p=plot(0)

fill(hi_p,mid_p,color=dir1,transp=80)
fill(lo_p,mid_p,color=dir2,transp=80)
fill(top_p,hi_p,color=dir_all,transp=0)

// Entry
long_cond = trend==1 and trend_2==1
short_cond = trend==-1 and trend_2==-1

if long_cond
    strategy.entry("Long",strategy.long)
if short_cond
    strategy.entry("Short",strategy.short)
```

> Detail

https://www.fmz.com/strategy/428700

> Last Modified

2023-10-08 14:25:40
