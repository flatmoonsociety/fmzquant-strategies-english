
> Name

Day-of-the-Week-Custom-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Summary
This is a custom long-short trading strategy for Bitcoin. It allows you to backtest long or short positions based on different trading days of the week. Price may tend to move in one direction or the other on different trading days each week, and this strategy allows you to take advantage of this by testing different trading days over a range of days.
Please make sure you take the daily chart when viewing performance and trading history to ensure the script is working as expected and you are getting as much historical data as possible from Trading View.
## Strategy Principle
The core logic of this strategy is to allow the user to choose between long trades, short trades, or no trades each day of the week.
First, it allows users to set the date range for backtesting, including the starting month, date, and year and the ending month, date, and year.
It then uses an array of timeframes to store the numeric representation of each day of the week, from 0 for Sunday to 6 for Saturday.
Another array, timeframes_options, is used to store the choice of long, short, or no trading for each day. This is set via an input option.
In the for loop, the strategy checks whether the current trading day matches a day in the timeframes array. If there is a match, and the options are different from the previous day, all open positions are closed first.
If the option is not "None", a position in the corresponding direction is opened based on the selected long or short position.
This way, the strategy can trade long and short based on settings for each day of the week within a set date range.
## Advantage Analysis
The main advantage of this strategy is that it provides highly customizable long and short trades. Users are free to choose which trading direction to pursue each day of the week.
Unlike a fixed weekly trading strategy, this strategy can be flexibly adjusted. If the results are not satisfactory on certain days, you can easily modify it to only trade other days.
Backtesting date ranges are also very flexible, allowing you to test any user-specified time period to see which date combinations perform best.
The transaction logic is very clear and simple, easy to understand and modify. Users can adjust parameters without programming.
The strategy also automatically closes open positions every day when direction changes, avoiding unnecessary risk.
## Risk Analysis
The main risk with this strategy is that the daily trading selections set by the user may not necessarily be suitable for all date ranges.
For example, going long on weekdays and short on weekends may prove effective during certain periods of time, but may fail during other periods of time.
Therefore, you must be careful to test different date ranges and not rely on the results of a single backtest. Parameter adjustments must be based on specific market conditions.
Another risk is the inability to stop losses and close positions in time when the daily direction changes. This could lead to wider losses. But this strategy attempts to mitigate this problem by automatically closing positions.
Generally speaking, this strategy relies more on parameter optimization and requires sufficient testing to find parameter combinations suitable for different market conditions.
## Optimization direction
This strategy can be optimized through the following aspects:
1. When the daily direction changes, add stop loss logic, set a trailing stop loss when the position is profitable, and reduce the retracement.
2. Add a filter to only send a signal when the price breaks through the high or low of a certain day to avoid repeated trading when there is no trend.
3. Reduce the position size during periods of high volatility and increase the position during periods of low volatility to keep risks under control.
4. Choose to add machine learning to the trading day, judge the daily trading probability based on historical data, and generate dynamic daily directions.
5. Add processing logic for emergencies, such as suspending transactions when major financial events occur to avoid being trapped.
## Summarize
This strategy provides highly flexible long and short trading capabilities through daily direction selection. Users can freely combine tests to find the best parameters. However, this strategy has high optimization requirements and requires a lot of testing to find settings suitable for different markets. Adding stop losses, filters, dynamic adjustments and other optimization methods can reduce risks and improve stability. With careful parameter optimization, this strategy can become an efficient daily directional trading tool.
||


## Overview

This is a custom long/short trading strategy for bitcoin that allows backtesting longing or shorting on different days of the week. The price may tend to move in one direction or another on each weekday, and this strategy allows testing across a range of dates to capitalize on this.

Make sure you are on the daily timeframe when viewing performance and trade history to ensure the script works as intended and you have maximum historical data from TradingView.

## Strategy Logic  

The core logic of the strategy is to allow the user to choose long, short or no trading for each day of the week.

First, it allows the user to set the date range for backtesting, including start month, day, year and end month, day, year.

Then, it uses an array timeframes to store the numeric representation of each day of the week, from Sunday 0 to Saturday 6. 

Another array timeframes_options is used to store the choice of long, short or no trading for each day. This is set via an input option.

In a for loop, the strategy checks if the current trading day matches a day in the timeframes array. If so, and the option differs from the previous day, it first closes all open positions.

If the option is not "None", it opens a position in the appropriate direction based on the chosen long or short.

Thus, the strategy can trade long/short over the set date range based on the settings for each day of the week.

## Advantage Analysis

The main advantage of this strategy is providing highly customizable long/short trading. The user has complete freedom in choosing trading direction for each day of the week.

Unlike fixed weekly trading strategies, this one can be flexibly adjusted. Poor performing days can be easily modified to only trade other days. 

