
> Name

Golden-Parabola-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c088cafeb6927cc610.png)
[trans]

### Overview
The gold parabolic breakout strategy is a technical analysis strategy that combines the judgment of the gold parabola shape and the moving average breakthrough Exit signal. The goal is to enter the market when the gold parabola is formed and exit when it breaks through the Exit signal to achieve trading profits.
### Strategy Principles
This strategy is mainly based on the following judgment rules:
1. Draw a gold parabolic channel using a simple moving average of the highest and lowest prices on 5 candles.
2. When the closing price breaks through the channel from bottom to top, a golden parabolic shape is formed, which serves as a buy signal to enter the market. At this time, it means that the price is breaking through the upper edge of the channel and may enter the market.
3. After buying, Trail trailing stop loss is near the entry price to prevent stop loss. At the same time, set a moving take-profit line to lock in profits.
4. When the price breaks through the lower edge of the channel, an Exit signal is generated, the buy order is closed, and the market is exited. At this time, it indicates that the price may re-enter the shock or downward channel.
The main judgment criteria of this strategy include the judgment of the gold parabolic shape and the judgment of the moving average breakthrough Exit signal, so that it can enter when the trend breaks through, and the risk can be controlled through moving stop-profit and stop-loss.
### Strategic Advantages
This strategy has the following advantages:
1. Combines morphological analysis and technical indicator judgment to improve the reliability of trading signals.
2. Use trailing stop loss to control the risk of single loss and avoid excessive losses.
3. Use moving take-profit to lock in profits and prevent profit taking.
4. It has a high profit-loss ratio and is suitable for investors who pursue stable income.
5. The easytrade strategy has simple syntax and is easy to write and optimize.
### Strategy Risk
This strategy also has the following risks:
1. The price may not effectively break through the channel, resulting in a false breakthrough. This will cause unnecessary losses. The probability of false breakthroughs can be reduced by optimizing parameters.
2. The trailing stop may be breached, thereby expanding losses. This requires setting the stop loss distance appropriately.
3. Moving take profit may lead to premature exit and loss of greater profit opportunities. This requires adjusting the take profit position according to the market.
4. Channel parameters need to be adjusted in a timely manner to adapt to market adjustments in different cycles.
### Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Optimize channel parameters, find a more suitable parameter combination, and improve signal quality.
2. Add other filtering conditions, such as sudden increase in transaction volume, to improve the accuracy of signals.
3. Try other exit signals, such as Bollinger Bands Exit or SAR Stop, etc., to find a better exit point.
4. Test different stop loss and take profit algorithms to optimize fund management.
5. Add an adaptability module to enable automatic optimization of strategy parameters based on real-time market conditions.
### Summarize
The gold parabolic breakthrough strategy combines morphological analysis and technical indicator judgment, and has the advantages of high quality trading signals and risk control with stop loss and profit. This strategy can be optimized in a variety of ways to improve profitability. It is a quantitative trading strategy that is easy to master and has stable returns. It is suitable for investors who have a certain foundation but want to obtain stable income.
||

### Overview  

The golden parabola breakout strategy is a technical analysis strategy that combines the judgment of golden parabola patterns and the breakout of moving average exit signals to enter the market when the golden parabola pattern is formed and exit when the exit signal breaks out, in order to make profitable trades.

### Strategy Principles  

The main judgment rules of this strategy are:  

1. Use the simple moving average of the highest and lowest prices of 5 K-lines to draw the golden parabola channel.

2. When the closing price breaks through the channel upwards, it forms a golden parabola pattern as a buy signal to enter the market. This indicates that the price is breaking through the upper edge of the channel and may be entering a trend.

3. After buying, set the trailing stop loss near the entry price to prevent loss. At the same time, set the trailing take profit line to lock in profits.  

4. When the price breaks through the lower edge of the channel, it generates an exit signal to close the long order and exit the market. This indicates that the price may re-enter the shock or downward channel.

