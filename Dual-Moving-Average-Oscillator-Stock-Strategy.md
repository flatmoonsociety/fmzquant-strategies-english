
> Name

Dual-Moving-Average-Oscillator-Stock-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d394aa96c57518e417.png)
[trans]
### Overview
This strategy uses the Double Smoothed Moving Average Oscillator indicator to determine buy and sell points for stocks. The Double Smoothed Average Oscillator Index consists of double exponential moving averages with two different parameters, long and short, and measures overbought and oversold phenomena by calculating the momentum of price changes.
### Strategy Principles
The core indicator of this strategy is the Double Smoothed Moving Average Oscillator Index (TSI). The index is calculated as:
1. Calculate price changes pc=close-preclose
2. Perform double exponential smoothing on pc, taking the long-period 12-day and short-period 9-day exponential averages respectively. Get double smoothed price change:double_smoothed_pc
3. Also perform double exponential smoothing on the absolute value |pc| to obtain double_smoothed_abs_pc
4. Final TSI index=100*(double_smoothed_pc/double_smoothed_abs_pc)
By calculating the relationship between the TSI value and its signal line tsi_signal, we can determine the overbought and oversold area and decide whether to buy or sell.
Buy signal: The TSI value crosses its signal line, indicating that the stock price has reversed and entered the oversold area, and you can buy.
Sell ​​signal: The TSI value falls below its signal line, indicating that the stock price has reversed, the oversold area has ended, and it should be sold.
### Advantage Analysis
The biggest advantage of this strategy is that it uses the double-smoothed moving average indicator to identify cyclical characteristics in stock prices. The use of both long and short periods in the double smoothed moving average indicator can more sensitively and accurately capture the price change trend, and has a stronger advantage than a single moving average when judging buying and selling points.
In addition, this strategy uses the TSI index instead of other common technical indicators because the TSI index pays more attention to calculating the momentum information of price changes. This can more accurately determine overbought and oversold phenomena, thereby achieving better selection of buying and selling nodes.
### Risk Analysis
The biggest risk of this strategy is that the double smoothed moving average itself is highly sensitive to price changes. When the stock price fluctuates, it is easy to generate false signals. In addition, the TSI index's criteria for determining overbought and oversold areas are still relatively subjective, and improper parameter settings will also affect the accuracy of the judgment.
In order to control these risks, it is recommended to appropriately optimize parameters and adjust the length of long and short moving averages; at the same time, combine other indicators to verify signals and avoid opening positions in volatile markets. In addition, it is also necessary to optimize stop loss strategies and set up risk control measures for emergencies.
### Optimization direction
The optimization direction of this strategy mainly focuses on two aspects:
1. Parameter optimization. More backtests can be used to test the optimal combination of long and short moving average and signal line parameters to improve the sensitivity of the indicator.
2. Configure filtering indicators. For example, combine Bollinger Bands, KDJ and other indicators to verify buying and selling signals to avoid incorrect opening of positions. Or set up a trading volume filter to only open a position when the trading volume increases.
3. Add a stop loss strategy. Set up trailing stop loss and time stop loss to control single losses. At the same time, transactions can also be suspended based on market conditions to control systemic risks.
4. Optimize warehouse management. Establish dynamically adjusted position sizes and proportions to control the risk exposure of each transaction according to market conditions.
### Summarize
This strategy uses the calculation method of the double-smoothed moving average oscillator index and combines the long and short periods to analyze price momentum changes to determine the overbought and oversold areas and determine the timing of buying and selling. Compared with a single moving average, it has the advantage of more accurate and sensitive judgment. Of course, parameters still need to be properly optimized and supplemented by other indicators to filter signals, thereby improving the stability and profitability of the strategy. In general, this strategy provides a technical means to effectively judge buying and selling points, and is worthy of real-time verification and optimization.
||

### Overview

This strategy uses the Dual Moving Average Oscillator index to determine the buy and sell points of stocks. The Dual Moving Average Oscillator index consists of two exponential moving averages with different parameters, and measures the momentum of price changes to detect overbought and oversold conditions.

### Strategy Principle  

The core indicator of this strategy is the True Strength Index (TSI). The calculation method is:

1. Calculate the price change pc=close-preclose

2. Smooth pc twice using both long period of 12 days and short period of 9 days exponential moving average. Obtain double smoothed price change: double_smoothed_pc

