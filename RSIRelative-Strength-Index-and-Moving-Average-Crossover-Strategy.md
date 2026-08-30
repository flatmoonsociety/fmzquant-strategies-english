
> Name

RSI Indicator and Average Crossover Strategy Relative-Strength-Index-and-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/32041c05f0b7369606.png)
[trans]

## Overview
The RSI indicator and average crossover strategy is a quantitative trading strategy that combines the relative strength index (RSI) and moving averages. This strategy uses the RSI indicator to determine the overbought and oversold conditions of a security's value, and combines the golden cross and dead cross signals of RSI and its average line to decide to establish a bullish or bearish position.
## Strategy Principle
1. Calculate the RSI indicator value. The RSI indicator is based on the rise and fall over a period of time and determines whether a security is overbought or oversold by comparing the average closing gain with the average closing fall.
2. Calculate the moving average MA of the RSI indicator. Use exponential moving average EMA or simple moving average SMA.
3. When the RSI indicator crosses its moving average, a golden cross signal is generated and you go long; when the RSI indicator goes below its moving average, a dead cross signal is generated and you go short.
4. When the RSI is above the overbought line, the security is considered overbought and you go short; when the RSI is below the oversold line, the security is considered oversold and you go long.
## Advantage Analysis
1. Combine indicators and average line cross signals to avoid relying on only one indicator when making orders and improve the accuracy of decision-making.
2. Use the RSI indicator to determine the timing of overbought and oversold conditions, set overbought and oversold lines, and determine the timing of opening positions and stopping losses.
3. Use indicators to cross the average line to do long and short positions, and you can capture the market turning point in time.
## Risk Analysis
1. The RSI indicator is prone to produce false signals in volatile markets.
2. The basis for judging RSI overbought and oversold can be adjusted. Improper settings may lead to being too loose or strict.
3. The moving average system is too sensitive to short-term abnormal fluctuations and may be trapped in stop losses.
## Optimization direction
1. Adjust RSI parameters and find the best length parameters.
2. Optimize the moving average parameters and find the best moving average period.
3. Test different overbought and oversold line parameters to optimize the opportunity to open a position.
4. Combine with other indicators to filter signals to avoid wrong transactions.
## Summarize
RSI indicator and average line crossover strategy, using RSI to determine overbought and oversold combined with moving average crossover signals, can effectively determine market hot areas and capture reversal opportunities at key points. Through parameter optimization and signal filtering, strategy performance can be improved and trading risks reduced. This strategy is suitable for short- and medium-term traders and can provide better excess returns.
|| 

## Overview  

The Relative Strength Index (RSI) and Moving Average Crossover strategy combines the RSI indicator and moving averages to make quantitative trading decisions. It utilizes the overbought and oversold levels indicated by RSI to determine entries and exits, alongside golden cross and death cross signals generated when RSI crosses its moving average line.

## Strategy Logic   

1. Calculate the RSI indicator value. RSI measures the magnitude of recent price changes to evaluate if an asset is overbought or oversold. 

2. Compute a moving average line (MA) of RSI, using an Exponential Moving Average (EMA) or Simple Moving Average (SMA).  

3. When RSI crosses above its MA line, a golden cross buy signal is generated. When RSI crosses below its MA line, a death cross sell signal is triggered.

4. When RSI rises above the overbought threshold, the asset is considered overbought and a short position can be initiated. When RSI falls below the oversold threshold, the asset is considered oversold and a long position can be opened.

## Advantage Analysis

1. Combining indicator crossover signals with RSI overbought/oversold levels improves the accuracy of trading decisions.   

2. RSI overbought and oversold thresholds determine optimal entries and exits.

3. Capturing trend reversals by acting on indicator crossover signals. 

## Risk Analysis  

1. RSI may generate incorrect signals during choppy or sideways markets.

2. Improper overbought or oversold threshold settings could lead to signals that are too loose or too strict. 

3. Moving averages are sensitive to short-term anomalies and volatility spikes, increasing the likelihood of being stopped out prematurely.

## Optimization Directions 

1. Optimize RSI parameter by testing different length periods.  

2. Find the optimal moving average periods by assessing different MA lengths.

3. Test various overbought and oversold threshold levels to refine entry signals.  

4. Incorporate additional filters to validate signals and avoid false trades.

## Conclusion

The RSI and Moving Average Crossover Strategy combines RSI overbought/oversold levels with MA crossover signals to identify market turning points and capture reversals. Performance and risk management can be enhanced through parameter optimization and signal filtering. This medium-term trading strategy offers strong alpha generation potential for experienced investors.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|13|Length|
|v_input_2|9|MA Lenght|
|v_input_3|false|Exponential|
|v_input_4|10|From Month|
|v_input_5|3|From Day|
|v_input_6|2017|From Year|
|v_input_7|true|To Month|
|v_input_8|true|To Day|
|v_input_9|9999|To Year|
|v_input_10|90|RSI % start overbought|
|v_input_11|10|RSI % start oversold|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-14 00:00:00
end: 2023-12-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//dfurrer45
strategy(title="Relative Strength Index", shorttitle="RSI", overlay=true)
src = close, len = input(13, minval=1, title="Length"), maLen = input(9, minval=1, title="MA Lenght"), exponential = input(false, title="Exponential")

// === BACKTEST RANGE ===
FromMonth = input(defval = 10, title = "From Month", minval = 1)
FromDay   = input(defval = 3, title = "From Day", minval = 1)
FromYear  = input(defval = 2017, title = "From Year", minval = 2014)
ToMonth   = input(defval = 1, title = "To Month", minval = 1)
ToDay     = input(defval = 1, title = "To Day", minval = 1)
ToYear    = input(defval = 9999, title = "To Year", minval = 2014)
// ===  BACKTEST END  ===
backtestdaterange = (time > timestamp(FromYear, FromMonth, FromDay, 00, 00))

rsioverbought = input(90, minval=1, title="RSI % start overbought")
rsioversold = input(10, minval=1, title="RSI % start oversold")
up = rma(max(change(src), 0), len)
down = rma(-min(change(src), 0), len)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
ma = exponential ? ema(rsi, maLen) : sma(rsi, maLen)
rsimacrossup = cross(rsi,ma) and rsi > ma
rsimacrossdown = cross(rsi,ma) and rsi < ma
plotchar(rsimacrossup, char='⇧', location = location.belowbar, color = green, text = "", textcolor = green, size=size.small)
plotchar(rsimacrossdown, char='⇩', location = location.abovebar, color = red, text = "", textcolor = red, size=size.small)
plotchar(rsi > rsioverbought, char='x', location = location.belowbar, color = aqua, text = "", textcolor = red, size=size.small)
plotchar(rsi < rsioversold, char='x', location = location.belowbar, color = aqua, text = "", textcolor = red, size=size.small)


closetrade = rsimacrossup or rsimacrossdown
strategy.close_all(closetrade)
strategy.close_all((rsi > rsioverbought) or (rsi < rsioversold))
strategy.entry("Short Overbought",strategy.short, when=(rsi > rsioverbought) and backtestdaterange)
strategy.entry("Buy Overbought",strategy.long, when=(rsi < rsioversold) and backtestdaterange)
strategy.entry("Long Cross", strategy.long, when=rsimacrossup and backtestdaterange)
strategy.entry("Short Cross", strategy.short, when=rsimacrossdown and backtestdaterange)

```

> Detail

https://www.fmz.com/strategy/436099

> Last Modified

2023-12-21 11:30:27
