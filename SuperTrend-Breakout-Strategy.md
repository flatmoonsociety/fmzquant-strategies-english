
> Name

SuperTrend-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/134269a5b75a42232e6.png)
[trans]

### Overview
This strategy uses the average true volatility indicator and the ascending and descending channel formed by the upper and lower rails calculated by price to generate trading signals when the price breaks through the channel. The strategy has outstanding trend following capabilities.
### Strategy Principles
This strategy first calculates the ATR indicator as a measure of price fluctuations, and then combines the average of the highest price, lowest price, and closing price to calculate the upper and lower rails. When the price rises and breaks through the lower track, a buy signal is generated; when the price falls and breaks through the upper track, a sell signal is generated. In this way, an adaptive ascending and descending channel is formed to track the price trend.
After entering the market, the strategy will set the target profit points and stop loss points. When the price reaches the target points, the profit will be taken. If the retracement reaches the stop loss points, the loss will be stopped.
### Advantage Analysis
The biggest advantage of this strategy is its excellent trend following capabilities. The ascending and descending channels can be adjusted adaptively to capture changes in price trends. At the same time, the use of the ATR indicator also provides a certain guarantee of following the trend. In addition, the stop-profit and stop-loss mechanism in the strategy also makes profit and loss control clearer.
### Risk Analysis
One of the main risks of this strategy is that it tends to generate more short positions. When the price is in shock, the upper and lower channels are often triggered frequently, resulting in more invalid transactions. In addition, the stop loss point setting will also directly affect the final profit.
To reduce these risks, you can consider optimizing the ATR parameters or adjusting the channel width to make the channel closer to the real trend. In addition, you can also combine other indicators to filter market entry opportunities.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize ATR parameters. Different cycle parameters can be tested to make ATR better reflect the real fluctuations.
2. Channel width optimization. Different multiplier values ​​can be tested to determine the optimal parameters.
3. Add other indicator filters. For example, combining the MACD indicator to determine buying and selling points can reduce invalid transactions to a certain extent.
4. Optimize stop loss points and take profit points. Test the impact of different parameters on the final yield.
5. Consider Sharpe ratio or profit-loss ratio as an optimization goal. to more fully assess strategy quality.
### Summarize
This strategy achieves excellent trend following through adaptive ascending channels and breakout principles. At the same time, it also has relatively clear take-profit and stop-loss logic. Through certain parameter and rule optimization, it is expected to further enhance the dynamic tracking performance of the strategy and make it applicable to a wider range of market environments.
||

### Overview   

This strategy generates trading signals when price breaks out of the uptrend/downtrend channel formed by the SuperTrend indicator. The strategy has outstanding trend following ability.   

### Strategy Logic

The strategy first calculates the ATR indicator as a measure of price volatility, then combines it with the average of highest, lowest and closing prices to compute the upper and lower bands. When price breaks above the lower band during an uptrend, a buy signal is generated. When price breaks below the upper band during a downtrend, a sell signal is triggered. This forms an adaptive uptrend/downtrend channel that tracks price trends.   

After entering the market, the strategy sets target profit ticks and stop loss ticks. It closes position for profit when price reaches the profit target, and stops out when drawdown hits the stop loss level.  

### Advantage Analysis  

The biggest advantage of this strategy is its excellent trend following ability. The adaptive channel can capture trend changes quickly. Using ATR also provides some assurance of trading along with momentum. In addition, the profit target and stop loss mechanism gives clear risk/reward control.  

### Risk Analysis   

One major risk is that it may generate excessive whipsaws during range-bound markets, as the price constantly pierces through the bands. In addition, stop loss setting also directly impacts final results.  

To reduce such risks, parameters like ATR period or channel multiplier could be optimized to fit the true trend better. Other filters may also be added on entry signals to avoid whipsaws.

### Enhancement Opportunities

The strategy can be enhanced in several aspects:

1. Optimize ATR parameters to better reflect actual volatility dynamics. 

2. Test different multipliers for channel width optimization.

3. Add other indicators as filters on entries, e.g. MACD for better timing.

4. Optimize profit target and stop loss levels for maximized risk-adjusted returns. 

5. Consider other objectives like Sharpe ratio or profit factor to evaluate overall quality.

### Summary  

The strategy leverages the adaptive channel breakout model to achieve great trend following ability. It also has clear risk control mechanisms. With further parameter tuning and logic enhancement, it has the potential to work even better across various market conditions and asset classes.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|10|ATR Length|
|v_input_float_1|3|Multiplier|
|v_input_int_2|100|Target Points|
|v_input_int_3|50|Stop Loss Points|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-26 00:00:00
end: 2024-02-26 20:20:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Supertrend Strategy", overlay=true)

// Input parameters
atr_length = input.int(10, title="ATR Length")
multiplier = input.float(3.0, title="Multiplier")

target_points = input.int(100, title="Target Points")
stop_loss_points = input.int(50, title="Stop Loss Points")

// Calculate ATR and Supertrend
atr = ta.atr(atr_length)
upper_band = hlc3 + (multiplier * atr)
lower_band = hlc3 - (multiplier * atr)
is_uptrend = close > lower_band
is_downtrend = close < upper_band
trend_changed = (is_uptrend[1] and is_downtrend) or (is_downtrend[1] and is_uptrend)

// Strategy logic
long_condition = is_uptrend and trend_changed
short_condition = is_downtrend and trend_changed

// Plot Supertrend
plot(is_uptrend ? lower_band : na, color=color.green, title="Supertrend Up", style=plot.style_linebr)
plot(is_downtrend ? upper_band : na, color=color.red, title="Supertrend Down", style=plot.style_linebr)

// Strategy entry and exit
if long_condition
    strategy.entry("Long", strategy.long)
if short_condition
    strategy.entry("Short", strategy.short)

// Calculate target and stop loss levels
long_target = strategy.position_avg_price + target_points
long_stop_loss = strategy.position_avg_price - stop_loss_points
short_target = strategy.position_avg_price - target_points
short_stop_loss = strategy.position_avg_price + stop_loss_points

// Strategy exit
strategy.exit("Long Exit", "Long", limit=long_target, stop=long_stop_loss)
strategy.exit("Short Exit", "Short", limit=short_target, stop=short_stop_loss)

```

> Detail

https://www.fmz.com/strategy/443044

> Last Modified

2024-02-28 18:12:47
