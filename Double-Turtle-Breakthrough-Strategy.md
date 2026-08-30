
> Name

Double-Turtle-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/715268dfbd64de6a51f9156af8297269982ebcbc8944d2bdc8794baa992a7e2e.png)

[trans]
#
## Overview
The Double Turtle Breakout Strategy combines the breakthrough strategy of the Turtle Trading Method and the trailing stop principle of Linda Raschke, with excellent breakthrough performance and strict risk control. This strategy monitors both upper and lower price breakouts, establishing a long or short position when a breakout occurs, and manages the position using Trailing Stop Loss and Trailing Take Profit.
## Strategy Principle
The core logic is to go short when the high point of the big cycle breaks through the high point of the small cycle, and go long when the low point of the big cycle breaks through the low point of the small cycle. After opening a position, set a trailing stop loss and a trailing take profit, and first stop the loss to confirm the risk. When the position quantity accumulates to the set take-profit quantity, the stop-loss order will be canceled in the next period, then half the position will be taken out and the trailing stop-loss and trailing take-profit will be set to lock in the profit and track the price difference.
The specific steps are:
1. Calculate the high point prevHigh of the large period (20 periods) and the high point smallPeriodHigh of the small period (4 periods).
2. When the high of the latest K line is greater than prevHigh, and prevHigh is greater than smallPeriodHigh, it indicates that the high of the large cycle breaks through the high of the small cycle. If there is no position at this time, go short.
3. Set a trailing stop loss after opening a position, and cancel the stop loss order after the position is reversed to prevent being stopped.
4. When the number of positions reaches the set number of moving take-profit periods (currently 0 periods), half of the position will be taken out in the next period, and the moving stop-loss and moving take-profit will be set to track the price difference and lock in profits.
5. Similar to the breakthrough of low points, establish a long position based on the breakthrough relationship between large cycle lows and small cycle lows.
## Advantage Analysis
This is a comprehensive breakthrough strategy that also has the following advantages:
1. Combined with the double-cycle turtle trading method, it can effectively identify breakthrough signals.
2. Use trailing stop loss and trailing take profit technology to strictly control risks and avoid huge losses.
3. Enter the market in two times, take profit once to take out half of the position, and then use moving take profit to take out the full position to lock in profits.
4. Taking into account both long and short two-way operations, it conforms to the market characteristics of long and short swaps.
5. The backtesting effect is excellent and it has strong real-time performance capabilities.
## Risk Analysis
The main risks and countermeasures are as follows:
1. Risk of false breakthrough. Cycle parameters should be adjusted appropriately to ensure the effectiveness of the breakthrough.
2. The risk of chasing the rise and killing the fall. Filtering should be done based on trends and patterns to avoid opening positions at the end of the trend.
3. Risk of stop loss being offset. The stop loss range can be appropriately relaxed to ensure there is enough space.
4. Risk of too sensitive trailing stop loss. The slippage setting after stop loss should be adjusted to avoid unnecessary stop loss.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Increase the breakthrough filtering of trading volume to ensure the authenticity of breakthroughs.
2. Add trend judgment indicators to avoid opening positions at the end of the trend.
3. Combine more time periods to determine the breakthrough opportunity.
4. Add machine learning algorithms and dynamically optimize parameters.
5. Combine other strategies to implement statistical arbitrage.
## Summary
The Double Turtle breakthrough strategy comprehensively uses dual-cycle technology, breakthrough theory and strict risk management methods to maintain a high winning rate while ensuring the stability of returns. This strategy model is simple and clear, easy to understand and apply, and is an excellent quantitative strategy. This strategy also has a lot of room for optimization, and investors can innovate on this basis to create a better trading system.
||

## Overview
The Double Turtle Breakthrough Strategy integrates the turtle trading breakthrough strategy and Linda Raschke's moving stop loss principle, with excellent breakthrough performance and strict risk control. The strategy simultaneously monitors the price breakout up and down, establishes long or short positions when a breakthrough occurs, and uses moving stop loss and moving take profit to manage positions.

## Strategy Principle  
The core logic is to go short when breaking through the small cycle high on the large cycle high point, and go long when breaking through the small cycle low at the large cycle low point. After opening a position, set up a moving stop loss and moving take profit, first stop loss to confirm the risk. When the holding quantity accumulates to the set take profit quantity, cancel the stop loss order in the next cycle, then exit half of the position and set up a moving stop loss and moving take profit to lock in profits and track spreads.


The specific operation steps are:

1. Calculate the large cycle (20 cycles) high point prevHigh and the small cycle (4 cycles) high point smallPeriodHigh.

2. When the high of the latest K-line is greater than prevHigh, and prevHigh is greater than smallPeriodHigh, it indicates that the large cycle high point breaks through the small cycle high point. At this time, if there is no position, go short.

3. After opening a position, set a moving stop loss. Wait for the position to reverse before cancelling the stop loss order to prevent being stopped out.  

4. When the holding quantity reaches the set moving take profit cycle number (currently 0 cycles), exit half of the position in the next cycle, and set up a moving stop loss and moving take profit to track the spread and lock in profits.

5. For breakthroughs of low points, long positions are established based on breakthrough relationships between large cycle lows and small cycle lows.


## Advantage Analysis
This is a highly comprehensive breakthrough strategy with the following advantages:

1. Combining double cycle turtle trading can effectively identify breakthrough signals.

2. The use of moving stop loss and moving take profit techniques strictly controls risks and avoids huge losses.

3. Exiting in two stages, taking profit half position at a time, then fully exiting through moving take profit, locking in profits.

4. Take into account both long and short operations, matching the characteristics of alternating multi-empty markets.

5. Excellent backtesting results with strong real trading performance.


