
> Name

Seasonal-Range-Moving-Average-RSI-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/7d3e207a19c32f7517.png)

[trans]

## Overview
This strategy combines two technical indicators, the moving average and the relative strength index (RSI), to capture seasonal cyclical characteristics and generate trading signals. The advantage of this strategy is that it can very clearly identify seasonal trends, but it also carries the risk of being misled by false signals. By adjusting parameter settings, further optimization can be achieved and the strategy effect can be improved.
## Strategy Principle
This strategy first calculates the moving average of a certain period n to capture the medium and long-term trend direction of the price. Then calculate the RSI indicator of this moving average to determine whether it is currently overbought or oversold. RSI determines the current market sentiment by calculating the ratio of increases and decreases within a certain period.
When the RSI crosses the lower rail, a buy signal is generated, indicating that it is currently oversold and can be bought. When the RSI goes below the upper rail, a sell signal is generated, indicating that it is currently overbought and can be sold. In addition, the strategy also sets a range of months and days, trading only between specified months and days to capture seasonal characteristics.
## Strategic Advantages
- Use the moving average to determine the general trend, RSI to determine overbought and oversold phenomena, and combine dual indicators to improve the accuracy of judgment.
- Set the month and date range to effectively identify seasonal market characteristics and capture such trading opportunities
- RSI parameter setting is flexible and can adjust the sensitivity of judging overbought and oversold.
- You can customize the moving average parameters and adjust the sensitivity to the general trend judgment.
## Strategic Risks and Solutions
- There is a risk of being misled by false signals. For example, trend reversals caused by non-seasonal emergencies may lead to inappropriate trading signals. The solution is to adjust the month date range to avoid possible event risks.
- When the trend turns, there may be a divergence between the moving average and the RSI indicator, resulting in inconsistent trading signals. The solution is to appropriately adjust the moving average parameters and shorten the period to capture the trend turning point faster.
- The preset month date range may deviate from the actual seasonal market timing. The solution is to determine more accurate seasonal range parameters based on testing with historical data.
- There may be false breakthroughs in trading signals. The solution is to set a wider range to avoid being misled by small fluctuations.
## Strategy optimization direction
- Other auxiliary indicators can be introduced, such as the Oscillatory Stock Index (STOCH), etc., to set more stringent filtering conditions and reduce false signals.
- You can test more different parameter combinations and find optimal parameters to improve the strategy effect. For example, adjust the moving average period, the upper and lower rail parameters of RSI, etc.
- The step optimization method can be used to automatically search the parameter space and find the optimal parameter combination.
- You can collect more historical data and use machine learning methods to train and optimize policy rules.
- You can consider adding a stop-loss and stop-profit strategy to optimize fund management.
## Summarize
This strategy comprehensively uses moving averages and RSI indicators, and adds seasonal factor judgment to form a relatively complete trend and overbought and oversold identification system. The advantage of the strategy is that it can clearly identify seasonal trends and seize such trading opportunities. There is a certain risk of being misled, but it can be optimized through parameter adjustment, introduction of auxiliary indicators, machine learning and other methods to improve the strategy effect to a higher level. Overall, this strategy provides a reliable and effective seasonal trading framework, which is worthy of real-time testing and application.
||

## Overview

This strategy combines moving average and relative strength index (RSI), two technical indicators, to capture seasonal cyclical characteristics and generate trading signals. The advantage of this strategy is that it can identify seasonal trends very clearly, but it also has the risk of being misled by wrong signals. Further optimizations can be made by adjusting parameter settings to improve strategy performance.

## Strategy Logic

The strategy first calculates the moving average of a certain period n to capture the medium-to-long term trend direction. Then it calculates the RSI indicator of the moving average to judge whether it is currently in an overbought or oversold state. RSI measures market sentiment by calculating the ratio of gains versus losses over a certain period.

