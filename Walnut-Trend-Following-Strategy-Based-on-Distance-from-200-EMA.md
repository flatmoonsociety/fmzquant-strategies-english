
> Name

Walnut-Trend-Following-Strategy-Based-on-Distance-from-200-EMA
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/187acfb97a481b452b3.png)
[trans]

This article will analyze in detail a trend-following strategy based on the distance between the 200-day moving average and price, called the "Nuts Offline Trend Following Strategy." This strategy tracks the distance between price and the 200-day moving average, establishes a position when it exceeds a set threshold, and closes the position after reaching the profit target.
**1. Strategy Principle**
The core indicator of this strategy is the 200-day exponential moving average (200 EMA). The strategy determines whether the price deviates from the 200-day line by a set percentage, and then establishes a position when the last K line is a positive line (long entry) or a negative line (short entry). The entry conditions for longs are that the price is lower than the 200-day line and the distance percentage between the price and the 200-day line is greater than the threshold, and the entry is long when the last K-line closes the positive line; the entry conditions for the shorts are that the price is higher than the 200-day line and the distance percentage between the price and the 200-day line is greater than the threshold, and the entry is short when the last K-line closes the negative line.
The exit condition is to close the position when the price returns to the 200-day moving average or reaches the take-profit target (1.5 times the entry price). Set the stop loss at 20% of the option's declared value.
Detailed entry and exit conditions are as follows:
**Bull entry:** The closing price <200-day line and the distance percentage between the closing price and the 200-day line ≥ the threshold and the most recent K-line closed positive
**Short entry:** The closing price > the 200-day line and the distance percentage between the closing price and the 200-day line ≥ the threshold and the most recent K-line closed as a negative line
**Bull exit:** The closing price ≥ 200-day line or the profit-taking target is reached or the trading day ends
**Short exit:** Closing price <= 200-day line or reach profit-taking target or end of trading day
The stop loss condition is 20% of the declared value of the option.
**2. Strategic advantages**
This strategy mainly has the following advantages:
1. Use the 200-day moving average to determine the medium and long-term price trend direction to avoid being disturbed by short-term market noise.
2. Establish a trend tracking mechanism to track medium and long-term price trends
3. Optimize the judgment of entry timing and enter when the direction of the last K-line is consistent with the general trend.
4. Reasonable stop-loss and stop-profit mechanisms to avoid loss expansion
**3. Strategic Risk**
This strategy mainly involves the following risks:
1. During the market shock period, the price may touch the moving average multiple times, resulting in multiple losses.
2. A sudden reversal in trend causes stop loss and exit.
3. The set parameters, such as the moving average period, are improperly selected and the trend cannot be accurately judged.
In order to reduce the above risks, the following aspects can be optimized:
1. Adjust moving average parameters, or add other indicators to determine the general trend
2. Optimize the stop loss mechanism, such as adjusting the stop loss distance according to price changes
3. Optimize entry conditions and add more judgment indicators
**4. Strategy Optimization Direction**
This strategy can be optimized mainly from the following aspects:
1. Optimize the moving average parameters and test the impact of different period parameters on the strategy effect.
2. Add other indicators to judge the general trend, such as Bollinger Bands channel, KDJ indicator, etc.
3. Adjust the stop loss strategy so that the stop loss level can be dynamically adjusted according to market changes
4. Optimize entry conditions to avoid incorrect entry due to short-term adjustments
**5. Summary**
This article analyzes in detail the principles, advantages, risks and optimization directions of the trend following strategy based on the distance between price and the 200-day moving average. This strategy determines the direction of the mid- to long-term trend by tracking the distance between the price and the long-term moving average. When the price reaches a certain threshold above the moving average, a position is opened to track the trend, and the exit condition is triggered by stop loss or take profit. This strategy can track medium and long-term price trends very well, but there is also some room for parameter optimization. In the future, this strategy can be continued to be improved from many aspects so that it can obtain stable returns under more different market conditions.
||

This article will analyze in detail a trend following strategy based on the distance between price and 200-day moving average, called “Walnut Trend Following Strategy Based on Distance from 200 EMA”. This strategy establishes positions when the price exceeds a preset threshold from the 200-day moving average and closes positions when reaching the profit target.  

**I. Strategy Logic**

