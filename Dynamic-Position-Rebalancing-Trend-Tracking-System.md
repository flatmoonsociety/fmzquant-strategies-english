
> Name

Dynamic-Position-Rebalancing-Trend-Tracking-System
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/785514f6062fef0c5a794e3d098c9c2a1cbe5aaa327fac48430e2e6fdbfb189c.png)

[trans]

### Overview
This strategy combines two popular system trading strategies, the exponential moving average crossover system and the turtle trading system. This system is specially designed for the daily time frame, and has strong tracking capabilities by dynamically adjusting positions and tracking market trends in real time.
### Strategy Principles
This strategy contains two sub-strategies: trend strategy and breakout strategy.
Trend strategies use the crossover of fast EMA and slow EMA as trading signals. The fast EMA cycle length is set by the user, and the slow EMA cycle length is 5 times the fast EMA. The signal is obtained by dividing the difference between fast and slow EMA by the standard deviation of the 252-period return rate, and is adjusted for volatility to produce a more reliable trading signal. When a new trend is detected, go long or short.
Breakout strategies use the average of the highest and lowest prices in a fixed period as a baseline. When the price rises or falls by more than a certain amount relative to the baseline, a long or short signal is generated.
Position adjustments are calculated based on recent price volatility and the annualized risk target set by the user. When volatility is low, the position is larger, and when volatility is high, the position is smaller, achieving risk-adjusted dynamic position management.
Stop loss is set based on multiples of the true volatility. Trailing stops are based on the moving zurück closing of the highest and lowest price.
### Advantage Analysis
This strategy has the following advantages:
1. Combining the two sub-strategies of trend tracking and breakthrough, it can perform adaptive switching in different market environments and has strong robustness.
2. Apply advanced position management and risk control technology to dynamically adjust positions and effectively control risks.
3. By adjusting positions using true volatility and annualized risk targets, a relatively stable portfolio risk level can be obtained in high and low volatility markets.
4. Setting the stop loss position based on the actual price fluctuation can effectively avoid unnecessary small losses caused by stop loss and exit.
5. Adjust the tracking stop position in real time, you can flexibly follow the trend to make profits, and stop the loss in time to leave the market.
### Risk Analysis
The main risks of this strategy are:
1. Depends on parameter optimization. Different parameters have a greater impact on strategy performance, and comprehensive testing is required to obtain the best parameters.
2. Trailing stop loss may be stopped too frequently in a volatile trend. The stop loss range can be appropriately relaxed and the stop loss mechanism can be optimized.
3. Position management and risk control technology are sensitive to initial capital and transaction costs. Initial funds that are too small and transaction costs that are too high will affect strategy profitability.
4. The strategy’s setting of annualized risk targets and maximum leverage relies on correctly assessing the volatility of the underlying. Inaccurate volatility assessments can result in positions that are too large or too small.
### Optimization direction
The main optimization directions of this strategy include:
1. Find the optimal parameter combination. The optimal parameter settings can be found through backtesting of more historical data.
2. Improve the stop loss mechanism. You can test trailing stop loss, time stop loss, shock stop loss and other stop loss forms to optimize the stop loss strategy.
3. Optimize position and risk management. Different risk targets can be tested to find the best risk-return combination. It is also possible to test the impact of different leverage levels.
4. Try other auxiliary indicators. More technical indicators can be added to improve the accuracy of signals and the robustness of strategies.
5. Test different holding periods. You can try to use higher cycles to assist decision-making to improve the accuracy of position allocation.
### Summary
This strategy integrates two major categories of trading strategies, trend tracking and trend breakthrough, and uses advanced dynamic position management technology to achieve risk-adjusted position configuration. It can effectively control risks while tracking market trends. It has strong profitability and is worthy of further testing and optimization.
||

### Overview

This strategy integrates the exponential moving average crossover system and turtle trading system, two popular systematic trading strategies. It is specially designed for the daily timeframe to track market trends in real-time by dynamically managing positions.  

### Strategy Logic  

The strategy contains two sub-strategies: trend strategy and breakout strategy.  

The trend strategy uses fast EMA and slow EMA crossovers as trading signals. The fast EMA period is user-defined and the slow EMA period is 5 times of the fast EMA. The signal is generated by dividing the EMA difference by the 252-period return standard deviation, which is volatility-adjusted to produce more reliable signals. It goes long or short when detecting new trend formations.

The breakout strategy uses the average of highest high and lowest low prices over a fixed lookback period as the baseline. Long/short signals are generated when the price breaks out above/below the baseline by a certain percentage.

Position sizing is based on recent price volatility and user-defined annual risk target. Larger size is taken when volatility is low while smaller size is taken when volatility is high. This realizes dynamic position management with risk adjustment.  

Hard stops are set as multiples of the average true range. Trailing stops trail recent highest high or lowest low prices.

### Advantage Analysis 

The main advantages of this strategy include:  

1. Combining trend tracking and breakout sub-strategies adapts to different market environments with strong robustness.  

2. Applying advanced position sizing and risk management techniques dynamically manages position and effectively controls risk.