When RSI crosses above the lower band, a buy signal is generated, indicating an oversold status, and a long position can be opened. When RSI crosses below the upper band, a sell signal is generated, indicating an overbought status, and a short position can be opened. In addition, the strategy also sets the range for month and date to trade only during specific months and days, in order to capture seasonal patterns.

## Advantages of the Strategy

- Utilize moving average to determine the major trend, and RSI to judge overbought/oversold scenarios, combining dual indicators to improve accuracy

- Setting monthly and date range can effectively identify seasonal trends and capture such trading opportunities 

- Flexible RSI parameter settings to adjust sensitivity in determining overbought/oversold levels

- Customizable moving average parameters to adapt sensitivity in judging major trends

## Risks and Solutions

- Risk of being misled by wrong signals, e.g. trend reversals triggered by non-seasonal events, may generate improper trading signals. Solution is to adjust monthly and date range to avoid potential event risks.

- Divergence may appear between moving average and RSI when trend is reversing. Solution is to properly shorten moving average period to capture trend turns faster.  

- Preset monthly and date range may deviate from actual seasonal trends. Solution is to determine a more precise seasonal range based on historical data testing.

- Trading signals may encounter false breakouts. Solution is to set wider range to avoid being misled by minor fluctuations. 

## Optimization Directions

- Introduce other auxiliary indicators, e.g. Stochastic Oscillator, to set more stringent filtering conditions and reduce wrong signals.

- Test more different parameter combinations to find optimum parameters and improve strategy performance, e.g. adjust moving average period, RSI bands etc.

- Utilize parameter optimization methods to automatically search parameter space for optimal parameter sets.

- Collect more historical data and utilize machine learning to train and optimize strategy rules.

- Consider adding stop loss/take profit strategies to optimize money management.

## Summary

This strategy combines moving average and RSI, with the addition of seasonal judgments, to form a relatively complete system for trend and overbought/oversold identification. The advantage lies in its ability to clearly recognize seasonal patterns and capitalize on such trading opportunities. There are certain risks of being misled, but optimizations can be made via parameter tuning, introducing auxiliary indicators, machine learning etc. to elevate strategy performance. Overall, this strategy provides a reliable and effective seasonal trading framework that is worth live testing and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|15|Length of MA|
|v_input_2|14|Length|
|v_input_3|70|Upper Band for RSI|
|v_input_4|30|Lower Band for RSI|
|v_input_5|true|monthfrom|
|v_input_6|12|monthuntil|
|v_input_7|true|dayfrom|
|v_input_8|31|dayuntil|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-26 00:00:00
end: 2023-10-26 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title = " RSI of MA Strategy ",shorttitle="MARSI Strategy",default_qty_type = strategy.percent_of_equity, default_qty_value = 100,commission_type=strategy.commission.percent,commission_value=0.1,initial_capital=1)



lengthofma = input(15,minval=1,title="Length of MA")
len = input(14, minval=1, title="Length")
upperband = input(70,minval=1,title='Upper Band for RSI')
lowerband = input(30,minval=1,title="Lower Band for RSI")

src=sma(close,lengthofma)
up = rma(max(change(src), 0), len)
down = rma(-min(change(src), 0), len)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
plot(rsi, color=purple)

band1 = hline(upperband)
band0 = hline(lowerband)
fill(band1, band0, color=purple, transp=90)



longCond =  crossover(rsi,lowerband)

shortCond =  crossunder(rsi,upperband)




monthfrom =input(1)
monthuntil =input(12)
dayfrom=input(1)
dayuntil=input(31)

if (  longCond ) 
    strategy.entry("LONG", strategy.long, stop=close, oca_name="TREND",  comment="LONG")
    
else
    strategy.cancel(id="LONG")
    



if ( shortCond ) 

    strategy.entry("SHORT", strategy.short,stop=close, oca_name="TREND",  comment="SHORT")
else
    strategy.cancel(id="SHORT")




```

> Detail

https://www.fmz.com/strategy/430365

> Last Modified

2023-10-27 16:04:21
