
> Name

Monthly-Trend-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/106a0a3b55b4b738b3e.png)

[trans]

## Overview
The Monthly Trend Breakout Strategy is a TradingView indicator based on the pine script. This strategy uses a combination of adaptive moving averages, trendline breakouts, and the RSI indicator to identify long entry opportunities only once a month. When the RSI indicator shows overbought, close the position and exit.
## Strategy Principle
1. Define the variable lastEntryMonth to record the previous entry month. currentMonth gets the current month.
2. Set the TRAMA adaptive moving average parameter length=99 to smooth the price and determine the trend direction.
3. Set the parameter length_trend=14 and draw the high trend line upper. When the price crosses the trend line, it is judged as a breakthrough.
4. Calculate the RSI indicator parameter rsiLength=14 and determine whether it is overbought or oversold.
5. Entry logic: When the closing price is higher than TRAMA and the closing price breaks through the upper track, if you did not enter the market last month, enter long.
6. Exit logic: When RSI is greater than 70, close the position.
7. Draw the TRAMA curve and the overbought line of RSI to complete the strategy.
This strategy combines three major mainstream technical indicators to determine the trend, momentum and overbought and oversold conditions, and looks for lower-risk long opportunities that only occur once a month. At the same time, it is restricted to enter the market only when the price breaks through the upward trend to avoid invalid operations in the consolidation range.
## Advantage Analysis
1. A combination of multiple indicators to comprehensively judge the market status and improve the accuracy of decision-making.
2. Only enter when the monthly time frame breaks out and avoid frequent trading.
3. Use adaptive moving averages to determine the trend direction and quickly capture turning points.
4. Combine with overbought indicators to avoid market highs and effectively control risks.
5. Simple and intuitive entry and exit conditions, easy to master.
6. You can adjust parameters according to your own needs to obtain better strategy optimization.
## Risk Analysis
1. Whipsaw risk caused by failure of breakthrough. After entering the market, if the price falls below the upper track again, losses may occur.
2. If the trend breaks through poorly, you will choose to enter the market at a high level near the top.
3. Improper setting of indicator parameters causes the indicator to produce misleading signals.
4. Breakthroughs only reflect recent market volatility. Consider adaptive stops/position sizing.
5. Monitor risk/reward. Consider only trading pullbacks or adding other confirmation filters.

6. Validate indicators on multiple timeframes. Use higher timeframes to identify trend and lower for entry.

7. Backtest over different market conditions. Optimize parameters to match strategy to market type.

## Optimization direction
1. Add Volume and MA trading volume indicator confirmation to avoid low-volume false breakthroughs.
2. When closing a position when RSI is overbought, consider partial profit stop loss and leave the remaining position.
3. Optimize moving average parameters, adapt to changes, and better track trend transitions.
4. Set up a range before and after the breakthrough point to avoid entering the market directly at the high turning point.
5. Add more filtering conditions, such as channel indicators, volatility indicators, etc., to improve decision-making accuracy.
6. Graded entry, when the price continues to break through the new resistance line, you can increase your position.
## Summarize
The monthly trend breakout strategy takes into account a variety of factors including trend, energy and extreme conditions. It determines the trend direction on the monthly time frame and executes entry in combination with breakthroughs on the lower time frame. At the same time, use the RSI indicator to effectively control trading risks. This strategy uses simple logic to find the best long opportunity once a month. It considers both trend following and risk management. Through parameter optimization, it can be adjusted for different market environments. Generally speaking, the monthly trend breakthrough strategy is a trading strategy that is both simple and practical and focuses on risk control.
|| 

## Overview

The Monthly Trend Breakout Strategy is a TradingView indicator based on Pine Script. It combines an adaptive moving average, trendline breakouts and the RSI indicator to determine long entry signals once per month. Exits occur when the RSI shows overbought conditions.

## Strategy Logic

1. Define variable lastEntryMonth to track last entry month. currentMonth gets current month.

2. Set TRAMA adaptive MA parameters length=99 to smooth price and determine trend.

3. Set length_trend=14 to plot trendline upper based on pivot highs. Long when price breaks above trendline.

4. Calculate RSI indicator with rsiLength=14 to determine overbought/oversold. 

5. Entry logic: Go long if close > TRAMA and close breaks above upper trendline, if no entry last month.

6. Exit logic: Close long if RSI > 70 (overbought).

7. Plot TRAMA line and RSI overbought level 70.

The strategy combines 3 major technical indicators to find low risk long entries once per month. Entries are limited to trend breaks only, avoiding whipsaws in ranges.

## Advantages

1. Combines multiple indicators for robust market analysis and higher accuracy.

2. Limits entries to monthly timeframe, avoiding overtrading.

3. Adaptive MA quickly adapts to trend changes.

4. Oversold RSI avoids buying at market tops and controls risk.

