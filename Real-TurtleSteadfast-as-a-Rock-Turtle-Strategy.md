
> Name

Real-TurtleSteadfast-as-a-Rock-Turtle-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17395aa63e37b6c45b6.png)
[trans]
## Overview
The Rock Solid Turtle Strategy is a quantitative trading strategy that follows the Brady Turtle Trading Rules. It adopts the method of entry when price breaks and stop-loss tracking to exit, calculates the position size based on the real volatility, and strictly controls single losses. This strategy operates stably in the long term and has strong resistance to decline and retracement, just like a solid rock.
## Strategy Principle
### Admission rules
The rock solid Turtle strategy on breakout entries. Specifically, it will calculate the highest price and lowest price within a certain period based on the input breakthrough cycle parameters. When the price breaks through the highest price, enter the long position; when the price breaks through the lowest price, enter the short position.
For example, if the entry cycle parameter is set to 20 K lines, then the strategy will extract the highest and lowest prices of the last 20 K lines. If the closing price of the current K-line is higher than the highest price of the past 20 K-lines, the strategy will issue a long stop order at the closing price and wait for the entry to be made if the highest price is exceeded.
### Rules of appearance
The rock solid Turtle strategy is trailing the stop on the exit. It will dynamically calculate the highest price and lowest price within a certain period based on the input exit cycle parameters. This becomes the strategy's exit channel.
When holding a long position, if the price falls below the lowest price of the exit channel, the position will be stopped and exited. On the other hand, when holding a short position, if the price rises above the highest price of the exit channel, the position will be stopped and exited.
In addition, the strategy will also calculate the stop loss position based on the true volatility as the final stop loss line. As long as the price does not break through the exit channel, the stop loss position will be tracked and corrected to ensure that the stop loss distance is just right. It will not be too aggressive and cause unnecessary stop loss, nor will it be too far away to effectively control losses.
### Position size
The rock-solid Turtle strategy calculates individual position sizes based on true volatility. Specifically, it will first measure the potential loss percentage near the entry price, and then infer the position size based on the expected risk parameters. This can effectively control the maximum loss of each transaction.
## Advantage Analysis
### Stable operation
The rock-solid Turtle strategy follows the Brady Turtle trading rules, strictly enforces the entry and exit rules, and does not change them at will. This allows the strategy to operate stably for a long time without causing system failure due to temporary errors in judgment.
### Anti-retracement
The strategy adopts price breakthrough entry method, which can effectively avoid the risk of high Fault entry, thus reducing the possibility of systematic losses. At the same time, the stop-loss trailing stop method is adopted to ensure single loss control and to minimize the occurrence of retracement caused by continuous losses.
### Risk controllable
The strategy calculates positions through true volatility, strictly controls the maximum loss of each transaction within the allowable range, and avoids risk spillover caused by a single large loss. At the same time, the stop-loss tracking method is used to ensure that the stop-loss distance is appropriate, the loss can be stopped in time, and the risk can be effectively controlled.
## Risk Analysis
### Breakthrough Failure Risk
If the market fluctuates and breaks through without volume, it is easy to form false signals and lead to system errors and losses. At this time, it is necessary to adjust parameters and increase entry confirmation conditions to avoid noise interference from invalid breakthroughs.
### Parameter optimization risk
The parameters of the strategy such as entry period, exit period, etc. are all set statically. If the market environment changes significantly, these parameter settings may become invalid. At this time, it is necessary to re-evaluate the parameter settings and optimize the parameters to adapt to the new market status.
### Technical indicator failure risk
The strategy uses technical indicators such as price breakout judgment flags. These technical indicators may become ineffective when market trends and volatility patterns change significantly. At this time, it is necessary to introduce more technical indicators to judge the reliability of the overall optimization strategy.
## Optimization direction
### Add trend judgment
Commonly used trend judgment indicators, such as MA, MACD, etc., can be added to the strategy. Judging the upward trend when going long and judging the downward trend when going short can reduce losses in reverse operations.
### Multiple time frame judgment
Technical indicators in a higher-level time frame can be introduced to make comprehensive judgments. For example, the MA line position at the 86400 level can determine the overall trend direction and further confirm the operation signal on the time-sharing chart.
### Dynamic parameter optimization
Parameters can be automatically optimized based on historical data through machine learning and other means, and parameters can be adjusted in real time to adapt to changes in the market environment. This can make the strategy more adaptable and stable.
## Summarize
The rock-solid turtle strategy follows the classic turtle trading rules, using price breakthrough entry and stop-loss trailing stop-loss exit. It strictly controls risks, can operate stably in the long term, and has excellent ability to withstand declines and retracements. Although there are still some risks such as breakthrough failure and parameter failure that need to be guarded against, these risks can be effectively reduced and the stable operation capability of the strategy can be greatly improved by introducing trend judgment, time frame judgment, dynamic parameter optimization and other means. Overall, this strategy has excellent stability and ability to withstand declines and retracements, and is worthy of trust and holding.
||

