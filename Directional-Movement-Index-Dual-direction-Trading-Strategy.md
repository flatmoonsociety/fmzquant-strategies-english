
> Name

Directional-Movement-Index-Dual-direction-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12561eb6474bfab559c.png)
[trans]

## Overview
This strategy realizes two-way trading of commodities by calculating the movement index (DI) of commodities and combining it with restriction parameters. Go long when DI+ is greater than DI- a limit parameter, go short when DI- is greater than DI+ a limit parameter.
## Strategy Principle
The core indicator of this strategy is the Movement Index (DI). DI is calculated by the following formula:
DI+ = (DM+ / true range)×100
DI- = (DM- / true range) × 100
Among them, DM+ represents the long trend and DM- represents the short trend. The true range represents the recent fluctuation range by calculating the maximum value of the three-day highest price, lowest price and yesterday's closing price.
According to the definition of DI, when DI+ > DI-, it means that the power of bulls is greater than the power of shorts in the current market, and it is a long market; when DI- > DI+, it means that the power of shorts is stronger than the power of bulls, and it is a short market.
This strategy takes advantage of this feature and sets a limiting parameter. When DI+ is greater than a limit parameter DI-, it is judged that the current market is a long market and go long; when DI- is greater than a limit parameter DI+, it is judged that the current market is a short market and go short.
For example, if the limit parameter is set to 3, then the specific trading rules are:
1. When DI+ - DI- > 3, go long
2. When DI- - DI+ > 3, go short
Since there are often small difference fluctuations between DI+ and DI-, setting limit parameters can filter out some trading signals with no obvious direction and reduce unnecessary transactions. This is an advantage of this strategy.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Using DI to judge the market direction has strong direction and high reliability.
DI directly determines the market trend by calculating the strength comparison between long and short parties. There are no complex algorithms such as curve fitting, and the theory is simple and reliable.
2. Setting limiting parameters can effectively filter signals
Filter out small fluctuations with no obvious directionality by limiting parameters, and only choose the market segment with strong directionality to trade to avoid being trapped.
3. Implement automatic two-way transactions
Long and short positions can be automatically switched according to the DI indicator, eliminating the need for manual judgment and reducing the difficulty of transactions.
4. Customizable trading time periods
It supports setting up transactions only within a customized date range, and automatically closes the position after the end, which is flexible and convenient.
5. You can choose to only go long or only short according to the situation.
Through the long-short switch, only one-way signals can be selected to achieve only long or short positions to adapt to different market environments.
## Risk Analysis
There are also some risks with this strategy:
1. Possibility of DI sending wrong signals
When the market fluctuates violently, DI may send out wrong signals in the short term, leading to transaction failure. Other indicators need to be combined for verification.
2. Improper setting of restriction parameters
Setting the limit parameters too large or too small may result in too few or too many trading signals, and the parameters need to be adjusted according to the market.
3. Unable to judge the end of the trend
DI can only determine the direction of the current trend, but cannot determine whether the trend has ended or reversed. It requires the combination of other indicators.
Risk-based solutions include:
1. Filter DI signals by combining indicators such as moving averages
2. Adjust restriction parameters based on backtest results
3. Combine Volumes, MACD, etc. to determine whether the trend is reversed
## Optimization direction
This strategy can continue to be optimized from the following aspects:
1. Combined with other trend judgment indicators such as public opinion barometer
Indicators that more intuitively judge long and short strength, such as the public opinion barometer, can be combined with DI to improve the accuracy of judgment.
2. Add a stop-profit and stop-loss strategy
Set trailing stop-profit, time or ratio stop-loss points to lock in profits and reduce losses.
3. Adjust parameters for specific varieties
Adjusting the restriction parameters and trading time according to the trading characteristics of different varieties can improve the strategy effect.
4. Use machine learning technology for dynamic optimization
Apply techniques such as reinforcement learning to optimize parameter settings based on real trading signals.
## Summarize
This strategy is generally simple and practical. It uses the DI calculation method to determine the market direction; filters signals by limiting parameters; it can trade in both directions, or only long or short; it supports setting trading time periods. The main advantages are high reliability and effective signal filtering. At the same time, there are also problems such as sending error signals and parameter settings. We can improve the strategy effect by combining it with other indicators, setting stop loss and profit, adjusting parameters, etc. We can also use machine learning for dynamic optimization. Generally speaking, this strategy is suitable as one of the combined indicators for judging the market direction, and can achieve good results when combined with other strategies.
||

## Overview 

This strategy calculates the Directional Movement Index (DI) of commodities and combines it with limit parameters to implement dual-direction trading. It goes long when DI+ is greater than DI- by a limit parameter and goes short when DI- is greater than DI+ by a limit parameter.

## Strategy Principle

The core indicator of this strategy is the Directional Movement Index (DI). DI is calculated by the following formulas:  

DI+ = (DM+ / True Range) × 100
DI- = (DM- / True Range) × 100

Where DM+ represents the Directional Movement Positive, DM- represents the Directional Movement Negative. The True Range represents the recent volatility by calculating the maximum value of the highest price, the lowest price and the closing price of the previous day over three days.

According to the definition of DI, when DI+ > DI-, it means the current market momentum is stronger, belonging to a bull market; when DI- > DI+, it means the bear momentum is stronger than the bull momentum, belonging to a bear market.