5. Simple entry/exit rules are easy to implement.

6. Customizable parameters allow strategy optimization.

## Risks

1. Whipsaw risk if breakout fails. Stop loss if price breaks back below trendline.

2. Poor timing leads to entries near tops.

3. Bad indicator parameters cause misleading signals. 

4. Breakouts may Reflect recent market volatility. Consider adaptive stops/position sizing.

5. Monitor risk/reward. Consider only trading pullbacks or adding other confirmation filters.

6. Validate indicators on multiple timeframes. Use higher timeframes to identify trend and lower for entry. 

7. Backtest over different market conditions. Optimize parameters to match strategy to market type.

## Optimization

1. Add volume indicator to avoid false breakouts with low volume.

2. Consider partial profit taking on RSI overbought exit, keeping partial position.

3. Optimize MA parameters to better adapt to trend changes. 

4. Add zones before/after breakout point to avoid buying right at reversal.

5. Add more filters like channels, volatility for higher accuracy.

6. Scale in with additional breakouts at new resistance levels.

## Conclusion

The Monthly Trend Breakout Strategy analyzes trend, momentum and extremes. It determines trend on monthly timeframe but enters on shorter timeframe breakouts. RSI oversees risk management. Simple logic identifies optimized monthly long entries. It balances trend following and risk controls. Parameter optimization adapts it to different market conditions. Overall, this is a simple yet robust strategy combining usability and effective risk management.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|99|length_trama|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-17 00:00:00
end: 2023-10-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('Bannos Strategy', shorttitle='Bannos', overlay=true)

//The provided script is an indicator for TradingView written in Pine Script version 5. The indicator is used to determine entry and exit points for a trading strategy. Here's a detailed breakdown of what the script does:

// Strategy Definition:

// Bannos Strategy is the full name, with a short title Bannos.
// The overlay=true option indicates that the strategy will be overlayed on the price chart.
// Tracking Entry Month:

// A variable lastEntryMonth is set up to track the month of the last entry.
// currentMonth identifies the current month.
// Trend Regularity Adaptive Moving Average (TRAMA):

// It takes an input of length 99 as default.
// It uses adaptive calculations to track trend changes.
// Trendlines with Breaks:

// Identifies local peaks over a given period (in this case, 14) and calculates a slope based on these peaks.
// Relative Strength Index (RSI):

// Uses a length of 14 (default) to calculate the RSI.
// RSI is an oscillation indicator that indicates overbought or oversold conditions.
// Strategy Logic for Long Entry:

// A long position is opened if:
// The close price is above the TRAMA.
// There's a crossover of the close price and the upper trendline.
// The position is taken only once per month.
// Strategy Logic for Long Exit:

// The long position is closed if the RSI exceeds 70, indicating an overbought condition.
// Plotting:

// The TRAMA is plotted in red on the chart.
// A horizontal line is also drawn at 70 to indicate the RSI's overbought zone.
// In summary, this strategy aims to enter a long position when certain trend and crossover conditions are met, and close the position when the market is considered overbought as per the RSI. Additionally, it ensures entries only occur once a month.
//



// Variable pour suivre le mois de la dernière entrée
var float lastEntryMonth = na
currentMonth = month(time)

// Parameters for Trend Regularity Adaptive Moving Average (TRAMA)
length_trama = input(99)
src_trama = close
ama = 0.
hh = math.max(math.sign(ta.change(ta.highest(length_trama))), 0)
ll = math.max(math.sign(ta.change(ta.lowest(length_trama)) * -1), 0)
tc = math.pow(ta.sma(hh or ll ? 1 : 0, length_trama), 2)
ama := nz(ama[1] + tc * (src_trama - ama[1]), src_trama)

// Parameters for Trendlines with Breaks
length_trend = 14
mult = 1.0
ph = ta.pivothigh(length_trend, length_trend)
upper = 0.
slope_ph = 0.
slope_ph := ph ? mult : slope_ph
upper := ph ? ph : upper - slope_ph

// Parameters for RSI
rsiLength = 14
up = ta.rma(math.max(ta.change(close), 0), rsiLength)
down = ta.rma(-math.min(ta.change(close), 0), rsiLength)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))

// Strategy Logic for Long Entry
longCondition = close > ama and ta.crossover(close, upper) and (na(lastEntryMonth) or lastEntryMonth != currentMonth)
if (longCondition)
    lastEntryMonth := currentMonth
    strategy.entry('Long', strategy.long)

// Strategy Logic for Long Exit
exitCondition = rsi > 70
if (exitCondition)
    strategy.close('Long')

// Plotting
plot(ama, 'TRAMA', color=color.red)
hline(70, 'Overbought', color=color.red)

```

> Detail

https://www.fmz.com/strategy/430051

> Last Modified

2023-10-24 16:08:33