The core indicator of this strategy is the 200-day exponential moving average (200 EMA). The strategy judges if the price deviates from the 200-day line by a set percentage threshold. Long positions are established when the last candlestick is a green candle and short positions are established when the last candlestick is a red candle. The long entry conditions are price below 200 EMA and price percentage deviation above threshold. The short entry conditions are price above 200 EMA and price percentage deviation above threshold.

The exit conditions are when price reverts to 200 EMA or reaches 1.5 times the entry price as profit target. The stop loss is set at 20% of the option premium.  

The detailed entry and exit conditions are:

**Long Entry:** Close < 200 EMA && Percentage Distance ≥ Threshold && Last Candle Green

**Short Entry:** Close > 200 EMA && Percentage Distance ≥ Threshold && Last Candle Red   

**Long Exit:** Close ≥ 200 EMA || Reaches Profit Target || End of Day

**Short Exit:** Close <= 200 EMA || Reaches Profit Target || End of Day

The stop loss is 20% of the option premium.

**II. Advantages**

The main advantages of this strategy are:

1. Using 200-day moving average to determine medium-long term trend, avoiding short-term market noise  
2. Establishing trend following mechanism to track medium-long term price trend
3. Optimizing entry timing when last candle direction aligns with major trend   
4. Reasonable stop loss and take profit to avoid larger losses

**III. Risks**  

The main risks of this strategy are:

1. Multiple losses may occur during market consolidation around moving average
2. Sudden trend reversal triggers stop loss
3. Inappropriate parameter selection like moving average period leads to inaccurate trend judgment

The following aspects can be optimized to reduce the above risks:

1. Adjust moving average parameters or add other indicators to determine major trend
2. Optimize stop loss mechanism like adjusting stop distance based on price change 
3. Optimize entry conditions with more judgment indicators  

**IV. Optimization Directions**

The main optimization directions for this strategy are:  

1. Optimize moving average parameters, test impacts of different period parameters
2. Add other indicators like Bollinger Bands, KDJ to determine major trend
3. Adjust stop loss strategy to trail price dynamically   
4. Optimize entry conditions to avoid wrong entries due to short-term corrections

**V. Conclusion**   

This article analyzed in detail the logic, strengths, weaknesses and optimization directions of the trend following strategy based on the distance between price and 200-day moving average. This strategy judges medium-long term trend by tracking the price deviation from long-term moving average. Positions are established when the deviation exceeds a threshold and closed when hitting stop loss or take profit targets. This strategy can track medium-long term trend well but still has some parameter optimization space. Future improvements can be made from multiple perspectives to make the strategy more robust across different market conditions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|EMA Period|
|v_input_2|0.75|Threshold Percent|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-22 00:00:00
end: 2024-02-24 06:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Intraday Price Away from 200 EMA Strategy", overlay=true)

// Define inputs
emaPeriod = input(200, title="EMA Period")
thresholdPercent = input(0.75, title="Threshold Percent", minval=0)  // Define the threshold percentage

// Calculate 200 EMA
ema = ema(close, emaPeriod)

// Calculate distance from 200 EMA as a percentage
distance_percent = ((close - ema) / ema) * 100

// Track average entry price
var float avgEntryPrice = na

// Buy conditions
buy_condition = close < ema and abs(distance_percent) >= thresholdPercent and close[1] < close[2]

// Exit conditions for buy
exit_buy_condition = close >= ema or time_close(timeframe.period) or (avgEntryPrice * 1.5) <= close

// Sell conditions
sell_condition = close > ema and abs(distance_percent) >= thresholdPercent and close[1] > close[2]

// Exit conditions for sell
exit_sell_condition = close <= ema or time_close(timeframe.period) or (avgEntryPrice * 1.5) >= close

// Execute buy and sell orders only if there are no open trades
if strategy.opentrades == 0
    strategy.entry("Buy", strategy.long, when=buy_condition)
    strategy.entry("Sell", strategy.short, when=sell_condition)

// Update average entry price for buy condition
if buy_condition
    avgEntryPrice := close

// Update average entry price for sell condition
if sell_condition
    avgEntryPrice := close

// Close buy position if exit condition is met
strategy.close("Buy", when=exit_buy_condition)

// Close sell position if exit condition is met
strategy.close("Sell", when=exit_sell_condition)

// Plot 200 EMA
plot(ema, color=color.blue, linewidth=2)

// Plot buy and sell signals
plotshape(buy_condition, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small)
plotshape(sell_condition, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.small)

```

> Detail

https://www.fmz.com/strategy/443228

> Last Modified

2024-03-01 10:50:03
