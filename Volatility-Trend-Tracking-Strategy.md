
> Name

Based on Volatility-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c5820774c1f3cee91b.png)
[trans]
## Overview
This strategy uses the WaveTrend indicator to determine price trends and overbought and oversold conditions, combines the RSI indicator to filter signals, and uses trend tracking to perform reverse operations at overbought and oversold levels.
## Strategy Principle
This strategy uses the WaveTrend indicator to determine the price trend direction. The WaveTrend indicator is improved from the Rainbow indicator and determines the price trend direction by calculating the difference between the Heikin-Ashi moving average and the absolute value of the price. Combined with the RSI indicator to determine overbought and oversold conditions, a trading signal is issued.
Specifically, the WaveTrend formula in the strategy is:
```
esa = ema(hlc3, 10) 
d = ema(abs(hlc3 - esa), 10)
ci = (hlc3 - esa) / (0.015 * d)
wt = ema(ci, 21)
```
Among them, esa is the calculated Heikin-Ashi moving average, and d is the average difference between the Heikin-Ashi moving average and the absolute value of the price. ci is the so-called adaptive interval, which reflects the intensity of price fluctuations. wt is the moving average of ci, which is a key indicator for judging the price trend direction.
The RSI indicator is used to determine overbought and oversold. The calculation formula of RSI in the code is:
```
rsiup = rma(max(change(close), 0), 14) 
rsidown = rma(-min(change(close), 0), 14) 
rsi = rsidown == 0 ? 100 : rsiup == 0 ? 0 : 100 - (100 / (1 + rsiup / rsidown))
```
Its standard value is 0-100. Above 70 is the overbought zone, and below 30 is the oversold zone.
Combining these two indicators, when RSI is lower than 25 and WaveTrend is lower than -60, it is an oversold zone and a long signal; when RSI is higher than 75 and WaveTrend is higher than 60, it is an overbought zone and a short signal.
## Advantage Analysis
This strategy has the following advantages:
1. Use the WaveTrend indicator to determine the price trend direction accurately and reliably.
2. RSI indicator filtering can avoid unnecessary transactions and improve the winning rate. 
3. Using trend tracking methods, you can maximize the profits brought by capturing price trends.
4. The strategic ideas are clear and easy to understand, and the parameter settings are flexible and can be adjusted according to different varieties and markets.
5. The strategy is simple to implement, easy to verify, and is conducive to framework optimization.
## Risk Analysis
There are also some risks with this strategy:
1. Both WaveTrend and RSI indicators have a certain lag and may miss the price reversal point.
2. Although there are filtering conditions, false signals may still be generated in volatile market conditions.
3. The trailing stop loss strategy needs to be improved and cannot effectively control single losses.
4. It is very critical that the parameter settings are reasonable and match the characteristics of the product and the frequency of transactions.
Countermeasures:
1. Optimize by combining additional judgment indicators to improve signal accuracy. 
2. Add a stop-loss strategy to control single losses.
3. Find the best parameter combination and adjust the strategy to adapt to market varieties.
## Optimization direction
This strategy can be optimized from the following directions:
1. Replace the judgment indicator or add a judgment indicator to optimize the accuracy of the signal. For example, add MACD, KD and other judgment indicators.
2. Optimize parameter settings to adapt to different trading varieties. For example, adjust the smoothing period and find the best parameter combination.
3. Add a trailing stop loss strategy to effectively control single losses. For example, balance percentage stop loss, trailing stop loss, etc.
4. Consider different strategies for adding positions. For example, use Martingale to increase your position instead of the original fixed quantity increase.
5. Optimize the adaptability interval parameters and find the best parameters to improve the accuracy of judgment.
## Summary
The overall idea of this strategy is clear, using volatility indicators to judge price trends and effectively filtering noise trading signals. The strategy optimization space is large and can be improved from multiple angles to make the strategy more stable and reliable. Through parameter adjustment and optimization, it can be adapted to different trading varieties and is worthy of further testing and verification.
||

## Overview
This strategy uses the WaveTrend indicator to determine price trends and overbought/oversold situations. It combines the RSI indicator to filter signals and adopts a trend tracking method to make counter-trend operations at overbought/oversold levels.

## Strategy Logic  
The strategy uses the WaveTrend indicator to determine the price trend direction. The WaveTrend indicator is improved based on the Rainbow indicator. It judges the price trend direction by calculating the difference between the Heikin-Ashi moving average and the absolute value of the price. It generates trading signals by combining the RSI indicator to determine overbought/oversold situations.

Specifically, the WaveTrend formula in the strategy is:
```
esa = ema(hlc3, 10)
d = ema(abs(hlc3 - esa), 10) 
ci = (hlc3 - esa) / (0.015 * d)
wt = ema(ci, 21)
```
Where esa is the calculated Heikin-Ashi moving average, d is the mean of the difference between the Heikin-Ashi moving average and the absolute value of the price. ci is the so-called adaptive range, reflecting the volatility of prices. wt is the moving average of ci, which determines the price trend direction and is the key indicator for long and short.

