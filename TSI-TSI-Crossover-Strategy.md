
> Name

TSI-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/91f8e060a4d99d6ab35e5b8045d5600b623ccb2ddf646e0edc0cf8350e3dd352.png)

[trans]
#### Overview
This strategy uses the TSI indicator as the main trading signal. When the TSI indicator crosses its signal line and the TSI indicator is lower than the lower limit or higher than the upper limit, the strategy will generate a signal to open a position. At the same time, the strategy also uses indicators such as EMA and ATR to optimize strategy performance. The strategy only runs during specific trading sessions and has a minimum trading frequency set to control overtrading.
#### Strategy Principle
1. Calculate TSI indicator value and signal line value.
2. Determine whether the current time range is within the allowed trading time range, and the current bar is at least the specified minimum number of bars away from the last transaction.  
3. If the TSI indicator crosses the signal line from bottom to top and the signal line is lower than the specified lower limit at this time, a long signal will be generated.
4. If the TSI indicator crosses the signal line from top to bottom and the signal line is higher than the specified upper limit, a short signal will be generated.
5. If you currently hold a long position, once the TSI indicator crosses the signal line from top to bottom, all long positions will be closed.
6. If you currently hold a short position, once the TSI indicator crosses the signal line from bottom to top, all short positions will be closed.
#### Advantage Analysis
1. The strategy logic is clear, using the cross of the TSI indicator as the only condition for opening and closing positions, which is simple and easy to understand.
2. By limiting trading periods and trading frequency, the risk of over-trading is effectively controlled.
3. Stop losses and profits in a timely manner, and decisively close positions once opposite signals appear, thus controlling the risk exposure of a single transaction.
4. Use multiple indicators to assist judgment, such as EMA, ATR, etc., which enhances the robustness of the strategy.
#### Risk Analysis
1. The strategy is sensitive to the selection of TSI indicator parameters. Different parameters will bring about great performance differences, so careful selection is required.
2. The conditions for opening and closing positions are relatively simple, lacking trend judgment and volatility constraints, and losses may occur in volatile market conditions.
3. Lack of position management and fund management makes it difficult to control retracements. Continuous losses will lead to significant retracements.
4. If you only do long and short reversals without trend tracking, you will miss many opportunities for trending market conditions.
#### Optimization direction
1. Optimize the parameters of the TSI indicator and find a more robust parameter combination. Methods such as genetic algorithms can be used to automatically search for optimization.
2. Add trend judgment indicators, such as MA or MACD, and choose the trend direction when opening a position to increase the success rate.
3. Add volatility indicators, such as ATR, to reduce the number of transactions in a high-volatility market environment.
4. Introduce a position management model to dynamically adjust the position size of each transaction based on recent market performance and account net value.
5. You can add the logic of trend tracking, continue to hold positions in the trending market, and improve the strategy's ability to capture big market trends.
#### Summary
This strategy takes the TSI indicator as the core and generates trading signals through the intersection of TSI and the signal line. At the same time, trading hours and trading frequency are limited to control risks. The advantage of the strategy is that the logic is simple and clear, and the loss and profit can be stopped in a timely manner. However, the disadvantage is that it lacks trend judgment and position management, is sensitive to TSI parameters, and can only capture reversal trends but miss trend trends. In the future, the strategy can be improved from aspects such as trend and volatility judgment, position management, and parameter optimization.
|| 

#### Overview
This strategy uses the TSI indicator as the main trading signal. When the TSI indicator crosses its signal line, and the TSI indicator is below the lower limit or above the upper limit, the strategy will generate an open position signal. At the same time, the strategy also uses indicators such as EMA and ATR to optimize strategy performance. The strategy only runs within specific trading sessions and sets a minimum trading frequency to control overtrading.

#### Strategy Principle
1. Calculate the TSI indicator value and signal line value.
2. Determine whether the current time is within the allowable trading range, and the current bar is at least the specified minimum number of bars away from the last trade.
3. If the TSI indicator crosses above the signal line from below, and the signal line is below the specified lower limit, a long signal is generated.
4. If the TSI indicator crosses below the signal line from above, and the signal line is above the specified upper limit, a short signal is generated.
5. If currently holding a long position, once the TSI indicator crosses below the signal line from above, close all long positions.
6. If currently holding a short position, once the TSI indicator crosses above the signal line from below, close all short positions.

#### Advantage Analysis
1. The strategy logic is clear, using the cross of the TSI indicator as the only condition for opening and closing positions, which is simple and easy to understand.
2. By limiting the trading session and trading frequency, the risk of overtrading is effectively controlled.
3. Timely stop loss and stop profit, once a opposite signal appears, decisively close the position, controlling the risk exposure of a single transaction.
4. Multiple indicators are used to assist in judgment, such as EMA, ATR, etc., enhancing the robustness of the strategy.

