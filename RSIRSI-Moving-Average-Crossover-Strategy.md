
> Name

RSI Moving Average Crossover Strategy RSI-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1d5d7459f77c30dc8d6.png)

[trans]

## Overview
The RSI moving average crossover strategy is a strategy applied to cryptocurrency trading. This strategy applies a moving average to the RSI indicator and issues buy and sell signals based on the intersection of RSI with its moving average.
## Strategy Principle
The strategy first calculates the RSI indicator. The RSI indicator is based on the rise and fall changes within a certain time period and reflects the strength of the price. When the RSI is greater than 70, it is an overbought zone, and when it is less than 30, it is an oversold zone.
The strategy then applies moving averages based on the RSI indicator. Moving averages can filter out random fluctuations and determine the trend direction. A 10-period RSI moving average is set here.
When the RSI crosses above its moving average, it is considered a buy signal; when the RSI crosses below its moving average, it is considered a sell signal. Trade based on these two signals.
In the code, the RSI indicator of the length period is first calculated. Then calculate the moving average ma of the 10-period RSI. When ma crosses rsi above, buy; when ma crosses rsi below, sell.
In addition, the code also draws line graphs of rsi, ma, and histograms of rsi-ma. The dividing line for rsi=70, rsi=30 is drawn. And when buying or selling, the corresponding signal arrows are marked on the chart.
## Strategic advantage analysis
- The RSI indicator can determine overbought and oversold, the moving average can filter out random fluctuations, and the combination of the two can identify trend transition points.
- RSI moving average crossover is a relatively mature trading strategy idea, which can filter out some false signals.
- The strategy code implementation is simple, clear and easy to understand. The drawing function is complete and trading signals can be clearly observed.
- This strategy is suitable for cryptocurrencies with obvious trends and has better results.
## Strategy risk analysis
- Improper period parameters used for RSI and moving averages may result in too many false signals.
- Simply relying on indicator crossovers cannot completely avoid being trapped. Need to be combined with trend analysis.
- Transaction fees will have a certain impact on profits. Position management needs to be optimized.
- The cryptocurrency market is highly volatile, so you need to be alert to the risk of stop loss.
For risks, you can adjust parameters to optimize indicator effects, shorten positions appropriately, set stop loss lines, and filter signals with trend analysis.
## Strategy optimization direction
- Can study the best combination of RSI and moving average under different period parameters
- You can increase your position when the trend is strong and reduce your position when the trend is unclear.
- You can set dynamic stop loss and follow the trend to stop loss
- You can explore other indicators to combine with RSI to form new trading signals
- You can explore machine learning models based on this strategy to improve the strategy’s winning rate
## Summarize
The RSI moving average crossover strategy combines the advantages of trend indicators and filter indicators and is relatively mature and reliable. The logic of this strategy is simple and easy to understand, and the code implementation is relatively complete. Overall, it is a better cryptocurrency trading strategy. However, any strategy needs to be optimized, and it requires continuous testing and adjustment, supplemented by trend judgment, in order to achieve better strategic results.
||

## Overview

The RSI Moving Average Crossover Strategy is a strategy that is mostly used for cryptocurrency trading. It applies a moving average to the RSI indicator and trades based on the crossovers between the RSI and its moving average. It also includes the indicator that it is made from.

## Strategy Logic

The strategy first calculates the RSI indicator. The RSI indicator reflects the strength of price based on the upward and downward movements over a certain period of time. RSI above 70 is considered overbought, and below 30 oversold.

Then, the strategy applies a moving average to the RSI indicator. The moving average can filter out random fluctuations and determine the trend direction. Here a 10-period RSI moving average is set. 

When the RSI crosses above its moving average, it is considered a buy signal. When the RSI crosses below its moving average, it is considered a sell signal. Trading is conducted according to these two signals.

In the code, the RSI indicator with length period is calculated first. Then the 10-period moving average ma of RSI is calculated. When ma crosses above rsi, it will buy. When ma crosses below rsi, it will sell.

In addition, the code plots the line chart for rsi and ma, as well as the column chart for rsi-ma. The dividing lines for rsi=70 and rsi=30 are also plotted. The corresponding signal arrows are marked on the chart when buying or selling.

## Advantage Analysis

- RSI can judge overbought and oversold conditions. Moving average can filter out random fluctuations. The combination of the two can identify trend reversal points.

