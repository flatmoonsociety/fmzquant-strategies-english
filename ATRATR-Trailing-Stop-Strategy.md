
> Name

ATR Trailing Stop Strategy ATR-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

Overview: The ATR trailing stop loss strategy is a trading strategy that dynamically sets stop loss levels based on the average true volatility indicator. This strategy is suitable for foreign exchange trading varieties with large price fluctuations. It sets stop losses by dynamically tracking market fluctuations, capturing profits in the general trend while controlling risks.
### Strategy Principles
This strategy forms a trading channel by calculating the AVERAGE indicator (the average price) and the upper track DIFF and lower track DIFFLOW calculated based on the ATR indicator. Go long when the price crosses the upper rail DIFF, go short when the price crosses the lower rail DIFFLOW, use ATR to dynamically set the stop loss position, and close the position when the stop loss is reached.
Specifically, the strategy first calculates the price's simple moving average AVERAGE and ATR indicators, and calculates the upper track DIFF and lower track DIFFLOW based on the ATR value multiplied by a multiple coefficient. This forms a trading channel, and the upper and lower boundaries of the channel are determined by DIFF and DIFFLOW. When the price breaks through the upper band, take a long position; when the price breaks through the lower band, take a short position. In addition, the stop loss position will also dynamically change as the ATR value changes, thereby achieving variable stop loss.
In this way, the strategy can continuously go long and short in the general trend to capture profits, and at the same time control risks through ATR dynamic tracking stop loss, which is suitable for varieties with large fluctuations.
### Advantage Analysis
This strategy has the following advantages:
1. Use the ATR indicator for dynamic stop loss. You can flexibly set the stop loss position according to the degree of market volatility to avoid the stop loss being too close or too far.
2. Establish trading channels to capture mean reversion opportunities in the general trend. When the price stays in the channel, this strategy can achieve better capital utilization.
3. Continuously participate in the trend by going long and short. There is no need to predict upward or downward price breakthroughs. Follow the trend to obtain better profits.
4. Simple parameter setting and trading rules, easy to understand and implement, suitable for automatic trading.
5. The capital utilization rate is high, there is no need to predict the direction of breakthroughs, and continuous trading can obtain more profit opportunities.
### Risk and optimization analysis
There are also some risks to be aware of with this strategy:
1. If the ATR parameter is set too large, the stop loss distance will be too far and the risk cannot be effectively controlled. It is recommended that the ATR coefficient be set to 1-3 times the daily ATR.
2. In a consolidating market, trading is active and prices fluctuate greatly, so stop losses will be triggered frequently. The ATR coefficient can be adjusted appropriately to reduce the frequency of stop loss triggering.
3. In some cases, the price may break through the channel and then reverse back. At this time, the strategy will cause losses. You can combine it with a trend filter to only enter when the trend direction breaks through the channel.
4. When there is a large change, stop loss may not be able to play a good protective role. Consider adding a maximum stop loss setting to avoid excessive stop loss.
This strategy can be optimized as follows:
1. Optimize the ATR parameters and find the appropriate ATR multiple coefficient, which can not only track the stop loss, but also prevent the stop loss from being too sensitive.
2. Add trend judgment indicators, only go long when the trend is up, go short when the trend is down, and avoid non-trend transactions.
3. Test the parameters separately for different varieties and find the suitable parameter combination for each variety.
4. To optimize entry opportunities, consider entering when the channel breaks through the central axis.
5. Increase the size of the position, but also control the overall loss from being too large.
### Summarize
The ATR tracking stop loss strategy establishes a trading channel to continuously trade in the general trend to capture profits, and at the same time uses ATR to dynamically set stop losses and control risks. This strategy is suitable for volatile varieties and can achieve better capital utilization. In practice, parameters need to be optimized, and trend judgment can be considered for further improvement. Generally speaking, the ATR trailing stop loss strategy is a simple and practical trend following strategy.
||

Overview: The ATR trailing stop strategy is a trading strategy that dynamically sets stop loss levels based on the Average True Range (ATR) indicator. It is suitable for volatile FOREX pairs, capturing profits in major trends while controlling risk by dynamically tracking market volatility.  

### Strategy Logic

