
> Name

Based on Dual-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/19cc992015e07f4eeab.png)
[trans]
## Overview
This strategy utilizes double moving averages to form channels to capture the direction of the trend. Trading signals are generated when price breaks out of the channel. At the same time, combine the RSI indicator to filter out false breakthroughs. Only operates during London trading hours, with a maximum of 5 orders per day and a maximum loss of no more than 2%.
## Strategy Principle
This strategy uses two moving averages of length 5, one calculated from the highest price and one calculated from the lowest price, to form a price channel. Go long when the closing price breaks through the upper edge of the channel, and go short when it breaks through the lower edge of the channel.
In order to filter out false breakthroughs, the RSI indicator is also introduced to determine overbought and oversold. Only go long when the RSI is above 80 and short when it is below 20.
In addition, the strategy only trades during the London trading hours (3am to 11am), with a maximum of 5 orders per day and a maximum loss of no more than 2% of the equity in the stock.
## Advantage Analysis
### Capture trends
Double moving averages build trend channels and can better judge the direction of price trends. When the price breaks through the upper rail of the channel upward, the upward trend of the price is captured; when the price breaks through the lower rail of the channel downward, the downward trend of the price is captured.
### Reduce false breakthroughs
Combining the RSI indicator to determine overbought and oversold areas can reduce false breakthroughs caused by price shocks to a certain extent.
### Effectively control risks
The strategy only conducts transactions during the main active trading hours, and a maximum of 5 orders per day can effectively control the trading frequency; the maximum loss is set to 2% to control the maximum loss in a single day within a tolerable range.
## Risk Analysis
### The risk of false breakthrough when the price fluctuates greatly
When prices fluctuate significantly, certain false breakthrough signals may appear, which may lead to unnecessary trading losses. This risk can be reduced by adjusting parameter optimization or adding filter conditions.
### Fixed stop loss and take profit are easy to be trapped in the risk
The strategy uses a fixed number of points for stop loss and take profit. When the price fluctuates significantly, the fixed number of points for stop loss and take profit can easily be trapped. Therefore, percentage or dynamic stop loss and take profit should be used.
### Limited trading hours risk
The strategy only opens positions during fixed trading periods. If no signal is generated during this period, potential trading opportunities in other periods will be missed. You can consider appropriately expanding the trading time or dynamically adjusting it according to real-time conditions.
## Optimization direction
### Parameter optimization
You can optimize the length of the moving average, RSI parameters, fixed stop loss and take profit points, etc. to find the optimal parameter combination.
### Add filter conditions
Other indicators or conditions can be added to double-check the breakthrough signal, such as increasing trading volume, narrowing the Bollinger Bands channel, etc., to reduce false breakthroughs.
### Dynamic stop loss and take profit
You can use a percentage stop loss or dynamic stop loss strategy instead of a simple fixed point stop loss to better hedge the risk of unilateral market conditions.
### Combined with manual judgment
Manually review the signal, or only enter the market after a confirmed breakthrough to avoid being trapped.
## Summarize
This strategy is generally relatively simple and practical. It uses dual moving averages to build a channel to determine the trend direction; at the same time, the RSI indicator can effectively filter out some false breakthroughs. In terms of risk control, limiting trading hours and maximum losses can control overall risks. There is still a lot of room for optimization, and improvements can be made in terms of parameter optimization and stop-loss mechanism upgrades.
||

## Overview

This strategy uses dual moving averages to form a channel and capture trend direction. Trading signals are generated when price breaks through the channel. RSI indicator is also incorporated to filter false breakouts. It trades only during London session with max 5 trades per day and max 2% daily loss.

## Strategy Logic

The strategy employs two moving averages of length 5, one calculated from highest price and the other from lowest price, to form a price channel. Long signal triggers when close price breaks above the upper band, and short signal below the lower band. 

To avoid false breakout, RSI indicator is added to gauge overbought/oversold levels. Go long only if RSI is above 80, and go short only if RSI is below 20.

