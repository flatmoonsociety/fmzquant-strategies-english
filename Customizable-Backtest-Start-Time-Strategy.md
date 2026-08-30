
> Name

Customizable-Backtest-Start-Time-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
The purpose of this strategy is to allow users to customize the start time of backtesting, thereby achieving more flexible and customized backtesting.
## Strategy Principle
This strategy implements customized backtest startup time by using the time and timestamp functions of the pine script.
First, it lets users enter a custom backtest launch year, month, day, hour, and minute in the settings. It then uses these inputs to generate a timestamp and stores it in the startTime variable.
In the conditional judgment of the policy, it adds a startTime condition. The policy will only start when the current time is greater than or equal to startTime.
For example:
```pine
longCondition = crossover(sma(close, 14), sma(close, 28)) 

if (longCondition and startTime) 

  strategy.entry("My Long Entry Id", strategy.long)
```

This allows for customized backtest start times. Users can flexibly configure the start time of backtesting according to their needs, not just the hard-coded time.
## Advantage Analysis
This strategy of customized backtest start time has the following advantages:
1. More flexible: Users can completely customize the start time of backtesting, and it is no longer limited to a fixed time point.
2. More realistic: The start time of the backtest can be set to the time when the strategy is actually run, so that the backtest is closer to the real market situation.
3. Convenient event-driven backtesting: The startup time can be set according to the occurrence time of an event to conduct backtesting for specific events.
4. Convenient condition adjustment: The start-up conditions of the backtest can be adjusted very conveniently, so as to conduct targeted backtests at different stages.
5. Repeatable and reliable: Parameterize the start-up time of the backtest, so that it can be run repeatedly to obtain reliable backtest results.
## Risk Analysis
There are also some risks with using customized backtest launch times:
1. The backtest results depend on the startup time: different startup times may cause great differences in the backtest results.
2. The startup time needs to be carefully selected: unreasonable startup time may cause backtest distortion and fail to reflect the real situation.
3. Increased risk of curve fitting: It is easy to fit historical data by adjusting the startup time, thus creating the risk of over-fitting.
4. Reduce the comparability of backtest results: The backtest results of this strategy are not quite comparable to the backtest results of a fixed startup time.
Corresponding solutions:
1. Conduct multiple backtests to evaluate the impact of startup time changes on the results.
2. Select the time of major events as the start time to reduce backtest distortion.
3. Carefully adjust the startup time to avoid overfitting historical data.
4. Save the backtest with a fixed startup time as a baseline to compare with the customized backtest.
## Optimization direction
This customized backtest startup time strategy can also be optimized from the following aspects:
1. Support customization of start and end time, and realize flexible configuration of complete backtest time window.
2. Supports multiple time modes: specific date, relative date, event-driven, etc., making backtest time configuration more intelligent and convenient.
3. Supports graphical configuration interface to make time parameter setting more intuitive.
4. Support different time granularity configuration: year, month, day, hour, minute, second, etc.
5. Record the backtest time configuration to make the backtest results reproducible, traceable and comparable.
6. Add verification for improper time configuration to avoid unreasonable time configuration affecting the quality of backtesting.
7. Provide startup time binding function to synchronize and copy startup time to multiple policies with one click.
## Summarize
This strategy implements customized and flexible backtest startup time configuration, which can reduce the limitations of backtesting and make it closer to the actual situation. However, it is also necessary to be wary of the dependence of backtest results on startup time, and take measures such as multiple backtests and event driving to reduce backtest distortion. There are many optimization directions for this strategy, and it is expected to achieve more intelligent and convenient backtest time configuration in the future.
||

## Overview

The purpose of this strategy is to allow users to customize the start time of backtesting for more flexible and customizable backtesting.

## Strategy Logic

This strategy uses Pine Script's time and timestamp functions to implement a customizable backtest start time. 

It first allows users to input a customized backtest start year, month, date, hour, and minute in the settings. It then uses these inputs to generate a timestamp and stores it in the startTime variable.

