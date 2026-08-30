
> Name

Bollinger-Bands-Reversal-Oscillation-Trend-Strategy Bollinger-Bands-Reversal-Oscillation-Trend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11fded547fd60513c19.png)
[trans]

## Overview
This is a reversal-type shock trend strategy based on the Bollinger Bands channel. It uses the upper and lower Bollinger Bands channels as trend judgment and looks for reversal opportunities to enter when the price is close to the channel boundary.
## Strategy Principle
This strategy uses the Bollinger Bands indicator as the main technical indicator. The Bollinger Bands consist of the n-day moving average and its upper and lower fluctuation ranges. The upper Bollinger Bands = n-day moving average + m×n-day standard deviation, and the lower Bollinger Bands = n-day moving average – m×n-day standard deviation. where n and m are parameters.
When the price is close to the upper track, it means that it is currently in an upward trend, but it may peak and reverse; when the price is close to the lower track, it means that it is currently in a downward trend, but it may bottom out and reverse. At this time, if it effectively breaks through the upper and lower Bollinger Bands, it may begin to reverse.
The specific trading rules of this strategy are as follows:
1. When the closing price is greater than the upper Bollinger Band, enter the market as a long position; when the closing price is less than the lower track of the Bollinger Band, enter the market as a short position.
2. Take profit and stop loss with n-day moving average as signal. When the closing price of the long order falls below the n-day moving average, stop profit exiting; when the closing price of the short order breaks the n-day moving average, stop loss exiting.
3. Use a fixed transaction volume and a fixed value for each transaction.
4. Use the fixed ratio fund management method to set a fixed profit and loss ratio and order adjustment range. When a fixed rate of profit is achieved, the position is increased by a fixed range, and when a loss is achieved, the position is reduced.
## Advantage Analysis
This strategy has the following advantages:
1. Use the Bollinger Bands channel to determine the trend direction, adopt a counter-trend trading strategy, enter the market at a time when the price may reverse, avoid most shocks, and increase the winning rate.
2. The moving average is more reliable as a stop-profit and stop-loss signal and can lock in most profits.
3. The fixed trading volume strategy is simple and easy to implement and does not require complex calculations.
4. The fixed ratio fund management strategy can expand profits while controlling risks through position adjustment.
## Risk Analysis
This strategy also has certain risks:
1. There is a probability that Bollinger Bands judgment will generate wrong signals, and you may lose money by placing orders in the opposite direction during the trend.
2. The hysteresis of the moving average may lead to insufficient take-profit.
3. Fixed trading volume cannot adjust positions according to market conditions, and there is a problem of too large or too small positions.
4. The fixed ratio fund management method will expand the position to a large extent, which may lead to expanded losses.
Countermeasures: Optimize Bollinger Band parameters to improve signal accuracy; combine other indicators to determine trends; appropriately reduce the size of fixed positions; reduce the position adjustment range of fixed ratio fund management.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the parameters of Bollinger Bands, such as adjusting the n value and m value, to improve the accuracy of Bollinger Band channel judgment.
2. Add other indicator judgments, such as MACD, KD, etc., to avoid Bollinger Bands false signals.
3. Adjust fixed trading volume to dynamic trading volume and flexibly adjust positions according to market conditions.
4. Reduce the position adjustment range of the fixed ratio capital management method and optimize the capital curve.
5. Add stop loss strategies, such as trailing stop loss, range breakout stop loss, etc., to further control risks.
6. Carry out parameter optimization, automatically optimize parameter combinations, and find the best parameters to optimize the strategy.
## Summarize
This strategy as a whole is a more typical Bollinger Bands reversal strategy. It uses Bollinger Bands to determine trend reversal points, sets stop-profit and stop-loss settings in conjunction with moving averages, and uses fixed trading volume and fixed-ratio fund management to control risks. Compared with the traditional Bollinger Bands strategy, this strategy, as a reversal strategy, can theoretically avoid some shocks and increase the probability of profit. However, due to inherent flaws in indicators such as Bollinger Bands and moving averages, further optimization is still needed in actual application in order to parameterize the strategy and reduce trading risks.
|| 