This strategy utilizes this feature and sets a limit parameter. When DI+ is greater than DI- by a limit parameter, it determines that the current market is a bull market and goes long. When DI- is greater than DI+ by a limit parameter, it determines that the current market is a bear market and goes short. 

For example, if the limit parameter is set to 3, the specific trading rules are:

1. When DI+ - DI- > 3, go long
2. When DI- - DI+ > 3, go short

Since there are often small fluctuating differences between DI+ and DI-, setting a limit parameter can filter out some trades without significant directionality and reduce unnecessary trades. This is an advantage of this strategy.

## Advantage Analysis

The main advantages of this strategy are:

1. DI is reliable in judging market directionality

   DI directly judges market trends by calculating the power of bulls and bears. The theory is simple and reliable without complex algorithms like curve fitting.
   
2. The limit parameter can effectively filter signals

   The limit parameter filters small fluctuations without significant directionality, only selecting sections with significant directionality to trade, avoiding being trapped.
   
3. Achieve automated dual-direction trading

   Long and short positions can be automatically switched based on the DI indicator without manual judgment, reducing trading difficulty.

4. Customizable trading time frame

   Supports setting to only trade within a customizable date range and close all positions automatically afterwards, flexible and convenient.

5. Selectable long or short only

   Through the long and short switches, only single-direction signals can be selected to implement long or short only strategies suitable for different market environments.

## Risk Analysis

There are also some risks with this strategy:  

1. Possibility of DI giving wrong signals

   DI may give short-term wrong signals when drastic market fluctuations occur, leading to failed trades. Other indicators need to be combined for verification.

2. Improper limit parameter settings

   Improper high or low limit parameter settings can lead to too few or too many trading signals. The parameters need to be adjusted according to the market.

3. Unable to determine trend endpoint

   DI can only determine the current trend direction and cannot judge whether the trend has ended or reversed. Other indicators need to be combined.

The solutions for the risks include:

1. Combine moving average and other indicators to filter DI signals

2. Adjust limit parameters based on backtest results  

3. Combine Volume, MACD etc. to determine if trend reversal

## Optimization Directions

The strategy can be further optimized in the following ways:

1. Combine other trend judgment indicators like Market Profile

   Combining indicators like Market Profile which also intuitively judge long-short power with DI can improve judgment accuracy.

2. Add stop-profit and stop-loss strategies 

   Setting trailing stop-profit, time or percentage stop-losses can lock in profits and reduce losses.

3. Adjust parameters for specific products

   Adjusting limit parameters and trading times according to different product characteristics can improve strategy performance.
   
4. Dynamic optimization using machine learning

   Applying reinforcement learning algorithms to dynamically optimize parameter settings based on live signals.

## Summary

In summary, this strategy is relatively simple and practical. It utilizes DI’s calculation to determine market direction; filters signals via limit parameters; supports dual-direction trading or long/short only; allows setting trading time frame. The main advantages are high reliability and effective signal filtering. It also has issues like wrong signals and parameter settings. We can improve it by combining other indicators, setting stop-loss/profit, adjusting parameters etc, or dynamically optimizing it with machine learning. Overall it is suitable as a directional indicator to combine with other strategies for decent results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Capital, %|
|v_input_4|14|Length|
|v_input_5|3|limit, %|
|v_input_6|1900|From Year|
|v_input_7|2100|To Year|
|v_input_8|true|From Month|
|v_input_9|12|To Month|
|v_input_10|true|From day|
|v_input_11|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-12-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Noro's DI Strategy", overlay = false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
len = input(title="Length", defval=14)
limit = input(3, title = "limit, %")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//DI
TrueRange = max(max(high-low, abs(high-nz(close[1]))), abs(low-nz(close[1])))
DirectionalMovementPlus = high-nz(high[1]) > nz(low[1])-low ? max(high-nz(high[1]), 0): 0
DirectionalMovementMinus = nz(low[1])-low > high-nz(high[1]) ? max(nz(low[1])-low, 0): 0
SmoothedTrueRange = 0.0
SmoothedDirectionalMovementPlus = 0.0
SmoothedDirectionalMovementMinus = 0.0
SmoothedTrueRange := nz(SmoothedTrueRange[1]) - (nz(SmoothedTrueRange[1])/len) + TrueRange
SmoothedDirectionalMovementPlus := nz(SmoothedDirectionalMovementPlus[1]) - (nz(SmoothedDirectionalMovementPlus[1])/len) + DirectionalMovementPlus
SmoothedDirectionalMovementMinus := nz(SmoothedDirectionalMovementMinus[1]) - (nz(SmoothedDirectionalMovementMinus[1])/len) + DirectionalMovementMinus
DIPlus = SmoothedDirectionalMovementPlus / SmoothedTrueRange * 100
DIMinus = SmoothedDirectionalMovementMinus / SmoothedTrueRange * 100

//Trend
trend = 0
trend := DIPlus > DIMinus + limit ? 1 : DIPlus < DIMinus - limit ? -1 : trend[1]

//Background
col = trend == 1 ? lime : red
bgcolor(col, transp = 80)

//Lines
plot(DIPlus, color=lime, title="DI+", linewidth = 3)
plot(DIMinus, color=red, title="DI-", linewidth = 3)

//Trading
size = strategy.position_size
lot = 0.0
lot := size != size[1] ? strategy.equity / close * capital / 100 : lot[1]
if trend == 1
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
if trend == -1
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/435871

> Last Modified

2023-12-19 14:13:52
