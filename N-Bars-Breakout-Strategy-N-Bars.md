
> Name

N-Bars-Breakout-Strategy-N-Bars-Breakout Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b71d4a63cb656904c020f8509ea00512bce2ac1c2100624bbe6997b94700340b.png)

[trans]
#### Overview
The N Bars breakout strategy is a quantitative trading strategy based on price breakouts. The main idea of ​​this strategy is to open a long position when the closing price breaks through the highest price of the past N trading days, and close the long position when the closing price falls below the lowest price of the past N trading days. This strategy compares the current price with the highest and lowest prices in the past N trading days to capture strong market breakthroughs and achieve the effect of trend following.
#### Strategy Principle
1. Calculate the highest and lowest prices in the past N trading days.
2. If the current closing price is higher than the highest, open a long position (long).
3. If the current closing price is lower than the lowest, close the long position (short).
4. You can choose to use closing price (close) or high/low price (high/low) as the signal source.
5. Depending on the signal source, use ta.highest and ta.lowest to calculate the highest and lowest prices.
6. Use ta.crossover and ta.crossunder to determine price breakthroughs.
#### Strategic Advantages
1. The logic is simple and clear, easy to implement and optimize.
2. Can effectively capture strong market breakthroughs and has strong trend following capabilities.
3. The parameter tuning space is large and can be optimized according to different varieties and cycles.
4. It has wide applicability and has good performance on most varieties and cycles.
5. You can flexibly select signal sources to improve strategy adaptability.
#### Strategy Risk
1. Poor performance in volatile market conditions and small fluctuations, and frequent opening and closing of positions results in higher transaction costs.
2. Improper parameter selection may lead to the risk of overfitting.
3. A large retracement may occur when the trend turns.
4. A single signal source may face the risk of signal distortion.
#### Strategy optimization direction
1. Add trend filter conditions, such as MA trend direction, adx, etc., to reduce transactions under volatile market conditions.
2. Optimize parameter selection, such as N value, signal source, etc., to improve strategy stability and profitability.
3. Add stop loss and trailing stop loss logic to control single transaction risk.
4. Combine multiple signal sources to improve signal reliability, such as considering closing prices and high and low price breakthroughs at the same time.
5. Optimize parameters and logic respectively according to different varieties and cycles.
#### Summary
The N Bars breakthrough strategy is a simple and practical quantitative trading strategy that achieves better trend tracking effects by capturing price breakthroughs. This strategy has clear logic, large optimization space, and wide applicability. It is a quantitative strategy worthy of further research and optimization. Through reasonable parameter optimization and logic improvement, the stability and profitability of the strategy can be further improved and better adapted to different market environments.
|| 

#### Overview
The N Bars Breakout Strategy is a quantitative trading strategy based on price breakouts. The main idea of this strategy is to open a long position when the closing price breaks above the highest high of the past N bars, and close the long position when the closing price breaks below the lowest low of the past N bars. By comparing the current price with the highest and lowest prices of the past N bars, this strategy aims to capture strong breakout moves and achieve the effect of trend following.

#### Strategy Principle
1. Calculate the highest high (highest) and lowest low (lowest) of the past N bars.
2. If the current closing price is higher than the highest, open a long position (long).
3. If the current closing price is lower than the lowest, close the long position (short).
4. You can choose to use the closing price (close) or high/low price (high/low) as the signal source.
5. Depending on the signal source, use ta.highest and ta.lowest to calculate the highest and lowest prices.
6. Use ta.crossover and ta.crossunder to determine price breakouts.

#### Strategy Advantages
1. Simple and clear logic, easy to implement and optimize.
2. Can effectively capture strong breakout moves, with strong trend-following capability.
3. Large room for parameter optimization, can be optimized for different instruments and timeframes.
4. Wide applicability, performs well for most instruments and timeframes.
5. Flexible choice of signal source, improving strategy adaptability.

#### Strategy Risks
1. Performs poorly in choppy and small-fluctuation markets, with frequent opening and closing of positions leading to high transaction costs.
2. Improper parameter selection may lead to overfitting risk.
3. May experience large drawdowns during trend reversals.
4. Single signal source may face the risk of signal distortion.

#### Strategy Optimization Directions
1. Add trend filtering conditions, such as MA trend direction, ADX, etc., to reduce trading in choppy markets.
2. Optimize parameter selection, such as N value, signal source, etc., to improve strategy stability and profitability.
3. Add stop-loss and trailing stop-loss logic to control single-trade risk.
4. Combine multiple signal sources to improve signal reliability, such as considering both closing price and high/low price breakouts.
5. Optimize parameters and logic separately for different instruments and timeframes.

#### Summary
The N Bars Breakout Strategy is a simple and practical quantitative trading strategy that achieves good trend-following effects by capturing price breakouts. The strategy has clear logic, large optimization space, and wide applicability, making it a quantitative strategy worth further research and optimization. Through reasonable parameter optimization and logic improvement, the stability and profitability of this strategy can be further enhanced to better adapt to different market environments.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|5|N Bars|
|v_input_string_1|Close|Source|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-04-06 00:00:00
end: 2024-04-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Breakout", overlay=true, precision=6, pyramiding=0, initial_capital=1000, default_qty_type=strategy.percent_of_equity, default_qty_value=25.0, commission_value=0.05)

n = input.int(5, "N Bars", minval=1)
src_input = input.string("Close", "Source", ["Close", "High/Low"])

bull_src = switch src_input
	"Close" => close
	"High/Low" => high
	=>
		runtime.error("Invalid source input")
		na

bear_src = switch src_input
	"Close" => close
	"High/Low" => low
	=>
		runtime.error("Invalid source input")
		na

highest = ta.highest(bull_src[1], n)
lowest = ta.lowest(bear_src[1], n)

//-----------------------------------------------------------------------------------------------------------------------------------------------------------------
// Plots
//-----------------------------------------------------------------------------------------------------------------------------------------------------------------

bool long = ta.crossover(bull_src, highest)
bool short = ta.crossunder(bear_src, lowest)

//Plots
lowest_plot  = plot(lowest,  color=color.red, title="Lowest")
highest_plot  = plot(highest,  color=color.green, title="Highest")
bull_src_plot = plot(bull_src, color=color.blue, title="Bull")
bear_src_plot = plot(bear_src, color=color.orange, title="Bear")

// this message is an alert that can be sent to a webhook, which allows for simple automation if you have a server that listens to alerts and trades programmatically.
enter_long_alert = '{"side": "Long", "order": "Enter", "price": ' + str.tostring(open) + ', "timestamp": ' + str.tostring(timenow) + '}'
exit_long_alert = '{"side": "Long", "order": "Exit", "price": ' + str.tostring(open) + ', "timestamp": ' + str.tostring(timenow) + '}'

if long
    strategy.entry(id="Long", direction=strategy.long, limit=open, alert_message=enter_long_alert)

if short
    strategy.close(id="Long", comment="Close Long", alert_message=exit_long_alert)
```

> Detail

https://www.fmz.com/strategy/448067

> Last Modified

2024-04-12 16:57:15