The RSI indicator is used to determine overbought/oversold situations. The RSI calculation formula in the code is:
``` 
rsiup = rma(max(change(close), 0), 14)
rsidown = rma(-min(change(close), 0), 14)
rsi = rsidown == 0 ? 100 : rsiup == 0 ? 0 : 100 - (100 / (1 + rsiup / rsidown)) 
```
Its standard value is 0-100. Above 70 is overbought and below 30 is oversold.

Combined with these two indicators, when RSI is below 25 and WaveTrend is below -60, it is oversold to go long. When RSI is above 75 and WaveTrend is above 60, it is overbought to go short.

## Advantage Analysis
The advantages of this strategy include:

1. WaveTrend indicator can accurately and reliably determine the price trend direction.
2. RSI filters can avoid unnecessary trades and improve win rate.
3. Trend tracking method can maximize profits from catching price trends.  
4. The strategy idea is simple and clear, parameters are flexible to adjust for different products and markets.
5. Easy to implement and test in live trading, good for further optimization.

## Risk Analysis
There are also some risks:  

1. Both WaveTrend and RSI have some lag, may miss price reversal points. 
2. False signals may still occur in sideways markets despite filters.
3. Lack of effective stop loss method to control single loss.
4. Reasonable parameter tuning needs to match characteristics and trading frequency.

Solutions:
1. Add indicators for combinational optimizations to improve signal accuracy.
2. Add stop loss strategies to control single loss. 
3. Find optimal parameter combinations to adapt the strategy.

## Optimization Directions
The strategy can be optimized in the following directions:

1. Change or add judgment indicators to improve signal accuracy, e.g. MACD, KD etc.

2. Optimize parameter settings to adapt different products, e.g. adjust smooth periods. 

3. Add tracking stop loss strategies to control single loss, e.g. percentage stop loss, trailing stop loss etc.

4. Consider different pyramiding strategies, e.g. Martingale instead of fixed quantity.

5. Optimize adaptive range parameters to improve judgment accuracy.  

## Conclusion  
The overall idea of the strategy is clear, using volatility indicators to determine price trends and filter noise effectively. There is room for optimization in multiple aspects to make the strategy more robust. Through parameter tuning, it can be adapted to different products and is worth further live testing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|false|Use Martingale|
|v_input_4|100|Capital, %|
|v_input_5|true|Show Arrows|
|v_input_6|2018|From Year|
|v_input_7|2100|To Year|
|v_input_8|true|From Month|
|v_input_9|12|To Month|
|v_input_10|true|From day|
|v_input_11|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's WaveTrender Strategy v1.0", shorttitle = "WaveTrender str 1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 10)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
usemar = input(false, defval = false, title = "Use Martingale")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
showarr = input(true, defval = true, title = "Show Arrows")
fromyear = input(2018, defval = 2018, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//RSI
rsiup = rma(max(change(close), 0), 14)
rsidown = rma(-min(change(close), 0), 14)
rsi = rsidown == 0 ? 100 : rsiup == 0 ? 0 : 100 - (100 / (1 + rsiup / rsidown))

//WaveTrend
esa = ema(hlc3, 10)
d = ema(abs(hlc3 - esa), 10)
ci = (hlc3 - esa) / (0.015 * d)
wt = ema(ci, 21)

//Body
body = abs(close - open)
abody = sma(body, 10)

//Signals
bar = close > open ? 1 : close < open ? -1 : 0
overs = rsi < 25 and wt < -60
overb = rsi > 75 and wt > 60
up1 = (strategy.position_size == 0 or close < strategy.position_avg_price) and overs and bar == -1
dn1 = (strategy.position_size == 0 or close > strategy.position_avg_price) and overb and bar == 1
exit = (strategy.position_size > 0 and overs == false) or (strategy.position_size < 0 and overb == false)

//Arrows
col = exit ? black : up1 or dn1 ? blue : na
needup = up1
needdn = dn1
needexitup = exit and strategy.position_size < 0
needexitdn = exit and strategy.position_size > 0
plotarrow(showarr and needup ? 1 : na, colorup = blue, colordown = blue, transp = 0)
plotarrow(showarr and needdn ? -1 : na, colorup = blue, colordown = blue, transp = 0)
plotarrow(showarr and needexitup ? 1 : na, colorup = black, colordown = black, transp = 0)
plotarrow(showarr and needexitdn ? -1 : na, colorup = black, colordown = black, transp = 0)

//Trading
profit = exit ? ((strategy.position_size > 0 and close > strategy.position_avg_price) or (strategy.position_size < 0 and close < strategy.position_avg_price)) ? 1 : -1 : profit[1]
mult = usemar ? exit ? profit == -1 ? mult[1] * 2 : 1 : mult[1] : 1
lot = strategy.position_size == 0 ? strategy.equity / close * capital / 100 * mult : lot[1]

if up1
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot)

if dn1
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot)
    
if exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/441960

> Last Modified

2024-02-18 10:07:29
