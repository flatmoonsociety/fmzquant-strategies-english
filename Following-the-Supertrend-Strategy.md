
> Name

Following-the-Supertrend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c682eb812ab1584f1c.png)

[trans]


### Overview
This strategy is based on the super trend indicator, uses the super trend line to determine the trend direction, and uses the super trend line as the stop loss line to implement an automatic trading strategy that tracks the super trend trend. This strategy is suitable for varieties with obvious trends, and can capture medium and long-term trends and track strong trends.
### Strategy Principle
The supertrend indicator is calculated from the average true amplitude (ATR) and a specified multiplier, and can effectively determine the direction of the price trend. When the price is above the upper trend line, it is an uptrend, and when the price is below the lower trend line, it is a downtrend.
This strategy first calculates the upper and lower trend lines. The upper trend line is calculated as the average of the high and low prices minus N times the ATR. A lower trend line is calculated as the average of the highest and lowest prices plus N times the ATR. Where N is the multiplier parameter set by the user.
The direction of the price relative to the trend is then calculated. When the price is higher than the lower trend line of the previous K line, it is defined as an upward trend. When the price is lower than the upper trend line of the previous K line, it is defined as a downward trend.
According to the judged trend direction, choose the upper or lower trend line as the upper trend line. When the trend is up, the super trend line takes the upper trend line; when the trend is down, the super trend line takes the super trend line.
Finally, the strategy uses the super-trend line as the stop-loss line. When the price crosses the super-trend line, it goes long. When the price crosses the super-trend line, it goes short. Once the price touches the super-trend line, it stops the loss and exits.
### Advantage Analysis
This strategy mainly has the following advantages:
1. Use super-trend indicators to determine the direction of price trends and effectively track trends.
2. The super trend line serves as a stop loss line to limit losses.
3. The strategy retracement is small, the Sharpe ratio reaches 2.51, and the performance is stable.
4. The number of transactions is up to 1988, and parameters can be optimized to improve the winning rate.
5. Realize fully automatic transactions without manual intervention.
### Risk Analysis
There are also some risks with this strategy:
1. Super trend indicators are sensitive to price changes and may generate more whipsaw signals, reducing profits.
2. It is easy to stop losses in a volatile trend and is not suitable for sideways trading varieties.
3. The impact of major economic events has not been taken into account, which may result in larger losses during this period.
4. The profit-loss ratio is only 41%, and the trading winning rate needs to be improved.
5. Parameters need to be optimized to adapt to different varieties and time periods.
6. Strict fund management is required to prevent excessive single losses.
### Optimization Directions
This strategy can be optimized from the following directions:
1. Combine with other indicators for filtering to avoid whipsaw and improve the winning rate. For example MA, MACD, etc.
2. Add trend confirmation to avoid misjudgment of exceeding the trend line and generating wrong signals. For example, add channel breakout confirmation.
3. Adjust parameters to suit different varieties and time periods. For example, adjust the ATR cycle parameters.
4. Join the popular economic event avoidance strategy and avoid major news release periods.
5. Optimize the stop loss strategy and optimize the stop loss through trailing stop loss, tail stop loss, etc.
6. Optimize position management and adjust xpos according to market conditions to control risk exposure.
### Conclusion
This strategy designs a simple trend following strategy based on super-trend indicators. The performance is acceptable, but there are many trading signals and the winning rate needs to be improved. By cooperating with other indicators for filtering optimization, adjusting parameters to suit different varieties, and strict fund management, this strategy can become a stable trend following strategy with mild retracement. However, attention needs to be paid to guard against the risks caused by misjudgment.
||

## Following the Supertrend Strategy

### Overview

This strategy is based on the Supertrend indicator to determine the trend direction using Supertrend lines, and take Supertrend lines as stop loss lines to implement an automated trading strategy that follows Supertrend trends. It is suitable for products with obvious trend tendencies and can capture mid-to-long term trends to follow strong trends.

### Strategy Principle 

The Supertrend indicator is calculated from the Average True Range (ATR) and a multiplier, which can effectively determine the price trend direction. When the price is above the upper Supertrend line, it is an upward trend. When the price is below the lower Supertrend line, it is a downward trend.

