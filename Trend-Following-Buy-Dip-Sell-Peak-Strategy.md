
> Name

Trend-Following-Buy-Dip-Sell-Peak-Strategy Trend-Following-Buy-Dip-Sell-Peak-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/71105fac2b12533c39.png)

[trans]

### Overview
This strategy calculates the upper and lower rails of Bollinger Bands and combines the direction of the long and short-term moving averages to achieve an automated trading strategy of buying lows and selling highs in the direction of the trend. The idea is to track the long-term trend direction of the stock, buy at low points to establish a long position during short-term adjustments, and sell at overbought highs to realize profits.
### Strategy Principles
This strategy mainly implements automatic trading through the following parts:
1. Calculate the upper and lower rails of the Bollinger Bands: By calculating the n-period standard deviation of close, the upper and lower rails of the Bollinger Bands channel are obtained.
2. Long-term and short-term trend judgment: Calculate the long-term 300-period and short-term 20-period SMA to determine the overall stock trend and the current stage trend.
3. Buy signal: When close breaks through the lower track of the Bollinger Bands, the long-term SMA is above and the short-term SMA begins to rise, it is considered to be the low point of the range and a buy signal is generated.
4. Sell signal: When close breaks through the upper Bollinger Band, the long-term SMA is below and the short-term SMA begins to fall, it is considered to be the high point of the range and a sell signal is generated.
5. Use the OCO order group to ensure stop loss and take profit.
Through such a design, it is possible to automatically identify short-term adjustment buying opportunities and overbought high selling opportunities in line with the general trend, and implement trend trading strategies.
### Advantage Analysis
This strategy has the following advantages:
1. Automatically identify trends without manual judgment, reducing the difficulty of operation.
2. Systematically capture the buying opportunities of short-term adjustments to avoid missing the lows.
3. Systematically identify selling opportunities at overbought highs and cash out profits in a timely manner.
4. Setting stop-loss and take-profit points at the same time can effectively control risks.
5. It can filter out most invalid trading signals and improve the winning rate.
6. Ability to track trends and adjust positions in a timely manner.
7. The strategic ideas are clear and easy to understand, and easy to carry out subsequent optimization.
### Risk Analysis
There are also some risks to be aware of with this strategy:
1. Improper selection of underlying stocks may result in failure to follow the trend.
2. Improper parameter setting may lead to excessive trading frequency or missed trading opportunities.
3. Unexpected events cause trend reversal, which may lead to expansion of losses.
4. Setting the stop loss point too close may lead to too frequent stops.
5. Insufficient trading volume may result in failure to complete the transaction.
6. The backtest cycle is short, which may lead to overfitting.
Corresponding measures include: selecting stocks with good liquidity and obvious trends; adjusting parameters to achieve the best results; paying attention to major news to prevent reversals; appropriately relaxing stop loss points; evaluating real trading volumes; and expanding backtesting cycles to test stability.
### Optimization direction
This strategy can be optimized from the following directions:
1. Optimize parameters, such as Bollinger Band period, standard deviation multiple, moving average period, etc., to find the best parameter combination.
2. Add stop loss methods, such as trailing stop loss, average stop loss, etc., to further control risks.
3. Increase position management, adjust position size according to key points, and manage capital utilization efficiency.
4. Combine with trading volume indicators to avoid invalid breakthroughs with low volume.
5. Combined with the relative strength indicator, determine the general direction of buying and selling.
6. Add machine learning algorithms to realize automatic optimization of parameters and strategy evaluation.
7. Combine other strategies to form a multi-strategy combination to improve stability.
Through these optimizations, the effectiveness and stability of the strategy can be further enhanced.
### Summarize
The overall idea of ​​this strategy is clear and easy to understand. By systematically capturing the opportunities to buy at short-term lows and sell at highs, it can effectively track the stock trend and obtain better returns while controlling risks. The strategy can be further improved through parameter optimization, stop loss method improvement, position management, etc., and has great application potential in real trading. This strategy provides a good basic framework for automated trend trading.
||


### Overview