## Risk Analysis
The main risks and countermeasures are as follows:

1. Risk of false breakthroughs. Appropriately adjust cycle parameters to ensure breakthrough validity.

2. Risk of chasing rises and kills falls. Filtering should be combined with trends and patterns to avoid opening positions at the end of trends.

3. Risk of stop loss being washed out. Appropriately relax the stop loss amplitude to ensure sufficient space.  

4. Risk of overly sensitive moving stop loss. Adjust slippage settings after stop loss to avoid unnecessary stop outs.


## Optimization Directions
The strategy can also be optimized in the following aspects:

1. Add volume breakthrough filters to ensure authenticity of breakthroughs.  

2. Add trend judgment indicators to avoid opening positions at the end of trends.

3. Combine more time cycles to determine breakthrough timing.

4. Increase machine learning algorithms for dynamic optimization of parameters. 

5. Combine with other strategies for statistical arbitrage.


## Summary 
The Double Turtle Breakthrough Strategy comprehensively uses double cycle techniques, breakthrough theories and strict risk management methods to ensure high win rates while ensuring stable returns. This strategy model is simple and clear, easy to understand and apply, and it is an excellent quantitative strategy. This strategy still has great potential for optimization. Investors can innovate on this basis to create even better trading systems.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|bigPeriod|
|v_input_2|4|smallPeriod|
|v_input_3|false|takeProfitBars|
|v_input_4|5|Trailing stop percentages|
|v_input_5|false|Custom Backtesting Dates|
|v_input_6|2018|Backtest Start Year|
|v_input_7|3|Backtest Start Month|
|v_input_8|6|Backtest Start Day|
|v_input_9|8|Backtest Start Hour|
|v_input_10|2038|Backtest Stop Year|
|v_input_11|12|Backtest Stop Month|
|v_input_12|14|Backtest Stop Day|
|v_input_13|14|Backtest Stop Hour|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-21 00:00:00
end: 2023-11-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(title = "Turtle soup plus one", shorttitle = "Turtle soup plus one", overlay=true)

bigPeriod = input(20)
smallPeriod = input(4)
takeProfitBars = input(0)
trailingStop = input(5, title = "Trailing stop percentages")
if (strategy.position_size == 0)
    strategy.cancel("Long")
    strategy.cancel("Short")
    strategy.cancel("Stop")



stopLossPrice = 0.1
stopLossPrice := nz(stopLossPrice[1])
takeProfitStarted = false
takeProfitStarted := nz(takeProfitStarted[1])

prevHigh = highest(high, bigPeriod - smallPeriod)[smallPeriod]
smallPeriodHigh = highest(high, smallPeriod - 1)[1]
if (high > prevHigh and prevHigh > smallPeriodHigh and close > prevHigh and strategy.position_size == 0)
    strategy.order("Short", strategy.short, stop = prevHigh)

if strategy.position_size < 0 and strategy.position_size[1] == 0
    stopLossPrice := high[1]
    strategy.order("Stop", strategy.long, qty = -strategy.position_size, stop = stopLossPrice)
    takeProfitStarted := false

if (strategy.position_size < 0 and sum(strategy.position_size, takeProfitBars) == strategy.position_size * takeProfitBars and close < strategy.position_avg_price and not takeProfitStarted)
    takeProfitStarted := true
    strategy.cancel("Stop")
    strategy.order("ExitHalf", strategy.long, qty = ceil(-strategy.position_size / 2), stop = close)
    if (strategy.position_size != -1)
        strategy.exit("ExitFull", "Short", qty = -strategy.position_size - ceil(-strategy.position_size / 2), loss = stopLossPrice, trail_price  = close, trail_offset = -(close - strategy.position_avg_price) * trailingStop / 100 / syminfo.mintick)
        

prevLow = lowest(low, bigPeriod - smallPeriod)[smallPeriod]
smallPeriodLow = lowest(low, smallPeriod - 1)[1]
if (low < prevLow and prevLow < smallPeriodLow and close < prevLow and strategy.position_size == 0)
    strategy.order("Long", strategy.long, stop = prevLow)

if strategy.position_size > 0 and strategy.position_size[1] == 0
    stopLossPrice := low[1]
    strategy.order("Stop", strategy.short, qty = strategy.position_size, stop = stopLossPrice)
    takeProfitStarted := false

if (strategy.position_size > 0 and sum(strategy.position_size, takeProfitBars) == strategy.position_size * takeProfitBars and close > strategy.position_avg_price and not takeProfitStarted)
    takeProfitStarted := true
    strategy.cancel("Stop")
    strategy.order("ExitHalf", strategy.short, qty = ceil(strategy.position_size / 2), stop = close)
    if (strategy.position_size != 1)
        strategy.exit("ExitFull", "Long", qty = strategy.position_size - ceil(strategy.position_size / 2),loss = stopLossPrice, trail_price  = close, trail_offset = (close - strategy.position_avg_price) * trailingStop / 100 / syminfo.mintick)

// === Backtesting Dates ===
testPeriodSwitch = input(false, "Custom Backtesting Dates")
testStartYear = input(2018, "Backtest Start Year")
testStartMonth = input(3, "Backtest Start Month")
testStartDay = input(6, "Backtest Start Day")
testStartHour = input(08, "Backtest Start Hour")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,testStartHour,0)
testStopYear = input(2038, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(14, "Backtest Stop Day")
testStopHour = input(14, "Backtest Stop Hour")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,testStopHour,0)
testPeriod() =>
    time >= testPeriodStart and time <= testPeriodStop ? true : false
isPeriod = testPeriodSwitch == true ? testPeriod() : true
// === /END
if not isPeriod
    strategy.cancel_all()
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/433577

> Last Modified

2023-11-28 16:25:41