The backtest date range is also highly flexible, allowing testing of any user specified period to see which date combinations perform best.

The trading logic is very clear and simple, easy to understand and modify. Users can adjust parameters without coding.

The strategy also auto closes positions on direction change each day, avoiding unnecessary risk.

## Risk Analysis

The main risk is that the user's chosen daily trading selections may not fit every date range. 

For example, long on weekdays and short weekends may prove effective for some periods but fail in others.

So date ranges must be carefully tested, and not rely on one backtest outcome. Parameter tweaking needs to consider market conditions.

Another risk is inability to cut losses in time when direction changes daily. But the strategy attempts to mitigate this by auto closing.

Overall, the strategy is heavily optimization reliant, and requires sufficient testing to find parameter sets fitting different market conditions.

## Optimization Directions

The strategy can be improved in several aspects:

1. Add stop loss logic on daily direction change, setting trailing stops when positions are profitable to limit drawdowns.

2. Add a filter, only taking signals on breaking certain day high/low, avoiding trading without trend. 

3. Reduce position sizing in high volatility periods, and increase when volatility is low to control risk.

4. Add machine learning to trading day selections, judging probability of each day based on historical data, generating dynamic daily directions.

5. Add logic to handle sudden events like major news by pausing trading to avoid being caught offsides.

## Conclusion

This strategy provides highly flexible long/short trading ability through daily direction selections. Users can freely combine test for optimum parameters. But it has high optimization requirements, needing extensive testing to find settings fitting different markets. Adding enhancements like stops, filters, dynamic adjustments can reduce risk and improve robustness. With prudent parameter optimization, the strategy can become an effective daily directional trading tool.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|6|From Month|
|v_input_2|14|From day|
|v_input_3|2021|From Year|
|v_input_4|12|To Month|
|v_input_5|31|To day|
|v_input_6|2100|To Year|
|v_input_7|0|sunday: None|Short|Long|
|v_input_8|0|monday: Long|Short|None|
|v_input_9|0|tuesday: Long|Short|None|
|v_input_10|0|wednesday: Long|Short|None|
|v_input_11|0|thursday: None|Short|Long|
|v_input_12|0|friday: None|Short|Long|
|v_input_13|0|saturday: None|Short|Long|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-19 00:00:00
end: 2023-09-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/

//@version=4
// strategy("Day of Week Custom Buy/Sell Strategy", overlay=true, currency=currency.USD, default_qty_value=1.0,initial_capital=30000.00,default_qty_type=strategy.percent_of_equity)

frommonth = input(defval = 6, minval = 01, maxval = 12, title = "From Month")
fromday = input(defval = 14, minval = 01, maxval = 31, title = "From day")
fromyear = input(defval = 2021, minval = 1900, maxval = 2100, title = "From Year")

tomonth = input(defval = 12, minval = 01, maxval = 12, title = "To Month")
today = input(defval = 31, minval = 01, maxval = 31, title = "To day")
toyear = input(defval = 2100, minval = 1900, maxval = 2100, title = "To Year")

timeframes = array.new_int(7, 1)
timeframes_options = array.new_string(7, 'None')

array.set(timeframes,0,7)
array.set(timeframes_options,0, input(defval='None', options=['Long','Short','None'], title='sunday'))
array.set(timeframes,1,1)
array.set(timeframes_options,1, input(defval='Long', options=['Long','Short','None'], title='monday'))
array.set(timeframes,2,2)
array.set(timeframes_options,2, input(defval='Long', options=['Long','Short','None'], title='tuesday'))
array.set(timeframes,3,3)
array.set(timeframes_options,3, input(defval='Long', options=['Long','Short','None'], title='wednesday'))
array.set(timeframes,4,4)
array.set(timeframes_options,4, input(defval='None', options=['Long','Short','None'], title='thursday'))
array.set(timeframes,5,5)
array.set(timeframes_options,5, input(defval='None', options=['Long','Short','None'], title='friday'))
array.set(timeframes,6,6)
array.set(timeframes_options,6, input(defval='None', options=['Long','Short','None'], title='saturday'))



for i = 0 to array.size(timeframes) - 1
    
    if dayofweek == array.get(timeframes, i) and array.get(timeframes_options, i) != array.get(timeframes_options, i==0?6:i-1)
        strategy.close_all()

    if dayofweek == array.get(timeframes, i) and array.get(timeframes_options, i)!='None' and array.get(timeframes_options, i) != array.get(timeframes_options, i==0?6:i-1)
        if array.get(timeframes_options, i) == 'Long'
            strategy.entry("Long", strategy.long, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 00, 00)))
        else if array.get(timeframes_options, i) == 'Short'
            strategy.entry("Short", strategy.short, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 00, 00)))

```

> Detail

https://www.fmz.com/strategy/427930

> Last Modified

2023-09-26 20:49:44
