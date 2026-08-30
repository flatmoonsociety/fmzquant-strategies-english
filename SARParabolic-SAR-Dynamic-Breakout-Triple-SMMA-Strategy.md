
> Name

SAR Dynamic Tracking Breakout Three Moving Average Strategy Parabolic-SAR-Dynamic-Breakout-Triple-SMMA-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](https://www.fmz.com/upload/asset/1a4f3ced46ef3f60589.png)
[trans]


### Overview
This is a breakout trading strategy that combines the Parabolic SAR indicator with three SMMA moving averages of different periods. It goes long when the three moving averages rise across the board, and goes short when the three moving averages fall across the board. At the same time, it combines the SAR indicator to determine the trend direction, and opens a reverse position when the SAR indicator turns. This strategy supports both stop loss and take profit.
### Strategy Principles
This strategy is mainly based on the following points:
1. Use the Parabolic SAR indicator to determine the current trend direction. The SAR indicator can dynamically track price changes and determine bullish and bearish trends.
2. Set three SMMA moving averages with different periods (fast line 21 periods, middle line 50 periods, slow line 200 periods). When all three moving averages rise, a bullish trend is formed; when all three moving averages fall, a short trend is formed.
3. When the SAR indicator turns downward, if the three moving averages rise across the board, enter the market long.
4. When the SAR indicator turns upward, if the three moving averages fall across the board, enter the market short.
5. Set stop loss and take profit. The stop loss uses the SAR indicator as the dynamic stop loss level, and the take profit is set to a certain proportion of the entry price.
Specifically, the strategy first determines whether the SAR indicator of the current BAR has turned. If the SAR turns from up to down, and all three moving averages rise across the board, go long; if the SAR turns from down to up, and all three moving averages fall across the board, go short.
After holding the position, the stop loss line is set to the SAR indicator price of the next BAR, and SAR is used as the dynamic trailing stop. Take profit is set to 10% of the entry price. When the price reaches the take profit or stop loss level, close the position and exit.
### Advantage Analysis
This strategy combines the advantages of trend judgment indicators and multi-time period moving averages. It can enter the market in time when the trend turns and at the same time filter out false breakthroughs through the moving average. The main advantages are:
1. The SAR indicator can dynamically determine trend changes and quickly capture trend conversion opportunities.
2. Three moving averages can effectively filter market noise and avoid false breakthroughs.
3. Using SMMA moving average, the curve is smoother and reduces the interference of moving average fluctuations on transactions.
4. Combined with stop-loss and stop-profit settings, you can control a single loss and lock in part of the profit.
5. The strategy parameter setting is flexible, and parameters can be adjusted for different markets to optimize the strategy effect.
### Risk Analysis
This strategy also has some risks, mainly including:
1. In a turbulent trend, the SAR indicator may undergo multiple frequent turns, resulting in too frequent transactions and increased transaction costs.
2. The three moving average settings may not be completely suitable for all varieties and need to be adjusted according to the market conditions of specific varieties.
3. There is a time lag in setting the stop loss to the SAR price of the next BAR, which may increase losses.
4. The problem of false breakthroughs causing SAR to turn in a stable trend can be alleviated by adjusting parameters to smooth the SAR curve.
5. Improper moving average settings may miss the trend or generate wrong signals, which requires careful testing and optimization.

Corresponding risks can be optimized from the following points:
1. Adjust SAR parameters according to the degree of fluctuation of different varieties to reduce the probability of frequent turns.
2. Adjust the parameters of the three moving averages to make them closer to the characteristics of different varieties.
3. Optimize the stop loss strategy, such as using small stop loss, trailing stop loss, etc.
4. Use limit orders to stop losses in markets with frequent transactions to avoid slippage and expand losses.
5. Carry out parameter tuning tests and evaluate the impact of moving average and SAR parameters on the strategy effect.
### Optimization direction
Based on the above analysis, this strategy can be optimized from the following aspects:
1. Optimize SAR parameter settings, smooth the SAR curve, reduce the frequency of curve turning, and avoid over-trading.
2. Adjust the length of the three moving averages to make them more consistent with the characteristics of specific trading varieties and play a better trend filtering role.
3. Use dynamic stop loss strategies, such as trailing stop loss, small stop loss for pending orders, etc., to reduce losses caused by stop loss.
4. Use limit orders to stop losses in high-frequency trading markets to reduce stop-loss slippage losses.
5. Add other indicators for filtering, such as RSI, KD, etc., to improve signal quality and reduce the probability of false breakthroughs.
6. To optimize entry conditions, consider checking the K-line pattern when SAR turns to avoid low-quality signals.
7. Add re-entry conditions to re-enter when the price continues to move in a favorable direction after the stop loss.
8. Improve take-profit strategies, such as moving take-profit, partial take-profit, stepped take-profit, etc., to improve profitability.
9. Optimize parameters based on backtest results and evaluate the impact of parameters on the overall strategy effect.
### Summarize
Overall, this is a simple and practical breakout strategy that combines the trend following indicators SAR and moving averages. It uses SAR's sensitivity to determine trend reversal and the filtering effect of moving averages to quickly enter the market at trend turning points. At the same time, set stop loss and take profit to control risks and lock in profits. By adjusting the parameter SETTINGS and optimizing the entry and exit conditions, better strategic effects can be obtained. However, traders need to pay attention to controlling issues such as over-trading and false breakthroughs, and conduct parameter tuning and strategy testing for different varieties to obtain a stable trading system.
|| 


### Overview

This is a breakout trading strategy combining the parabolic SAR indicator and triple SMMA lines with different periods. It goes long when all three SMMA lines are rising and goes short when all are falling, while using the SAR indicator to determine the trend direction and taking counter trend entries when SAR flips directions. The strategy also incorporates stop loss and take profit.

### Strategy Logic

The strategy is based on the following key points:

1. Using the parabolic SAR indicator to determine the current trend direction. SAR can dynamically track price changes and identify uptrends and downtrends.

2. Setting up three SMMA lines with different periods (fast line 21, mid line 50, slow line 200). When all three lines are rising, it signals an uptrend. When all are falling, it signals a downtrend.

3. Going long when SAR flips down while all three SMMA lines are rising. 

4. Going short when SAR flips up while all three SMMA lines are falling.

5. Incorporating stop loss based on SAR and take profit at certain percentage of entry price.

Specifically, the strategy first checks if SAR flips directions on the current bar. If SAR flips from up to down while SMMAs are rising, it goes long. If SAR flips from down to up while SMMAs are falling, it goes short. 

After entry, the stop loss is set at the SAR price on the next bar, using SAR as a dynamic trailing stop loss. Take profit is set at 10% of the entry price. When price reaches either take profit or stop loss levels, the position is closed.

### Advantage Analysis

This strategy combines the advantage of a trend-following indicator and multiple time frame moving averages, allowing timely entries at trend reversals while filtering out false breaks with SMMAs. The main advantages are:

1. SAR can quickly detect trend changes and capture reversal opportunities.

2. The triple SMMAs effectively filter out market noise and avoid false breaks.

3. Using SMMA results in smoother curves and less interference from MA whipsaws. 

4. Incorporating stop loss and take profit helps control single trade loss and lock in partial profits.

5. Flexible parameter settings allow optimization for different markets.

### Risk Analysis

There are also some risks to consider:

1. SAR may flip frequently during choppy trends, increasing costs from excessive trading.

2. SMMA settings may not fit all instruments well, requiring individual optimization.

3. SAR stop loss has time lag, potentially increasing losses. 

4. SAR may flip on false breaks in steady trends. Smoothening SAR parameters can help.

5. Poor SMMA settings may cause missed trends or bad signals. Careful testing is needed.

To address the risks, optimizations can focus on:

1. Adjusting SAR parameters based on volatility to reduce flips.

2. Tuning SMMA periods to fit instrument characteristics. 

3. Improving stop loss, e.g. with trailing or limit orders.

4. Using limit orders for stop loss in active trading.

5. Extensive testing and tuning of parameters.

### Optimization Directions

Based on the above analysis, optimizations may involve:

1. Optimizing SAR parameters for smoother curves and fewer flips.

2. Adjusting SMMA lengths to match trading instruments.

3. Employing dynamic stop loss like trailing stops or limit orders. 

4. Using limit orders for stop loss in high-frequency trading.

5. Adding filters like RSI, KD to improve signal quality.

6. Improving entry conditions, e.g. checking candle patterns with SAR flips.

7. Adding re-entry conditions after stop loss triggers.

8. Enhancing take profit with trailing, partial close, staggering levels.

9. Parameter tuning based on backtest results and sensitivity analysis.

### Summary

In summary, this is a simple and practical breakout strategy combining the sensitivity of SAR in catching trend changes and the filtering effect of moving averages. It can identify trend reversal points fast. The use of stop loss and take profit helps control risks and lock in profits. Further optimizations on parameter settings, entry/exit rules, and robustness against false breaks can enhance strategy performance for different trading instruments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|0.02|(?SAR)start|
|v_input_float_2|0.02|increment|
|v_input_float_3|0.2|maximum|
|v_input_float_4|0.1|(?Stop Loss and Take Profit)Take Profit (%)|
|v_input_float_5|true|StopLoss (%)|
|v_input_int_1|21|(?Smooth Moving Average)Fast Length|
|v_input_int_2|50|Mid Length|
|v_input_int_3|200|Slow Length|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-08 00:00:00
end: 2023-11-07 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(title="SAR + 3SMMA with SL & TP", overlay=true, calc_on_order_fills=false, calc_on_every_tick=false, default_qty_type=strategy.percent_of_equity, default_qty_value=100, currency=currency.USD, commission_type= strategy.commission.percent, commission_value=0.03)
start = input.float(0.02, step=0.01, group="SAR")
increment = input.float(0.02, step=0.01, group="SAR")
maximum = input.float(0.2, step=0.01, group="SAR")

//Take Profit Inputs     
take_profit = input.float(title="Take Profit (%)", minval=0.0, step=0.1, defval = 0.1, group="Stop Loss and Take Profit", inline="TP") * 0.01

//Stop Loss Inputs
stop_loss = input.float(title="StopLoss (%)", minval=0.0, step=0.1, defval=1, group="Stop Loss and Take Profit", inline="SL") * 0.01

// Smooth Moving Average
fastSmmaLen = input.int(21, minval=1, title="Fast Length", group = "Smooth Moving Average")
midSmmaLen = input.int(50, minval=1, title="Mid Length", group = "Smooth Moving Average")
slowSmmaLen = input.int(200, minval=1, title="Slow Length", group = "Smooth Moving Average")

src = input(close, title="Source", group = "Smooth Moving Average")

smma(ma, src, len) => 
    smma = 0.0
    smma := na(smma[1]) ? ma : (smma[1] * (len - 1) + src) / len
    smma

fastSma = ta.sma(src, fastSmmaLen)
midSma = ta.sma(src, midSmmaLen)
slowSma = ta.sma(src, slowSmmaLen)

fastSmma = smma(fastSma, src, fastSmmaLen)
midSmma = smma(midSma, src, midSmmaLen)
slowSmma = smma(slowSma, src, slowSmmaLen)

isSmmaUpward = ta.rising(fastSmma, 1) and ta.rising(midSmma, 1) and ta.rising(slowSmma, 1)

var bool uptrend = na
var float EP = na
var float SAR = na
var float AF = start
var float nextBarSAR = na

if bar_index > 0
	firstTrendBar = false
	SAR := nextBarSAR
	if bar_index == 1
		float prevSAR = na
		float prevEP = na
		lowPrev = low[1]
		highPrev = high[1]
		closeCur = close
		closePrev = close[1]
		if closeCur > closePrev
			uptrend := true
			EP := high
			prevSAR := lowPrev
			prevEP := high
		else
			uptrend := false
			EP := low
			prevSAR := highPrev
			prevEP := low
		firstTrendBar := true
		SAR := prevSAR + start * (prevEP - prevSAR)
	if uptrend
		if SAR > low
			firstTrendBar := true
			uptrend := false
			SAR := math.max(EP, high)
			EP := low
			AF := start
	else
		if SAR < high
			firstTrendBar := true
			uptrend := true
			SAR := math.min(EP, low)
			EP := high
			AF := start
	if not firstTrendBar
		if uptrend
			if high > EP
				EP := high
				AF := math.min(AF + increment, maximum)
		else
			if low < EP
				EP := low
				AF := math.min(AF + increment, maximum)
	if uptrend
		SAR := math.min(SAR, low[1])
		if bar_index > 1
			SAR := math.min(SAR, low[2])
	else
		SAR := math.max(SAR, high[1])
		if bar_index > 1
			SAR := math.max(SAR, high[2])
	nextBarSAR := SAR + AF * (EP - SAR)

sarIsUpTrend = uptrend ? true : false

sarFlippedDown = sarIsUpTrend and not sarIsUpTrend[1] ? true : false
sarFlippedUp = not sarIsUpTrend and sarIsUpTrend[1] ? true : false


longEntryCondition = isSmmaUpward and sarFlippedDown
shortEntryCondition = not isSmmaUpward and sarFlippedUp

if(longEntryCondition)
    strategy.entry("L", strategy.long, stop=nextBarSAR, comment="L")

if(shortEntryCondition)
    strategy.entry("S", strategy.short, stop=nextBarSAR, comment="S")


strategy.exit("CL", when=strategy.position_size > 0, limit=strategy.position_avg_price * (1+take_profit), stop=strategy.position_avg_price*(1-stop_loss))
strategy.exit("CS", when=strategy.position_size < 0, limit=strategy.position_avg_price * (1-take_profit), stop=strategy.position_avg_price*(1+stop_loss))


plot(SAR, style=plot.style_cross, linewidth=1, color=color.orange)
plot(nextBarSAR, style=plot.style_cross, linewidth=1, color=color.aqua)
plot(series = fastSmma, title="fastSmma", linewidth=1)
plot(series = midSmma, title="midSmma", linewidth=2)
plot(series = slowSmma, title="slowSmma", linewidth=3)
plotchar(series = isSmmaUpward, title="isSmmaUpward", char='')
plotchar(series=sarIsUpTrend, title="sarIsUpTrend", char='')
plotchar(series=sarFlippedUp, title="sarFlippedUp", char='')
plotchar(series=sarFlippedDown, title="sarFlippedDown", char='')
plotchar(series=longEntryCondition, title="longEntryCondition", char='')
plotchar(series=shortEntryCondition, title="shortEntryCondition", char='')
plotchar(series=strategy.position_size > 0, title="inLong", char='')
plotchar(series=strategy.position_size < 0, title="inShort", char='')


//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)


```

> Detail

https://www.fmz.com/strategy/431495

> Last Modified

2023-11-08 11:53:09