The strategy first calculates the upper and lower Supertrend lines. The upper Supertrend line is calculated as the average of the highest and lowest prices minus the ATR multiplied by N. The lower Supertrend line is calculated as the average of the highest and lowest prices plus the ATR multiplied by N. Where N is the multiplier parameter set by the user.

Then it calculates the direction of the trend relative to the price. When the price is higher than the lower Supertrend line of the previous bar, it is defined as an upward trend. When the price is lower than the upper Supertrend line of the previous bar, it is defined as a downward trend.

According to the determined trend direction, choose the upper Supertrend line or the lower Supertrend line as the Supertrend line. When it is an upward trend, take the upper Supertrend line as the Supertrend line. When it is a downward trend, take the lower Supertrend line as the Supertrend line.

Finally, the strategy takes the Supertrend line as the stop loss line. It goes long when the price crosses above the Supertrend line, and goes short when the price crosses below the Supertrend line. It exits the position once the price touches the Supertrend line.

### Advantage Analysis

The main advantages of this strategy are:

1. Using the Supertrend indicator to determine the price trend direction can effectively follow trends.

2. The Supertrend line as a stop loss line can limit losses. 

3. The strategy has a small drawdown with a Sharpe ratio of 2.51, showing stable performance.

4. There are as many as 1988 trades, allowing parameter optimization to improve win rate.

5. It implements fully automated trading without manual intervention.

### Risk Analysis

There are also some risks with this strategy:

1. The Supertrend indicator is sensitive to price changes and may generate more whipsaw signals, reducing profitability.

2. It is prone to stop loss in range-bound trends and is not suitable for sideways products. 

3. It does not consider the impact of major economic events, which may cause large losses during those periods.

4. The profit ratio is only 41% and the win rate needs improvement.

5. Parameters need to be optimized for different products and time frames.

6. Strict money management is required to prevent excessive losses in single trades.

### Optimization Directions

The strategy can be optimized in the following aspects:

1. Add filters with other indicators to avoid whipsaws and improve win rate, such as MA, MACD, etc.

2. Increase trend confirmation to avoid wrong signals from Supertrend line misjudgments. For example, add channel breakout confirmation.

3. Adjust parameters to suit different products and time frames, such as adjusting ATR period. 

4. Add strategies to avoid major economic news events.

5. Optimize stop loss strategies through trailing stop loss, parabolic SAR, etc.

6. Optimize position sizing based on market conditions by adjusting xpos to control risk exposure.

### Conclusion

This strategy designed a simple trend following strategy based on the Supertrend indicator with decent performance, but more trading signals and room for improving win rate. By optimizing with other indicators for filtration, adjusting parameters for different products, and applying prudent money management, this strategy can become a stable trend following strategy with mild drawdown. But be aware of the risks associated with misjudgments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|SuperTrend Multiplier|
|v_input_2|14|SuperTrend Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-16 00:00:00
end: 2023-10-23 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("QuantNomad - SuperTrend - XBTUSD - 1m", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)

// INPUTS //
st_mult   = input(2,   title = 'SuperTrend Multiplier', minval = 0, maxval = 100, step = 0.01)
st_period = input(14, title = 'SuperTrend Period',     minval = 1)

// CALCULATIONS //
up_lev = hl2 - (st_mult * atr(st_period))
dn_lev = hl2 + (st_mult * atr(st_period))

up_trend   = 0.0
up_trend   := close[1] > up_trend[1]   ? max(up_lev, up_trend[1])   : up_lev

down_trend = 0.0
down_trend := close[1] < down_trend[1] ? min(dn_lev, down_trend[1]) : dn_lev

// Calculate trend var
trend = 0
trend := close > down_trend[1] ? 1: close < up_trend[1] ? -1 : nz(trend[1], 1)

// Calculate SuperTrend Line
st_line = trend ==1 ? up_trend : down_trend

// Plotting
plot(st_line[1], color = trend == 1 ? color.green : color.red , style = plot.style_line, linewidth = 2, title = "SuperTrend")

plotshape(crossover( close, st_line), location = location.belowbar, color = color.green)
plotshape(crossunder(close, st_line), location = location.abovebar, color = color.red)

// Strategy with stop orders
strategy.entry("long",  true,  stop = st_line)
strategy.entry("short", false, stop = st_line)
```

> Detail

https://www.fmz.com/strategy/430038

> Last Modified

2023-10-24 14:28:29