This strategy implements automated trend following trading by calculating Bollinger Bands to identify dips and peaks and using long-term and short-term moving averages to determine the overall trend direction. The core idea is to buy dips and sell peaks according to the prevailing trend.

### Strategy Logic

The key components of the strategy are:

1. Calculate Bollinger Bands with upper and lower bands based on close price and standard deviation. 

2. Determine long-term and short-term trend using 300-period and 20-period SMA.

3. Generate buy signal when close breaks below lower band while long SMA is above and short SMA turns up. 

4. Generate sell signal when close breaks above upper band while long SMA is below and short SMA turns down.

5. Use OCO orders to set stop loss and take profit.

With this design, the strategy can automatically identify dip buying and peak selling opportunities along the major trend direction.

### Advantage Analysis 

The advantages of this strategy include:

1. Automated trend detection without manual judgment.

2. Systematically capture dips for buying opportunities.

3. Systematically identify peak selling opportunities for profit taking.

4. Effective risk control using stop loss and take profit. 

5. Filter out invalid signals to improve win rate.

6. Flexible trend following by position adjustment. 

7. Clear logic and easy to understand and optimize.

### Risk Analysis

The main risks to consider:

1. Inappropriate security selection could fail the trend tracking.

2. Improper parameter tuning may cause overtrading or missed trades. 

3. Trend reversal from sudden events may lead to larger losses.

4. Stop loss too tight may cause excessive stops. 

5. Insufficient liquidity may prevent full execution. 

6. Overfitting with insufficient backtesting period.

The solutions include: select liquid stocks with clear trends; optimize parameters; watch out for news; relax stop loss; evaluate real trading volume; expand backtest period.

### Optimization Directions

Some ways to optimize the strategy:

1. Optimize parameters like Bollinger period, standard deviation multiplier and moving average periods.

2. Add stop loss methods like trailing stop or moving average stop to better control risks.

3. Incorporate position sizing based on key levels to improve capital utilization efficiency. 

4. Add volume filter to avoid invalid breakouts with low volume.

5. Add relative strength indicator to determine buy/sell bias.

6. Introduce machine learning for automatic parameter tuning and strategy evaluation.

7. Combine with other strategies to create multi-strategy portfolio for greater robustness.

These optimizations can further enhance the strategy's performance and stability.

### Summary

The strategy offers a clear and understandable approach to systematically buy dips and sell peaks along the trend. With proper risk control, it has good profit potential. Further improvements can be made via parameter tuning, stop loss modification, position sizing, etc. The strategy serves as a solid foundation for automated trend following trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|15|length|
|v_input_2|1.25|mult|
|v_input_3|300|longMAPeriod|
|v_input_4|20|shortMAPeriod|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-23 00:00:00
end: 2023-10-23 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Buy Dip Sell Rip Strategy", overlay=true)
source = close
length = input(15, minval=1)
mult = input(1.25, minval=0.001, maxval=50)
longMAPeriod = input(300, minval=5)
shortMAPeriod = input(20, minval=5)

basis = sma(source, length)
longMA = sma(source, longMAPeriod)
prevLongMA = sma(close[1],longMAPeriod)
shortMA = sma(source, shortMAPeriod)
dev = mult * stdev(source, length)

upper = basis + dev
lower = basis - dev

buyEntry = crossover(source, lower)
sellEntry = crossunder(source, upper)

if (source > lower and source[1] < lower)
    if (longMA < source  and shortMA>source)
        strategy.entry("BBandLE", strategy.long, stop=lower, oca_name="BollingerBands",  comment="BBandLE")
    else
        strategy.close("BBandSE")
else
    strategy.cancel(id="BBandLE")

if (source > upper and source[1] < upper)
    if (longMA > source  and shortMA < source)
        strategy.entry("BBandSE", strategy.short, stop=upper, oca_name="BollingerBands",  comment="BBandSE")
    else 
        strategy.close("BBandLE")
else
    strategy.cancel(id="BBandSE")

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)

```

> Detail

https://www.fmz.com/strategy/430031

> Last Modified

2023-10-24 13:54:18