3. Volatility-adjusting positions based on recent volatility and annual risk target maintains relatively stable portfolio risk across high/low volatility regimes.  

4. Setting stop loss based on actual price fluctuation avoids unnecessary small losses from stop runs.  

5. Adjusting trailing stop in real-time flexibly follows trends to book profits and stops out timely.

### Risk Analysis

The main risks of this strategy are:  

1. Reliance on parameter optimization. Different parameters considerably impact strategy performance so comprehensive testing is needed to find optimum parameters.  

2. Frequent stop outs in choppy trends. Stop loss width could be relaxed and stop mechanisms optimized.

3. Sensitivity to initial capital and trading costs. Insufficient initial capital and high trading costs negatively impact profitability.  

4. Reliance on accurate volatility estimates for position sizing and risk controls. Inaccurate volatility estimates lead to oversized or undersized positions.

### Optimization Directions 

The main optimization directions include:

1. Search for optimal parameter sets via more backtesting with larger historical dataset.  

2. Improve stop mechanisms by testing various stops like moving stops, time stops, volatility stops etc.  

3. Optimize position sizing and risk management by testing different risk targets to find best risk-return profile. Also test impacts of different leverage levels.  

4. Try more auxiliary indicators to improve signal accuracy and strategy robustness.

5. Test different holding periods by assisting decisions with higher timeframe signals to improve position allocation accuracy.  

### Conclusion
This strategy integrates two major categories of trading strategies: trend following and breakouts. By applying advanced dynamic position adjustment techniques, it effectively controls risk while tracking market moves to profit. It demonstrates strong profit potential and is worth further testing and optimization.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|(?Strategy Settings)Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|10|Lookback period for fast EMA|
|v_input_int_2|20|Lookback period for Breakout|
|v_input_2|true|(?Strategy toggle)Long|
|v_input_3|true|Short|
|v_input_4|false|Trend|
|v_input_5|true|Breakout|
|v_input_float_1|2|(?Risk Management Settings)Stop multiple|
|v_input_int_3|10|Trail lookback|
|v_input_float_2|true|Max Leverage|
|v_input_float_3|15|Annualised Volatility Target %|
|v_input_6|true|Compounding|
|v_input_float_4|50|%|
|v_input_int_4|true|(?Backtest range)From Day|
|v_input_int_5|true|From Mon|
|v_input_int_6|2018|From Yr|
|v_input_int_7|true|To Day|
|v_input_int_8|true|To Mon|
|v_input_int_9|9999|To Yr|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Crunchster1

//@version=5
strategy(title="Crunchster's Turtle and Trend System", shorttitle="Turtle Trend", overlay=true, slippage=10, pyramiding=1, precision = 4, calc_on_order_fills = false, calc_on_every_tick = false, default_qty_value = 0.1, initial_capital = 1000, commission_value = 0.06, process_orders_on_close = true)

// Inputs and Parameters
src = input(close, 'Source', group='Strategy Settings')
length = input.int(title="Lookback period for fast EMA", defval=10, minval=2, group='Strategy Settings', tooltip='This sets the lookback period for the fast exponential moving average. The slow EMA is 5x the fast EMA length')
blength = input.int(title="Lookback period for Breakout", defval=20, minval=5, step=5, group='Strategy Settings')

long = input(true, 'Long', inline='08', group='Strategy toggle')
short = input(true, 'Short', inline='08', group='Strategy toggle', tooltip='Toggle long/short strategy on/off')

EMAwt = input(false, 'Trend', inline='01', group='Strategy toggle')
breakwt = input(true, 'Breakout', inline='01', group='Strategy toggle', tooltip='Toggle trend/breakout strategy on/off')

stopMultiple = input.float(2, 'Stop multiple', step=0.5, group='Risk Management Settings', tooltip='Multiple for ATR, setting hard stop loss from entry price')
trail = input.int(10, 'Trail lookback', step=5, group='Risk Management Settings', tooltip='Lookback period for the trailing stop')
lev = input.float(1, 'Max Leverage', step=0.5, group='Risk Management Settings', tooltip='Max leverage sets maximum allowable leverage of total capital (initial capital + any net profit), capping maximum volatility adjusted position size')
riskT = input.float(15, maxval=75, title='Annualised Volatility Target %', group='Risk Management Settings', tooltip='Specify annual risk target, used to determine volatility adjusted position size. Annualised daily volatility is referenced to this value and position size adjusted accordingly')
comp = input(true, 'Compounding', inline='09', group='Risk Management Settings')
Comppct = input.float(50, '%', step=5, inline='09', group='Risk Management Settings', tooltip='Toggle compounding of profit, and set % of profit to compound')

// Backtesting period
FromDay = input.int(defval=1, title='From Day', minval=1, maxval=31, inline='04', group='Backtest range')
FromMonth = input.int(defval=1, title='From Mon', minval=1, maxval=12, inline='04', group='Backtest range')
FromYear = input.int(defval=2018, title='From Yr', minval=1900, inline='04', group='Backtest range', tooltip='Set start of backtesting period')
ToDay = input.int(defval=1, title='To Day', minval=1, maxval=31, inline='05', group='Backtest range')
ToMonth = input.int(defval=1, title='To Mon', minval=1, maxval=12, inline='05', group='Backtest range')
ToYear = input.int(defval=9999, title='To Yr', minval=1900, inline='05', group='Backtest range', tooltip='Set end of backtesting period')

