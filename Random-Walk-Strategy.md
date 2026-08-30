
> Name

Random-Walk-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The random walk strategy is an automated trading strategy based on random number generation. This strategy uses a linear congruential generator to randomly generate numbers based on the set seed. Go long when the number is greater than the threshold, go short when it is less than the threshold, and achieve random entry into long and short positions.
## Strategy Principle
This strategy mainly implements random trading through the following parts:
1. Set the parameters a, c and modulus m for random number generation, as well as the initial seed.
2. Define the random number generation function GetRandom, and use the linear congruential algorithm to generate random numbers between 0-m.
3. At each K line, if there is currently no position, compare the size of the generated random number. If it is greater than m/2, go long, otherwise go short.
4. Set the stop loss and take profit conditions, and set the stop loss and take profit range in percentage form.
5. Set the backtest period through the time period.
Through the above steps, this strategy achieves completely random long and short operations. When the random number is greater than m/2, open a long order, otherwise open a short order, and then set a stop loss and take profit to exit the position. The backtest period can be customized.
## Advantage Analysis
- The strategy logic is simple and clear, easy to understand and implement.
- Random trading can effectively avoid the influence of human emotions and reduce subjective misoperations.
- You can customize the random number generation algorithm parameters and adjust the randomness.
- Stop loss and profit conditions can be flexibly set to control single profit and loss.
- Supports backtest parameter optimization to facilitate testing of the impact of different parameters on overall returns.
## Risk Analysis
- Random trading may not have a clear trend for a long time, and there is uncertainty in returns.
- Unable to adjust positions according to market conditions and may miss trend opportunities.
- The single profit is limited and the risk of retracement is high.
- It is necessary to set a reasonable stop-loss and stop-profit ratio to avoid excessive losses.
- Randomness may lead to frequent opening and closing of positions, increasing transaction fees.
- Full backtesting is required to verify the rationality of parameter settings and cannot be used blindly.
Risks can be reduced by adding functions such as trend judgment, reducing the number of random openings, optimizing the stop loss mechanism, and strictly controlling single profits and losses.
## Optimization direction
- Increase trend judgment and avoid opening positions against the trend.
- Add position management and adjust the position size according to changes in funds.
- Optimize the random number generation algorithm to improve randomness.
- Dynamically adjust stop loss and take profit ranges.
- Added position opening frequency limit.
- Multi-parameter combination backtesting to find optimal parameters.
## Summarize
The random walk strategy realizes mechanical trading by controlling long and short positions through random numbers. This strategy is highly random, not affected by personal emotions, and avoids the risk of subjective misoperation. However, opening a position randomly may also miss the trend opportunity, and the single profit is limited, so the risk control mechanism needs to be optimized. Overall, this strategy is suitable for verifying trading concepts and understanding the impact of parameter settings on returns, but actual application requires careful evaluation.
||


## Overview

The random walk strategy is an automated trading strategy based on random number generation. It uses a linear congruential generator to randomly generate numbers based on a set seed. When the number is greater than a threshold it goes long, when less it goes short, implementing random entry long/short.

## Strategy Logic

The main parts implementing the random trading are:

1. Set the parameters a, c and modulus m for random number generation, as well as the initial seed. 

2. Define the random number generation function GetRandom using the linear congruential algorithm to generate random numbers between 0-m.

3. On each candlestick, if there is no position, compare the generated random number size, go long when greater than m/2, otherwise go short.

4. Set stop loss and take profit conditions in percentage.

5. Set backtest period by timeframe.

Through the above steps, the strategy realizes fully random long/short operations. When random number is greater than m/2 it opens long position, otherwise it opens short, then sets stop loss and take profit to exit positions. The backtest period is customizable.

## Advantage Analysis

- Simple and clear strategy logic, easy to understand and implement.

- Random trading effectively avoids emotional impacts and reduces subjective misoperations.

- Customizable random number generation parameters to adjust randomness.

- Flexible stop loss and take profit settings to control single profit/loss.

- Supports parameters optimization through backtesting different parameters' impact on total profit.

## Risk Analysis

- Random trading may result in undefined long term trend and uncertain profitability.

- Unable to adjust positions based on market conditions, could miss trend opportunities.

- Limited single profit, high drawdown risk.

- Needs reasonable stop loss/take profit ratio to avoid significant losses.

- Frequent open/close positions due to randomness increases trading costs.

- Sufficient backtesting required to verify reasonable parameter settings, do not blindly use.

Risks could be reduced by adding trend judgment, optimizing stop loss mechanism, strictly controlling single profit/loss etc.

## Improvement Directions

- Add trend judgment to avoid trading against trend.

- Add position sizing based on capital change.

- Optimize random number generation algorithm for better randomness.

- Dynamic stop loss/take profit percentage.

- Limit order frequency. 

- Multi-parameter backtest optimization.

## Summary

The random walk strategy realizes mechanical trading through random number controlled long/short. It has strong randomness and avoids emotional impacts and subjective misoperations. But random entries may also miss trend opportunities, limited single profit, needs optimized risk control mechanisms. Overall the strategy is suitable for verifying trading ideas, evaluating parameter impacts, but careful evaluation is needed for practical use.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|seed|
|v_input_2|30|Stop loss percentage(0.1%)|
|v_input_3|30|Take profit percentage(0.1%)|
|v_input_4|false|Custom Backtesting Dates|
|v_input_5|2018|Backtest Start Year|
|v_input_6|3|Backtest Start Month|
|v_input_7|6|Backtest Start Day|
|v_input_8|8|Backtest Start Hour|
|v_input_9|2018|Backtest Stop Year|
|v_input_10|12|Backtest Stop Month|
|v_input_11|14|Backtest Stop Day|
|v_input_12|14|Backtest Stop Hour|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-02 00:00:00
end: 2023-10-08 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//@author=Tr0sT
strategy(title = "Random strategy", shorttitle = "Random", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)

a = 16
c = 10
m = 1000
GetRandom(prev) =>
    GetRandom = (a * prev + c) % m

seed = input(200, minval = 2, maxval = m)
stopLoss = input(30, title = "Stop loss percentage(0.1%)")
takeProfit = input(30, title = "Take profit percentage(0.1%)")


curRandom = na
curRandom := nz(curRandom[1]) == 0 ? seed : GetRandom(curRandom[1])
if (strategy.position_size == 0)
    if (curRandom >= m / 2)
        strategy.entry("Enter", strategy.long)
    else
        strategy.entry("Enter", strategy.short)
        
    strategy.exit("Exit", "Enter", loss = close * stopLoss / 1000 / syminfo.mintick, profit = close * takeProfit / 1000 / syminfo.mintick)            

// === Backtesting Dates ===
testPeriodSwitch = input(false, "Custom Backtesting Dates")
testStartYear = input(2018, "Backtest Start Year")
testStartMonth = input(3, "Backtest Start Month")
testStartDay = input(6, "Backtest Start Day")
testStartHour = input(08, "Backtest Start Hour")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,testStartHour,0)
testStopYear = input(2018, "Backtest Stop Year")
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

https://www.fmz.com/strategy/428805

> Last Modified

2023-10-09 16:10:24