## Overview

Steadfast as a Rock Turtle strategy is a quantitative trading strategy that follows the rules of the Brady turtle trading methodology. It uses price breakout to enter positions and stops tracking stops for exit. It calculates position sizing based on true volatility and strictly controls losses per trade. The strategy has long-term stability in operation and strong tolerance for drawdowns, much like steadfast rocks.

## Principle 

### Entry Rule

Steadfast as a Rock Turtle strategy enters on breakouts. Specifically, it calculates the highest high and lowest low over the specified lookback period. When price breaks above highest high, it goes long. When price breaks below lowest low, it goes short. 

For example, with an entry period set to 20 bars, the strategy extracts the highest high and lowest low over the past 20 bars. If the close of the current bar exceeds the highest high of past 20 bars, the strategy would place a long stop order at that close price to prepare for breakout above the highest high.

### Exit Rule

Steadfast as a Rock Turtle strategy exits with stops tracking stops. It dynamically calculates highest high and lowest low over the specified exit period and uses them to determine the exit channel.

If holding long, once price drops below the lowest low of exit channel, the position would stop out. Vice versa for short position.

Additionally, the strategy calculates a stop-loss level based on true volatility, which serves as the final stop. As long as price remains above exit channel, the stop-loss will keep tracking and adjusting, making sure the stops are set at appropriate distances—not too tight for unnecessary stopouts, not too loose for risk control.

### Position Sizing

Steadfast as a Rock Turtle strategy sizes its positions based on true volatility. Specifically, it first estimates the potential loss percentage near entry price, then reverse calculates position size from expected risk parameter. This effectively controls the max loss per trade.

## Advantage Analysis

### Steady Operation  

Steadfast as a Rock Turtle strategy adheres strictly to classic turtle trading rules on entries and exits without arbitrary modifications. This allows the strategy to run steadily for the long haul without system failure due to temporary poor judgement.

### Drawdown Resilience

By entering on breakouts, the strategy avoids overvalued entries effectively, reducing the probability of system losses. And by exiting with stops tracking stops, it ensures max loss per trade is controlled to largely prevent consecutive losses leading to deep drawdowns.  

### Risk Containability  

By sizing based on true volatility, the strategy strictly controls the max loss per trade within tolerance. And by tracking stop distances, it can cut losses in time to effectively contain risks.

## Risk Analysis

### Breakdown Failure Risk

If price breaks out with low momentum, it may turn out to be false signal causing wrong entry losses. Parameters would need adjustment with more entry confirmation rules to avoid ineffective breakout noise.  

### Parameter Optimization Risk

Static strategy parameters like entry/exit periods could become invalid if market regime changes drastically. These parameters would need reevaluation and re-optimization to adapt.

### Technical Indicator Failure Risk

Indicators used like price breakout flags could fail when trend or volatility changes significantly. More techniques would need integration to improve strategy reliability.

## Optimization Directions 

### Add Trend Filter  

Common trend indicators like MA, MACD can be added. Go long only in uptrend and short only in downtrend to avoid countertrend whipsaws.

### Timeframe Synthesis  

Higher timeframe indicators, e.g. Daily MA levels, can help confirm overall direction to supplement lower timeframe signals.

### Dynamic Parameter Tuning      

Machine learning can auto update strategy parameters continually based on latest data to maintain efficacy in changing market dynamics.