The strategy calculates the AVERAGE indicator (price moving average) and upper/lower bands DIFF/DIFFLOW based on ATR values, forming a trading channel. It goes long when price crosses above DIFF and goes short when price crosses below DIFFLOW, with stops set dynamically based on ATR.  

Specifically, it first calculates the simple moving average AVERAGE and ATR indicator. The upper band DIFF and lower band DIFFLOW are then computed by multiplying ATR values with a coefficient. This forms a trading channel bounded by DIFF and DIFFLOW. When price breaks above the upper band, a long position is taken. When price breaks below the lower band, a short position is taken. In addition, the stop loss level moves dynamically with ATR values. This allows for adaptive stops.

Thus the strategy can continuously go long/short to capture profits in major trends, while using ATR trailing stops to control risk. This makes it suitable for volatile instruments.

### Advantage Analysis

The advantages of this strategy include:

1. ATR-based dynamic stops adjust to market volatility, avoiding stops too close or too far. 

2. Trading channel aims to capture mean reversion within trends. Good capital utilization when price oscillates within channel.

3. Continuous trend trading without predicting breakouts. Follows trends for better profitability.

4. Simple parameters and rules, easy to understand and automate.

5. High capital utilization, continuous trading provides more profit opportunities.

### Risks and Improvements

Some risks to consider:

1. Large ATR coefficients lead to stops too far away, failing to control risk. ATR multiples of 1-3x daily ATR are recommended.

2. Whipsaws in range-bound markets trigger frequent stops. Adjust ATR coefficients to reduce unwanted stops.

3. Potential losses when price reverses after initial breakout. Adding trend filter to trade channel breaks only in trend direction.  

4. Big spikes can make stops ineffective. Consider adding maximum stop loss limits.

Possible optimizations:

1. Optimize ATR parameters to find right balance between tracking volatility and preventing excessive stops.

2. Add trend indicator, only trade breaks in trend direction. Avoid countertrend trades.

3. Test parameters individually for each instrument to find optimal values.

4. Optimize entry, consider entering on channel midline breakouts. 

5. Increase position sizes while controlling total risk/drawdown.

### Conclusion
The ATR trailing stop strategy trades continuously in trends while dynamically managing risk. It suits volatile instruments and provides good capital utilization. Parameter optimization and adding filters can further refine performance. Overall a simple and practical trend following strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|26|Length|
|v_input_2|true|Length|
|v_input_3|2|Length|
|v_input_4|8|From Month|
|v_input_5|18|From Day|
|v_input_6|2008|From Year|
|v_input_7|true|To Month|
|v_input_8|true|To Day|
|v_input_9|2020|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-18 00:00:00
end: 2023-09-25 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Investoz

//@version=4
strategy("ATR Strategy FOREX", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

len = input(26, type=input.integer, minval=1, title="Length")
mul = input(1, type=input.float, minval=0, title="Length")
mullow = input(2, type=input.float, minval=0, title="Length")

price = sma(close, 1)
average = ema(close, len)
diff = atr(len) * mul
difflow = atr(len) * mullow

bull_level = average + diff
bear_level = average - difflow
bull_cross = crossunder(price, bear_level)
bear_cross = crossunder(bull_level, price)

FromMonth = input(defval = 8, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 18, title = "From Day", minval = 1, maxval = 31)
FromYear  = input(defval = 2008, title = "From Year", minval = 2008)
ToMonth   = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
ToYear    = input(defval = 2020, title = "To Year", minval = 2019)

start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)       
startTimeOk()  => true

if (startTimeOk())
    strategy.entry("KOP", strategy.long, when=bull_cross)
    strategy.close("KOP", when=bear_cross)  
    strategy.entry("SALJ", strategy.short, when=bear_cross)
    strategy.close("SALJ", when=bull_cross)

plot(price, title="price", color=color.black, transp=50, linewidth=2)
a0 = plot(average, title="average", color=color.red, transp=50, linewidth=1)
a1 = plot(bull_level, title="bull", color=color.green, transp=50, linewidth=1)
a2 = plot(bear_level, title="bear", color=color.red, transp=50, linewidth=1)
fill(a0, a1, color=color.green, transp=97)
fill(a0, a2, color=color.red, transp=97)
```

> Detail

https://www.fmz.com/strategy/427925

> Last Modified

2023-09-26 20:23:13