start = timestamp(FromYear, FromMonth, FromDay, 00, 00)
finish = timestamp(ToYear, ToMonth, ToDay, 23, 59)
window = time >= start and time <= finish

// Breakout strategy
lower = ta.lowest(low[1], blength)
upper = ta.highest(high[1], blength)
basis = math.avg(upper, lower)
signal = 20*(close - basis) / (upper - lower)

// Trend strategy
fEMA = ta.ema(close[1], length)
sEMA = ta.ema(close[1], length*5)
emadiff = fEMA - sEMA
nemadiff = 5*emadiff/(ta.stdev(close - close[1], 252))

//Risk Management formulae
strategy.initial_capital = 50000
tr = math.max(high - low, math.abs(high - close), math.abs(low - close)) //True range
stopL = ta.sma(tr, 14) //Average true range
stdev = ta.stdev(close-close[1], 14) //volatility of recent returns
maxcapital = strategy.initial_capital+strategy.netprofit //Maximum capital available to invest - initial capital net of profit
annvol = 100*math.sqrt(365)*stdev/close //converts recent volatility of returns into annualised volatility of returns - assumes daily timeframe

risk = 1.1
if comp
    risk := (strategy.initial_capital+(Comppct*strategy.netprofit/100))//adjust investment capital to include compounding
else
    risk := strategy.initial_capital

shares = (risk * (riskT/annvol)) / close //calculates volatility adjusted position size, dependent on user specified annualised risk target
if ((shares*close) > lev*maxcapital) //ensures position size does not exceed available capital multiplied by user specified maximum leverage
    shares := lev*maxcapital/close

//To set the price at the entry point of trade
Posopen() =>
    math.abs(strategy.position_size[1]) <= 0 and math.abs(strategy.position_size) > 0

var float openN = na
if Posopen()
    openN := stopL

// Trailing stop
tlower = ta.lowest(low[1], trail)
tupper = ta.highest(high[1], trail)
tbasis = math.avg(tupper, tlower)
tsignal = 20*(close - tbasis) / (tupper - tlower)

// Strategy Rules
if EMAwt
    if long
        longCondition2 = (nemadiff >2 and nemadiff[1] <2) and window
        exitlong = tsignal <= -10
        if (longCondition2)
            strategy.entry('Trend Long!', strategy.long, qty=shares)
        if strategy.position_size > 0    
            strategy.exit('Stop Long', from_entry = 'Trend Long!', stop=(strategy.opentrades.entry_price(0) - (openN * stopMultiple)))
        if (exitlong)
            strategy.close('Trend Long!', immediately = true)

    if short
        shortCondition2 = (nemadiff <-1 and nemadiff[1] >-1) and window
        exitshort = tsignal >= 10
        if (shortCondition2)
            strategy.entry('Trend Short!', strategy.short, qty=shares)
        if strategy.position_size < 0   
            strategy.exit('Stop Short', from_entry = 'Trend Short!', stop=(strategy.opentrades.entry_price(0) + (openN * stopMultiple)))
        if (exitshort)
            strategy.close('Trend Short!', immediately = true)

if breakwt
    if long
        longCondition1 = (signal >= 10) and window
        exitlong = tsignal <= -10
        if (longCondition1)
            strategy.entry('Break Long!', strategy.long, qty=shares)
        if strategy.position_size > 0    
            strategy.exit('Stop Long', from_entry = 'Break Long!', stop=(strategy.opentrades.entry_price(0) - (openN * stopMultiple)))
        if (exitlong)
            strategy.close('Break Long!', immediately = true)

    if short
        shortCondition1 = (signal <= -10) and window
        exitshort = tsignal >= 10
        if (shortCondition1)
            strategy.entry('Break Short!', strategy.short, qty=shares)
        if strategy.position_size < 0   
            strategy.exit('Stop Short', from_entry = 'Break Short!', stop=(strategy.opentrades.entry_price(0) + (openN * stopMultiple)))
        if (exitshort)
            strategy.close('Break Short!', immediately = true)

// Visuals of trend and direction
plot(nemadiff, title='EMA Forecast', color=color.black, display=display.none)
plot(ta.sma(ta.median(math.sqrt(math.pow(nemadiff,2)), 700), 350), 'Forecast mean', color=color.rgb(245, 0, 0), display=display.none)

MAColor = fEMA > sEMA ? #00ff00 : #ff0000
MA1 = plot(fEMA, title='Fast EMA', color=MAColor)
MA2 = plot(sEMA, title='Slow EMA', color=MAColor)
fill(MA1, MA2, title='Band Filler', color=MAColor)
```

> Detail

https://www.fmz.com/strategy/440077

> Last Modified

2024-01-26 14:41:08