The main judgment criteria of this strategy include golden parabola pattern judgment and moving average breakout exit signal judgment, allowing it to enter during trend breakouts and control risks through trailing stops and take profits.   

### Advantages  

This strategy has the following advantages:

1. Combining pattern analysis and technical indicators improves the reliability of trading signals.  

2. The trailing stop loss controls the risk of single loss and avoids excessive losses.

3. The trailing take profit locks in profits and prevents profit retracement.  

4. It has a relatively high profit ratio and is suitable for investors seeking stable returns.  

5. The easytrade strategy syntax is simple and easy to write and optimize.

### Risks 

The strategy also has the following risks:

1. Prices may not break through the channel effectively, causing false breakouts. This will cause unnecessary losses. You can reduce the probability of false breakouts by optimizing parameters.

2. The trailing stop loss may be broken through, thus expanding losses. This requires reasonably setting stop loss distances. 

3. The trailing take profit may exit too early, missing greater profit opportunities. This requires adjusting take profit positions based on market conditions.  

4. Need to adjust channel parameters in a timely manner to adapt to trend adjustments in different cycles.

### Optimization Directions

The strategy can be optimized in the following aspects:  

1. Optimize channel parameters to find more suitable parameter combinations to improve signal quality.

2. Add other filtering conditions such as trading volume surges to improve signal accuracy.   

3. Try other exit signals such as Bollinger Bands exit or SAR stop to find better exit points.  

4. Test different stop loss, take profit algorithms to optimize money management.  

5. Add adaptive modules to automatically optimize strategy parameters based on real-time market conditions.

### Summary  

The golden parabola breakout strategy combines pattern analysis and technical indicators for relatively high quality trading signals and uses stops and take profits to control risks. This strategy can improve profitability through various optimization methods and is an easy to master quantitative trading strategy with stable returns. It is suitable for investors with some foundation who want stable returns.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Number of Candles for Average|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-02-03 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("5MABAND + GBS Buy & Sell Strategy", overlay=true)

// Command 1 - 5MABAND Calculation
length = input(5, title="Number of Candles for Average")
avgHigh = ta.sma(high, length)
avgLow = ta.sma(low, length)

// Plotting 5MABAND Bands
plot(avgHigh, color=color.green, title="5MABAND High Line", linewidth=1)
plot(avgLow, color=color.red, title="5MABAND Low Line", linewidth=1)

// Command 2 - GBS concept Buy Entry
gbsBuyCondition = close > open and high - close < close - open and open - low < close - open and close - open > close[1] - open[1] and close - open > close[2] - open[2] and close - open > close[3] - open[3] and close[1] < avgHigh and close[2] < avgHigh and close[3] < avgHigh and open[1] < avgHigh and open[2] < avgHigh and open[3] < avgHigh

// Command 3 - GBS Concept Sell Entry
gbsSellCondition = open - close > open[1] - close[1] and open - close > open[2] - close[2] and open - close > open[3] - close[3] and open[1] > avgLow and open[2] > avgLow and open[3] > avgLow and open - close > open - low and open - close > high - open

// Command 6 - 5MABAND Exit Trigger
exitTriggerCandle_5MABAND_Buy = low < avgLow
exitTriggerCandle_5MABAND_Sell = high > avgHigh

// Exit Signals for 5MABAND
exitBuySignal_5MABAND = close < avgLow
exitSellSignal_5MABAND = close > avgHigh

// Execute Buy and Sell Orders
strategy.entry("Buy", strategy.long, when = gbsBuyCondition)
strategy.close("Buy", when = exitBuySignal_5MABAND)

strategy.entry("Sell", strategy.short, when = gbsSellCondition)
strategy.close("Sell", when = exitSellSignal_5MABAND)

// Exit Buy and Sell Orders for 5MABAND
strategy.close("Buy", when = exitTriggerCandle_5MABAND_Buy)
strategy.close("Sell", when = exitTriggerCandle_5MABAND_Sell)

```

> Detail

https://www.fmz.com/strategy/441013

> Last Modified

2024-02-04 18:07:14