## Summary
Steadfast as a Rock Turtle strategy follows the classic turtle trading methodology strictly—breakout entry and tracking stop exit with stringent risk control. This allows long-term steady operations with strong drawdown resilience. Despite risks like false breakout, parameter failure etc, these can be effectively mitigated via additions like trend filter, timeframe synthesis, dynamic tuning etc to significantly improve strategy stability. Overall an excellently robust strategy well worth trusting and holding.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2016|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2030|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|30|Backtest Stop Day|
|v_input_7|false|Color Background?|
|v_input_8|20|Entry Channel Length|
|v_input_9|10|Exit Channel Length|
|v_input_10|13|True Range Length|
|v_input_11|false|Use whole position on every trade|
|v_input_12|2|Use Desired Risk %|
|v_input_13|2|Desired multiple of ema Tr (N)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-18 00:00:00
end: 2024-02-17 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Real Turtle", shorttitle = "Real Turtle", overlay=true, pyramiding=1, default_qty_type= strategy.percent_of_equity,calc_on_order_fills=false, slippage=25,commission_type=strategy.commission.percent,commission_value=0.075)
//////////////////////////////////////////////////////////////////////
// Testing Start dates
testStartYear = input(2016, "Backtest Start Year")
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)
//Stop date if you want to use a specific range of dates
testStopYear = input(2030, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(30, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,0,0)

// A switch to control background coloring of the test period
// Use if using a specific date range
testPeriodBackground = input(title="Color Background?", type=bool, defval=false)
testPeriodBackgroundColor = testPeriodBackground and (time >= testPeriodStart) and (time <= testPeriodStop) ? #00FF00 : na
bgcolor(testPeriodBackgroundColor, transp=97)

testPeriod() => true
// Component Code Stop
//////////////////////////////////////////////////////////////////////

//How many candles we want to determine our position entry
enterTrade = input(20, minval=1, title="Entry Channel Length")
//How many candles we want ot determine our position exit
exitTrade = input(10, minval=1, title="Exit Channel Length")

//True Range EMA Length
trLength = input(13, minval=1, title="True Range Length")
//Go all in on every trade
allIn = input(false, title="Use whole position on every trade")
dRisk = input(2, "Use Desired Risk %")
//How much of emaTR to use for TS offset
multiEmaTR = input(2, "Desired multiple of ema Tr (N)")
//absolute value (highest high of of this many candles - lowest high of this many candles) . This is used if we want to change our timeframe to a higher timeframe otherwise just works like grabbing high o r low of a candle
//True range is calculated as just high - low. Technically this should be a little more complicated but with 24/7 nature of crypto markets high-low is fine.
trueRange = max(high - low, max(high - close[1], close[1] - low))
//Creates an EMA of the true range by our custom length
emaTR = ema(trueRange, trLength)
//Highest high of how many candles back we want to look as specified in entry channel for long
longEntry = highest(enterTrade)
//loweest low of how many candles back we want to look as specified in exit channel for long
exitLong = lowest(exitTrade)
//lowest low of how many candles back want to look as specified in entry channel for short
shortEntry = lowest(enterTrade)
//lowest low of how many candles back want to look as specified in exit channel for short
exitShort = highest(exitTrade)
//plots the longEntry as a green line
plot(longEntry[1], title="Long Entry",color=green)
//plots the short entry as a purple line
plot(shortEntry[1], title="Short Entry",color=purple)

howFar = barssince(strategy.position_size == 0)
actualLExit = strategy.position_size > 0 ? strategy.position_avg_price - (emaTR[howFar] * multiEmaTR) : longEntry - (emaTR * multiEmaTR)
actualLExit2 = actualLExit > exitLong ? actualLExit : exitLong
actualSExit = strategy.position_size < 0 ? strategy.position_avg_price + (emaTR[howFar] * multiEmaTR) : shortEntry + (emaTR * multiEmaTR)
actualSExit2 = actualSExit < exitShort ? actualSExit : exitShort

//plots the long exit as a red line
plot(actualLExit2[1], title="Long Exit",color=red)
//plots the short exit as a blue line
plot(actualSExit2[1], title="Short Exit",color=yellow)


//Stop loss in ticks
SLLong =(emaTR * multiEmaTR)/ syminfo.mintick
SLShort = (emaTR * multiEmaTR)/ syminfo.mintick


//Calculate our potential loss as a whole percentage number. Example 1 instead of 0.01 for 1% loss. We have to convert back from ticks to whole value, then divided by close
PLLong = ((SLLong * syminfo.mintick) * 100) / longEntry
PLShort = ((SLShort * syminfo.mintick) * 100) / shortEntry
//Calculate our risk by taking our desired risk / potential loss. Then multiple by our equity to get position size. we divide by close because we are using percentage size of equity for quantity in this script as not actual size.
//we then floor the value. which is just to say we round down so instead of say 201.54 we would just input 201 as TV only supports whole integers for quantity.
qtyLong = floor(((dRisk / PLLong) * strategy.equity) /longEntry )
qtyShort = floor(((dRisk / PLShort) * strategy.equity) /shortEntry )
qtyLong2 = allIn ? 100 : qtyLong
qtyShort2 = allIn ? 100 : qtyShort
//Only open long or short positions if we are inside the test period specified earlier
if testPeriod()
    //Open a stop market order at our long entry price and keep it there at the quantity specified. This order is updated/changed on each new candlestick until a position is opened
    strategy.entry("long", strategy.long, stop = longEntry, qty = qtyLong2) 
    //sets up or stop loss order by price specified in our actualLExit2 variable
    strategy.exit("Stoploss-Long", "long", stop=actualLExit2)
    
     //Open a stop market order at our short entry price and keep it there at the quantity specified. This order is updated/changed on each new candlestick until a position is opened
    strategy.entry("short", strategy.short, stop = shortEntry, qty = qtyShort2)
    //sets up or stop loss order by price specified in our actualLExit2 variable
    strategy.exit("Stoploss-Short", "short", stop=actualSExit2)


```

> Detail

https://www.fmz.com/strategy/441990

> Last Modified

2024-02-18 14:34:40
