
> Name

Super Trend Strategy SuperTrend
> Author

inventor quantification
> Strategy Description

[trans]

At the request of our platform users, FMZ is compatible with the Pine language function library of TradingView now, and has entered a stable version.

* the grammer is fully compatible with v5 version
* all indicators of ta library are fully implemented
* full implementation of math library
* full implementation of string library
* full implementation of array library
* input parameters are recognized in the interface automatically
* request.security support for heikinashi
* strategy library implementation (full support for stop loss/profit target/trailing stop/conditional orders, etc.)
* compatible with plot/plotchar/plotshape/plotcandle/alert/alertcondition etc.

It is a continuous process that provide full support for language functions, and this public version is made available in advance for user testing.

Later, FMZ will continue to increase and improve the function library support for Pine language of TradingView, if necessary, please leave a comment on this strategy.

Remark: If you encounter undefined variables, it is proved that this attribute is not supported. You can delete the relevant call, or send a work order to contact the technician to solve the problem.
||
At the request of platform users, FMZ is compatible with TradingView’s Pine language function library, which has now entered a stable version.
* The syntax is fully compatible with version v5
* All indicators of ta library are fully implemented
* math library fully implemented
* The string library is fully implemented
* The array library is fully implemented
*Input parameters are automatically recognized to the interface
* request.security support for heikinashi
* Strategy library implementation (supports complete support for stop loss/take profit/tracking take profit/conditional orders, etc.)
* compatible with plot/plotchar/plotshape/plotcandle/alert/alertcondition etc.
Full support for language functions is a continuous effort. This public version is released in advance to facilitate user testing.
In the future, FMZ will continue to add and improve the function library support for TradingView’s Pine language. If you have any needs, you can leave a message on this policy.
Note: If you encounter an undefined variable, it proves that this attribute is not supported yet. You can delete the relevant call, or send a work order to contact technical personnel to solve the problem.
[/trans]
 ![IMG](https://www.fmz.com/upload/asset/114b4feedd1ae4f8550.png)



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-08-17 08:00:00
end: 2024-08-29 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

strategy("supertrend", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 50)

[supertrend, direction] = ta.supertrend(input(5, "factor"), input.int(10, "atrPeriod"))

plot(direction < 0 ? supertrend : na, "Up direction", color = color.green, style=plot.style_linebr)
plot(direction > 0 ? supertrend : na, "Down direction", color = color.red, style=plot.style_linebr)

if direction < 0
    if supertrend > supertrend[2]
        strategy.entry("entry long", strategy.long)
    else if strategy.position_size < 0
        strategy.close_all()
else if direction > 0
    if supertrend < supertrend[3]
        strategy.entry("entry short", strategy.short)
    else if strategy.position_size > 0
        strategy.close_all()

```

> Detail

https://www.fmz.com/strategy/359806

> Last Modified

2024-08-30 18:24:36