## Overview

This is a reversal oscillation trend strategy based on Bollinger Bands channel. It uses Bollinger Bands upper and lower channel to determine trend, and looks for reversal opportunities when price approaches channel boundaries.

## Strategy Logic

The strategy uses Bollinger Bands as the main technical indicator. Bollinger Bands consist of n-period moving average and upper/lower bands deviation. Upper band = n-period MA + m * n-period standard deviation, Lower band = n-period MA - m * n-period standard deviation. n and m are parameters.

When price approaches upper band, it indicates an uptrend but may reverse at peak. When price approaches lower band, it indicates a downtrend but may reverse at bottom. Effective breakout of Bollinger Bands may signal potential reversal.

The specific trading rules are:

1. Go long when close > upper band, go short when close < lower band. 

2. Use n-period moving average as profit taking and stop loss signal. Close long when close breaks below MA, close short when close breaks above MA.

3. Use fixed quantity for each trade.

4. Use fixed fractional position sizing. Increase position size by fixed amount when meet fixed profit ratio, decrease size when loss.

## Advantage Analysis 

The advantages of this strategy:

1. Using Bollinger Bands channel to determine trend direction and trade reversals, avoids most whipsaws and improves win rate.

2. Moving average is a reliable profit taking/stop loss signal, locks in most profits.

3. Fixed quantity is simple and easy to implement, no complex calculation needed.

4. Fixed fractional position sizing expands profits while controls risk by position adjustment.

## Risk Analysis

The risks of this strategy:

1. Bollinger Bands may generate incorrect signals, causing losses trading against trend.

2. Lagging of moving average may lead to insufficient profit taking. 

3. Fixed quantity cannot adapt to market conditions, risks of over/under position sizing.

4. Aggressive position sizing adjustment in fixed fractional method may expand losses.

Solutions: Optimize Bollinger Bands parameters to improve signal accuracy. Add other indicators to determine trend. Reduce fixed quantity size. Lower position sizing adjustment ratio in fractional position sizing method.

## Improvement Directions

The strategy can be improved from the following aspects:

1. Optimize Bollinger Bands parameters like n and m to increase accuracy.

2. Add other indicators like MACD, KD to avoid wrong signals.

3. Change fixed quantity to dynamic positioning based on market conditions.

4. Lower position sizing adjustment ratio in fractional position sizing to smooth equity curve.

5. Add stop loss strategies like moving stop loss, breakout stop loss to control risk.

6. Parameter optimization to find optimal parameter combinations.

## Summary

In summary, this is a typical Bollinger Bands reversal strategy. It identifies reversal points by Bollinger Bands, sets profit taking/stop loss by moving average, controls risk by fixed quantity and fractional position sizing. As a reversal strategy, it theoretically avoids some whipsaws and improves profitability compared to traditional Bollinger Bands strategies. However, flaws in Bollinger Bands, moving averages require further optimization and risk management for robust practical application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|(?Technical Parameters)BB Length|
|v_input_float_1|2|Standard Deviation Multipler|
|v_input_int_2|20|SMA Exit Signal Length|
|v_input_int_3|400|(?Money Management)Fixed Ratio Value ($)|
|v_input_int_4|200|Increasing Order Amount ($)|
|v_input_1|timestamp(1 Jan 2020 00:00:00)|(?Backtesting Period)Start Date|
|v_input_2|timestamp(1 July 2024 00:00:00)|End Date|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-30 00:00:00
end: 2023-10-30 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © gsanson66


//This strategy uses the well-known Bollinger Bands Indicator
//@version=5
strategy("BOLLINGER BANDS BACKTESTING", shorttitle="BB BACKTESTING", overlay=true, initial_capital=1000, default_qty_type=strategy.cash, default_qty_value=950, commission_type=strategy.commission.percent, commission_value=0.18)


//----------------------------------------FUNCTIONS---------------------------------------//