#### Risk Analysis
1. The strategy is quite sensitive to the selection of TSI indicator parameters, and different parameters will bring large performance differences, which need to be chosen carefully.
2. The opening and closing conditions are relatively simple, lacking trend judgment and volatility constraints, and may result in losses in oscillating markets.
3. Lack of position management and fund management, it is difficult to control the drawdown, once a continuous loss will lead to a large drawdown.
4. Only doing long-short reversal, not trend tracking, will miss many trend opportunities.

#### Optimization Direction
1. Optimize the parameters of the TSI indicator to find a more robust parameter combination. Automatic optimization methods such as genetic algorithms can be used.
2. Add trend judgment indicators, such as MA or MACD, to select the trend direction when opening a position to improve the success rate.
3. Add volatility indicators, such as ATR, to reduce the number of trades in high volatility market environments.
4. Introduce a position management model to dynamically adjust the position size of each trade based on recent market performance and account net value.
5. Trend tracking logic can be added to continue holding positions in trend market to improve the strategy's ability to capture big trends.

#### Summary
This strategy is based on the TSI indicator and generates trading signals through the cross of TSI and its signal line. At the same time, it limits the trading time and frequency to control risks. The advantage of the strategy is that the logic is simple and clear, and it stops loss and profit in a timely manner. However, the disadvantage is the lack of trend judgment and position management, sensitivity to TSI parameters, and can only capture reversal market while missing trend market. In the future, the strategy can be improved from aspects such as trend and volatility judgment, position management, and parameter optimization.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-05-30 00:00:00
end: 2024-06-06 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © nikgavalas

//@version=5
strategy("TSI Entries", overlay=true, margin_long=100, margin_short=100)

//
// INPUTS
//

// Define the start and end hours for trading
string sessionInput = input("1000-1530", "Session")

// Day of the week.
string daysInput = input.string("23456", tooltip = "1 = Sunday, 7 = Saturday")

// Minimum number of bar's between entries
requiredBarsBetweenEntries = input.int(12, "Required Bars Between Entries")

// Show debug labels
bool showDebugLabels = input.bool(false, "Show Debug Labels")

//
// FUNCTIONS
//

//@function Define the triple exponential moving average function
tema(src, len) => tema = 3 * ta.ema(src, len) - 3 * ta.ema(ta.ema(src, len), len) + ta.ema(ta.ema(ta.ema(src, len), len), len)

//@function Atr with EMA
atr_ema(length) =>
    trueRange = na(high[1])? high-low : math.max(math.max(high - low, math.abs(high - close[1])), math.abs(low - close[1]))
    //true range can be also calculated with ta.tr(true)
    ta.ema(trueRange, length)

//@function Check if time is in range
timeinrange() => 
    sessionString = sessionInput + ":" + daysInput
    inSession = not na(time(timeframe.period, sessionString, "America/New_York"))

//@function Displays text passed to `txt` when called.
debugLabel(txt, color, y, style) =>
    if (showDebugLabels) 
        label.new(bar_index, y, text = txt, color = color, style = style, textcolor = color.black, size = size.small)


//
// INDICATOR CODE
//

long = input(title="TSI Long Length", defval=8)
short = input(title="TSI Short Length", defval=8)
signal = input(title="TSI Signal Length", defval=3)
lowerLine = input(title="TSI Lower Line", defval=-50)
upperLine = input(title="TSI Upper Line", defval=50)

price = close
double_smooth(src, long, short) =>
	fist_smooth = ta.ema(src, long)
	ta.ema(fist_smooth, short)

pc = ta.change(price)
double_smoothed_pc = double_smooth(pc, long, short)
double_smoothed_abs_pc = double_smooth(math.abs(pc), long, short)
tsiValue = 100 * (double_smoothed_pc / double_smoothed_abs_pc)
signalValue = ta.ema(tsiValue, signal)

//
// COMMON VARIABLES
//

var color trendColor = na
var int lastEntryBar = na

bool tradeAllowed = timeinrange() == true and (na(lastEntryBar) or bar_index - lastEntryBar > requiredBarsBetweenEntries)

// 
// CROSSOVER
//

bool crossOver = ta.crossover(tsiValue, signalValue)
bool crossUnder = ta.crossunder(tsiValue,signalValue)

if (tradeAllowed) 
	if (signalValue < lowerLine and crossOver == true)
		strategy.entry("Up", strategy.long)
		lastEntryBar := bar_index

	else if (signalValue > upperLine and crossUnder == true)

		strategy.entry("Down", strategy.short)
		lastEntryBar := bar_index

// 
// EXITS
// 

if (strategy.position_size > 0 and crossUnder == true)
	strategy.close("Up", qty_percent = 100)

else if (strategy.position_size < 0 and crossOver == true)
	strategy.close("Down", qty_percent = 100)

```

> Detail

https://www.fmz.com/strategy/453665

> Last Modified

2024-06-07 16:36:24