- RSI moving average crossover is a relatively mature trading strategy idea that can filter out some false signals.

- The strategy code is simple and clear, easy to understand. The plotting function is complete for clearly observing trading signals.

- This strategy works well for cryptocurrencies with relatively obvious trends.

## Risk Analysis

- Improper RSI and moving average period parameters may generate too many wrong signals.

- Relying solely on indicator crossovers cannot completely avoid being trapped. Trend analysis needs to be combined.

- Trading costs can have some impact on profits. Position sizing needs to be optimized. 

- High volatility of crypto market. Need to be alert to stop loss risks.

To address the risks, parameters can be adjusted to optimize the indicators, position sizes can be reduced, stop loss can be set, and trend analysis can be used to filter signals.

## Optimization Directions

- Research the optimal combination of RSI and moving average under different period parameters.

- Increase position size when the trend is strong, and reduce when trend is unclear.

- Set dynamic stop loss to trail the trend.

- Explore combining RSI with other indicators to form new trading signals.

- Explore machine learning models based on this strategy to improve win rate.

## Summary

The RSI moving average crossover strategy combines the advantages of trend and filtering indicators, relatively mature and reliable. The strategy logic is simple and clear, and the code implementation is also quite complete. Overall it is a pretty good cryptocurrency trading strategy. But every strategy needs optimization. It requires constant testing and adjustment, combined with trend analysis, in order to achieve better strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2019|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2022|Backtest Stop Year|
|v_input_5|true|Backtest Stop Month|
|v_input_6|true|Backtest Stop Day|
|v_input_7|true|Color Background?|
|v_input_8|27|Length|
|v_input_9|10|RSI MA Window|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-31 00:00:00
end: 2023-11-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("RSI w MA Strategy", shorttitle="RSI w MA Strategy", overlay=false, initial_capital=10000, currency='USD',process_orders_on_close=true)

//TIME FRAME AND BACKGROUND CONTROL/////////////////////////////////////////////
testStartYear = input(2019, "Backtest Start Year")
testStartMonth = input(01, "Backtest Start Month")
testStartDay = input(01, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear, testStartMonth, testStartDay, 0, 0)
testStopYear = input(2022, "Backtest Stop Year")
testStopMonth = input(1, "Backtest Stop Month")
testStopDay = input(1, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear, testStopMonth, testStopDay, 0, 0)
testPeriodBackground = input(title="Color Background?", type=input.bool, defval=true)
testPeriodBackgroundColor = testPeriodBackground and time >= testPeriodStart and time <= testPeriodStop ? 
   color.teal : na
//bgcolor(testPeriodBackgroundColor, transp=50)
testPeriod() => true
////////////////////////////////////////////////////////////////////////////////

src = close, len = input(27, minval=1, title="Length")
up = rma(max(change(src), 0), len)
down = rma(-min(change(src), 0), len)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
window = input(10, "RSI MA Window")
ma = sma(rsi,window)
plot(rsi, color=color.orange)
colorr= ma > rsi ? color.red : color.green
plot(ma,color=colorr)
band1 = hline(70)
band0 = hline(30)
fill(band1, band0, color=color.purple, transp=90)
diff = rsi - ma

plot(diff,style= plot.style_columns,transp=50,color = colorr)

plotshape(crossunder(rsi,ma)?rsi:na,title="top",style=shape.triangledown,location=location.absolute,size=size.tiny,color=color.red,transp=0)
plotshape(crossover(rsi,ma)?rsi:na,title="bottom",style=shape.triangleup,location=location.absolute,size=size.tiny,color=color.lime,transp=0)

buySignal = crossover(rsi,ma)
sellSignal = crossunder(rsi,ma)

//TRADE CONTROL/////////////////////////////////////////////////////////////////
if testPeriod()
    if buySignal
        strategy.close("Short", qty_percent = 100, comment = "Close Short")
        strategy.entry("Long", strategy.long, qty=.1)

    if sellSignal
        strategy.close("Long", qty_percent = 100, comment = "Close Long")
        strategy.entry("Short", strategy.short, qty=.1)

////////////////////////////////////////////////////////////////////////////////












```

> Detail

https://www.fmz.com/strategy/431398

> Last Modified

2023-11-07 15:35:58