//@function Displays text passed to `txt` when called.
debugLabel(txt, color) =>
    label.new(bar_index, high, text = txt, color=color, style = label.style_label_lower_right, textcolor = color.black, size = size.small)

//@function which looks if the close date of the current bar falls inside the date range
inBacktestPeriod(start, end) => (time >= start) and (time <= end)


//---------------------------------------USER INPUTS--------------------------------------//

//Technical parameters
bbLength = input.int(defval=20, minval=1, title="BB Length", group="Technical Parameters")
mult = input.float(defval=2, minval=0.1, title="Standard Deviation Multipler", group="Technical Parameters")
smaLength = input.int(defval=20, minval=1, title="SMA Exit Signal Length", group="Technical Parameters")
//Money Management
fixedRatio = input.int(defval=400, minval=1, title="Fixed Ratio Value ($)", group="Money Management")
increasingOrderAmount = input.int(defval=200, minval=1, title="Increasing Order Amount ($)", group="Money Management")
//Backtesting period
startDate = input(title="Start Date", defval=timestamp("1 Jan 2020 00:00:00"), group="Backtesting Period")
endDate = input(title="End Date", defval=timestamp("1 July 2024 00:00:00"), group="Backtesting Period")


//----------------------------------VARIABLES INITIALISATION-----------------------------//
strategy.initial_capital = 50000
//Exit SMA
smaExit = ta.sma(close, smaLength)
//BB Calculation
basis = ta.sma(close, bbLength)
dev = mult * ta.stdev(close, bbLength)
upperBB = basis + dev
lowerBB = basis - dev
//Money management
equity = strategy.equity - strategy.openprofit
var float capital_ref = strategy.initial_capital
var float cashOrder = strategy.initial_capital * 0.95
//Backtesting period
bool inRange = na


//------------------------------CHECKING SOME CONDITIONS ON EACH SCRIPT EXECUTION-------------------------------//

//Checking if the date belong to the range
inRange := true

//Checking performances of the strategy
if equity > capital_ref + fixedRatio
    spread = (equity - capital_ref)/fixedRatio
    nb_level = int(spread)
    increasingOrder = nb_level * increasingOrderAmount
    cashOrder := cashOrder + increasingOrder
    capital_ref := capital_ref + nb_level*fixedRatio
if equity < capital_ref - fixedRatio
    spread = (capital_ref - equity)/fixedRatio
    nb_level = int(spread)
    decreasingOrder = nb_level * increasingOrderAmount
    cashOrder := cashOrder - decreasingOrder
    capital_ref := capital_ref - nb_level*fixedRatio

//Checking if we close all trades in case where we exit the backtesting period
if strategy.position_size!=0 and not inRange
    strategy.close_all()
    debugLabel("END OF BACKTESTING PERIOD : we close the trade", color=color.rgb(116, 116, 116))


//-----------------------------------EXIT SIGNAL------------------------------//

if strategy.position_size > 0 and close < smaExit
    strategy.close("Long")
if strategy.position_size < 0 and close > smaExit
    strategy.close("Short")


//----------------------------------LONG/SHORT CONDITION---------------------------//

//Long Condition
if close > upperBB and inRange
    qty = cashOrder/close
    strategy.entry("Long", strategy.long, qty)
//Short Condition
if close < lowerBB and inRange
    qty = cashOrder/close
    strategy.entry("Short", strategy.short, qty)


//---------------------------------PLOTTING ELEMENT----------------------------------//

plot(smaExit, color=color.orange)
upperBBPlot = plot(upperBB, color=color.blue)
lowerBBPlot = plot(lowerBB, color=color.blue)
fill(upperBBPlot, lowerBBPlot, title = "Background", color=strategy.position_size>0 ? color.rgb(0, 255, 0, 90) : strategy.position_size<0 ? color.rgb(255, 0, 0, 90) : color.rgb(33, 150, 243, 95))

```

> Detail

https://www.fmz.com/strategy/430664

> Last Modified

2023-10-31 14:30:45