Also, the strategy trades only during London session (3am - 11am), with max 5 orders per day and max 2% loss of equity per day.

## Advantage Analysis 

### Catch the trend

The dual MA channel can effectively detect price trend direction. Breaking upper band catches the upside trend, while breaking lower band catches the downside trend.

### Reduce false breakout  

Using RSI overbought/oversold filter reduces some false breakout signals caused by price fluctuation.

### Effective risk control

Trading only during major session and having max orders per day limit trading frequency. Max 2% daily loss also defines risk tolerance.

## Risk Analysis

### False breakout with volatility

Significant price swing can cause some false breakout signals, leading to unnecessary losses. Parameters can be optimized and more filters added to reduce such risk.

### Fixed SL/TP risk

Using fixed pips for SL/TP risks being stopped out/missing profit in volatile market. Consider percentage-based or dynamic SL/TP instead.

### Limited trading session risk 

Opening positions only during fixed sessions runs the risk of missing potential trades in other hours. Consider expanding session or adjust dynamically based on real-time situation.

## Optimization Directions 

### Parameter tuning
Optimize parameters like MA length, RSI figures, fixed SL/TP pips etc to find best combination.

### Additional filters
Add more indicators or conditions to verify signals, e.g. higher volume, reduced BB width etc, to avoid false breakouts.

### Dynamic SL/TP
Use percentage-based or dynamic stop loss/take profit instead of fixed pips to better handle one-sided market moves.

### Manual review
Manually review signals, or only enter on confirmed breakout to prevent being trapped.

## Conclusion
The strategy is fairly simple and practical overall, using dual MA channel to determine trend and RSI to filter false breakouts. Risk management via trading hours and loss limit also defines risk tolerance. Still large room for improvements, e.g. parameter tuning, better SL/TP mechanism etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Length|
|v_input_2_high|0|Source: high|close|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|false|Offset|
|v_input_4|5|Length|
|v_input_5_low|0|Source: low|high|close|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_6|false|Offset|
|v_input_7|5|length|
|v_input_8|10|overSold|
|v_input_9|80|overBought|
|v_input_10_close|0|Source RSI: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_11|150|tp|
|v_input_12|80|sl|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-16 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SoftKill21
//@version=4
strategy(title="Moving Average", shorttitle="MA", overlay=true)
timeinrange(res, sess) => time(res, sess) != 0
len = input(5, minval=1, title="Length")
src = input(high, title="Source")
offset = input(title="Offset", type=input.integer, defval=0, minval=-500, maxval=500)
out = sma(src, len)
plot(out, color=color.white, title="MA", offset=offset)

len2 = input(5, minval=1, title="Length")
src2 = input(low, title="Source")
offset2 = input(title="Offset", type=input.integer, defval=0, minval=-500, maxval=500)
out2 = sma(src2, len2)
plot(out2, color=color.white, title="MA", offset=offset2)

length = input( 5 )
overSold = input( 10 )
overBought = input( 80 )
price = input(close, title="Source RSI")

vrsi = rsi(price, length)

longcond= close > out and close > out2 and vrsi > overBought
shortcont = close < out and close < out2 and vrsi < overSold
tp=input(150,title="tp")
sl=input(80,title="sl")


strategy.entry("long",1,when=longcond)
//strategy.close("long",when= close < out2)
strategy.exit("long_exit","long",profit=tp,loss=sl)

strategy.entry("short",1,when=shortcont)
//strategy.close("short",when=close >out)
strategy.exit("short_exit","short",profit=tp,loss=sl)

// maxOrder = input(6, title="max trades per day")
// maxRisk = input(2,type=input.float, title="maxrisk per day")
// strategy.risk.max_intraday_filled_orders(maxOrder)

// strategy.risk.max_intraday_loss(maxRisk, strategy.percent_of_equity)


// strategy.close_all(when =not timeinrange(timeframe.period, "0300-1100"))





```

> Detail

https://www.fmz.com/strategy/442377

> Last Modified

2024-02-21 14:43:26