3. Similarly, double smooth the absolute value |pc| to get double_smoothed_abs_pc

4. Finally TSI index = 100*(double_smoothed_pc/double_smoothed_abs_pc)

By comparing the TSI value with its signal line tsi_signal, we can determine overbought or oversold zones, thereby deciding buy and sell points.  

Buy signal: TSI crosses over its signal upward, indicating reversal of the stock price, marking the start of overbought zone where we should long.

Sell signal: TSI crosses below its signal downward, indicating reversal of the stock price, marking the end of overbought zone where we should sell out.

### Advantage Analysis   

The biggest advantage of this strategy lies in using the dual moving average indicator to identify cyclical features in stock prices. By simultaneously employing both long and short periods in the dual moving average, it can capture price change trends more sensitively and accurately than a single moving average, and is more effective in determining trading signals.

In addition, this strategy chooses the TSI index rather than other common technical indicators, because TSI pays more attention to calculating price change momentum, which can judge overbought/oversold conditions more precisely, resulting in better trading points. 

### Risk Analysis

The biggest risk of this strategy is that the dual moving average itself is quite sensitive to price changes. In case of price fluctuation, it can easily generate false signals. Moreover, the criteria for TSI to judge overbought/oversold zones are still subjective, and improper parameter settings also impact the accuracy.

To control such risks, it is advisable to optimize parameters appropriately by adjusting lengths of the double moving averages. Combining other indicators to verify signals is also necessary to avoid opening positions amid volatility. Furthermore, optimizing stop-loss strategies and setting up risk control measures against emergencies are quite essential.

### Optimization Directions   

The optimization directions of this strategy mainly focus on two aspects:

1. Parameter optimization. The optimal combination of parameters like lengths of long and short moving average and signal line can be backtested to improve the sensitivity.  

2. Configure filtering indicators. Such as combining Bollinger Bands, KDJ and so on to verify buy/sell signals and prevent wrong opening of positions. Trading volume filter can also be applied to open positions only when volume surges.

3. Add stop-loss strategy. Set up moving stop loss, timed exit to limit the loss of single position. Also we can suspend trading temporarily based on market condition to control systematic risk.

4. Optimize position sizing. Set up dynamic size and proportion of positions based on market condition to manage the risk exposure of every trade.

### Summary  

This strategy utilizes the calculation method of Dual Moving Average Oscillator index, integrating both long and short term analysis of price momentum changes, thereby determining overbought and oversold zones to decide entries and exits. Compared to a single moving average, it has the advantage of more accurate and sensitive judgement. Of course, proper parameter optimization is still necessary, coupled with other indicators for signal filtering, so as to enhance the stability and profitability. Overall, this strategy provides an effective technical tool to determine trading points, which is worth live testing and optimizing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10000|Initial Capital|
|v_input_2|true|Risk Percentage|
|v_input_3|12|Long Length|
|v_input_4|9|Short Length|
|v_input_5|12|Signal Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-29 00:00:00
end: 2024-02-04 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © shankardey7310

//@version=5
strategy("TSI STOCKS", shorttitle="TSI", overlay=true)

initialCapital = input(10000, title="Initial Capital")
riskPercent = input(1, title="Risk Percentage") / 100

longLength = input(12, title="Long Length")
shortLength = input(9, title="Short Length")
signalLength = input(12, title="Signal Length")

price = close
pc = ta.change(price)

double_smooth(src, long, short) =>
    first_smooth = ta.ema(src, long)
    ta.ema(first_smooth, short)

double_smoothed_pc = double_smooth(pc, longLength, shortLength)
double_smoothed_abs_pc = double_smooth(math.abs(pc), longLength, shortLength)
tsi_value = 100 * (double_smoothed_pc / double_smoothed_abs_pc)
tsi_signal = ta.ema(tsi_value, signalLength)

riskAmount = (initialCapital * riskPercent) / close

if (tsi_value > tsi_signal and tsi_value[1] <= tsi_signal[1])
    strategy.entry("Long", strategy.long)

if (tsi_value < tsi_signal and tsi_value[1] >= tsi_signal[1])
    strategy.close("Long")

plot(tsi_value, title="True Strength Index", color=#2962FF)
plot(tsi_signal, title="Signal", color=#E91E63)
hline(0, title="Zero", color=#787B86)
```

> Detail

https://www.fmz.com/strategy/441052

> Last Modified

2024-02-05 10:47:38