In the strategy's condition check, it adds a new startTime condition. The strategy will only start when the current time is greater than or equal to startTime.

For example:

```pine
longCondition = crossover(sma(close, 14), sma(close, 28))

if (longCondition and startTime)

  strategy.entry("My Long Entry Id", strategy.long) 
```

This allows implementing a customizable backtest start time. Users can flexibly configure the start time of backtesting instead of being limited to hardcoded times.

## Advantage Analysis

This customizable backtest start time strategy has the following advantages:

1. More Flexible: Users can fully customize the backtest start time instead of being limited to a fixed point in time.

2. More Realistic: The start time can be set to the actual runtime of the strategy, making the backtest more realistic.

3. Convenient for Event-driven Backtesting: The start time can be set based on the occurrence time of an event for backtesting specific events.

4. Easy Condition Adjustment: The backtest start conditions can be easily adjusted for targeted backtesting of different stages.

5. Repeatable and Reliable: Parameterizing the backtest start time allows repeatable and reliable backtest results.

## Risk Analysis

Using a customizable backtest start time also has some risks:

1. Results Depend on Start Time: Different start times may lead to very different backtest results.

2. Start Time Needs Careful Selection: Unreasonable start times may cause distortion in backtest results.

3. Increased Curve Fitting Risk: Easily overfit by adjusting the start time to historical data.

4. Reduced Comparability: The results of this strategy are less comparable to fixed start time backtests.

Solutions:

1. Backtest multiple times to evaluate the impact of start time changes on results.

2. Choose significant event times as start times to minimize distortion.

3. Carefully adjust start times to avoid overfitting historical data.

4. Keep fixed start time backtests as benchmark for comparison with customized backtests.

## Optimization Directions

This customizable backtest start time strategy can also be improved in the following aspects:

1. Support customization of both start and end times for full flexible configuration of the backtest time window.

2. Support multiple time modes: specific dates, relative dates, event-driven, etc. for smarter and more convenient time configuration.

3. Support graphical configuration interface for more intuitive time parameter setting. 

4. Support configuration of different time granularities: year, month, day, hour, minute, second, etc.

5. Record backtest time configuration for reproducible, traceable, and comparable results.

6. Add validation of improper time configurations to avoid low-quality backtests due to unreasonable time settings.

7. Provide start time binding to easily synchronize start times across multiple strategies.

## Summary

This strategy enables customizable and flexible configuration of backtest start times to reduce limitations and make backtests more realistic. But the dependency of results on start times needs to be watched out for using multiple backtests, event-driven models, etc. to reduce distortion. This strategy also has many directions for improvement to achieve smarter and more convenient backtest time configuration in the future.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2018|Start Year|
|v_input_2|true|Start Month|
|v_input_3|true|Start Day|
|v_input_4|false|Start Hour|
|v_input_5|false|Start Minute|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-19 00:00:00
end: 2023-09-25 00:00:00
period: 2d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("C320up Strategy Tester Start Time", overlay = true)
// Copy and paste below into your strategy
// Strategy Tester Start Time
xYear = input(2018, title = "Start Year")
xMonth = input(01, title = "Start Month", minval = 01, maxval = 12)
xDay = input(01, title = "Start Day", minval = 01, maxval = 31)
xHour = input(00, title = "Start Hour", minval = 00, maxval = 23)
xMinute = input(00, title = "Start Minute", minval = 00, maxval = 59)
startTime = time >= timestamp(xYear, xMonth, xDay, xHour, xMinute)
// End copy and paste
// Add (and startTime) at the end of your condition/s to activate

// The strategy below is just an example
longCondition = crossover(sma(close, 14), sma(close, 28))
if (longCondition and startTime)
    strategy.entry("My Long Entry Id", strategy.long)
shortCondition = crossunder(sma(close, 14), sma(close, 28))
if (shortCondition and startTime)
    strategy.entry("My Short Entry Id", strategy.short)
// Happy trading!

```

> Detail

https://www.fmz.com/strategy/427932

> Last Modified

2023-09-26 20:53:15
