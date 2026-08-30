
> Name

High-Low-Breakout-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description



[trans]
The name of this strategy is "High Low Low Breakout Trend Following Strategy". This strategy determines the direction of the trend by identifying new highs and lows when prices make new highs and lows, and trend following when prices break out of the latest highs or lows.
The specific transaction logic is as follows:
1. Calculate the highest price and lowest price within a certain period (for example, 22 days).
2. When the price breaks through the highest price of the last day, a buy signal is generated, indicating the formation of an upward trend.
3. When the price falls below the lowest price of the last day, a sell signal is generated, indicating the formation of a downward trend.
4. In order to filter out false signals, the trend direction needs to be verified. For example, if the price reaches a new high but the indicators deviate, buying is not considered.
5. Only follow a breakout of the latest high/low if the indicator is in line with the price trend.
The advantage of this strategy is to capture the opportunity when the price breaks through a key point, which is often accompanied by the start or acceleration of a trend. However, it is necessary to prevent too many invalid signals from being generated during the shock and consolidation.
Overall, focusing on breakouts of key price areas is a basic trend following approach. However, traders also need to use other indicators for confirmation and adjust parameters according to the actual situation to maximize the effectiveness of the strategy.


||



This strategy is named “High-Low Breakout Trend Following Strategy”. It identifies new price highs and lows to determine trend direction, and trades breakouts of latest high/low points to follow trends.

The specific logic is:

1. Calculate the highest high and lowest low over a certain period (e.g. 22 days). 

2. When price breaks above the latest 1-day high, a buy signal is generated, flagging an uptrend.

3. When price breaks below the latest 1-day low, a sell signal is generated, flagging a downtrend. 

4. Trend direction is checked to filter false signals. For example, new high price with bearish divergence is ignored for buying.

5. Only when indicators align with price trend will trades be taken on breakouts of the latest high/low points.

The advantage is capturing pivotal breakout timing, which often accompanies trend start or acceleration. But over-trading in ranging markets should be prevented.

In summary, watching key price area breakouts is essential in trend following. But confirmation with other indicators and parameter tuning based on actual conditions are needed to maximize the strategy’s utility.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_hlc3|0|price: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_2|22|LookBack|
|v_input_3|14|length|
|v_input_4|2|length2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-13 00:00:00
end: 2023-09-12 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=1
strategy(title="HIGHER HIGH LOWER LOW STRATEGY", shorttitle="HH LL STRATEGY", overlay=true, calc_on_order_fills=true, initial_capital=100000, default_qty_type=strategy.percent_of_equity, currency="USD", default_qty_value=100)

////


//Higher High or Lower Low Entry Inputs
price = input(hlc3)
LookBack = input(22)
Highest = highest(LookBack)
Lowest = lowest(LookBack)

long = price > Highest[1] 
short = price < Lowest[1]




//Divergence Check Inputs
length = input(14)
High_Guard = highest(length)
Low_Guard = lowest(length)

length2 = input(2)

long1 = long == 1 and Highest[1] > High_Guard[length2]
short1 = short == 1 and Lowest[1] < Low_Guard[length2]


plot(long and long[1], color=green, style=line)
plot(short and short[1], color=red, style=line)

strategy.entry("Long", strategy.long, when=long1)
strategy.entry("Short", strategy.short, when=short1)

```

> Detail

https://www.fmz.com/strategy/426597

> Last Modified

2023-09-13 15:50:50
