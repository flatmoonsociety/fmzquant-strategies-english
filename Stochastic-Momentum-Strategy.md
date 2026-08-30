
> Name

Relative Strength Index Quantitative Trading Strategy Stochastic-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/65cf30936b9b596545eaa4b7da4b34ab6f102f5793638263a7584433ce503a4b.png)
[trans]
## Overview
The momentum swing strategy is a quantitative trading strategy that combines the stochastic momentum indicator and the relative strength indicator. This strategy uses the stochastic momentum indicator to determine the overbought and oversold areas of the market, cooperates with the fast RSI indicator to filter signals, and then uses entity filtering to achieve more reliable trading signal selection.
## Strategy Principle
### Stochastic Momentum Indicator
The Stochastic Momentum Index (SMI) is a commonly used technical indicator in quantitative trading, which combines the advantages of momentum indicators and oscillators.
Specifically, the calculation formula of SMI is:
SMI = (Close - (HH + LL)/2)/(0.5*(HH - LL)) * 100

Among them, HH is the highest price in the past N days, and LL is the lowest price in the past N days.
In this way, SMI combines the trend judgment of momentum and the reversal judgment of shock. When the SMI is above 80, it is overbought, and when it is below 20, it is oversold. The strategy generates trading signals in overbought and oversold areas.
### Rapid RSI
The Relative Strength Index (RSI) is a commonly used indicator of overbought and oversold. This strategy uses the rapid RSI with a period of 7 to determine overbought and oversold conditions in the short term.
When the Rapid RSI is below 20, it is oversold, and when it is above 80, it is overbought. The strategy generates trading signals in overbought and oversold areas.
### Entity filtering
This strategy also adds an entity filter to filter some signals by calculating the size of the K-line entity. Only when the K-line entity exceeds a certain threshold, a trading signal will be issued.
This can filter out some false signals and improve signal reliability.
## Strategic Advantages
###Multiple indicator combinations
This strategy combines three components: Stochastic Momentum Indicator, Fast RSI Indicator and Reality Filter. Through the combination of multiple indicators, the signal accuracy can be improved and the strategy robustness can be enhanced.
### Overbought and oversold judgment
Both the stochastic momentum indicator and the fast RSI indicator can accurately determine the overbought and oversold status of the market. The strategy opens a position in the overbought and oversold area and follows the trading principle of buying low and selling high.
### Two-way transaction
The strategy can conduct long and short two-way transactions to maximize the capture of trading opportunities in the market.
### Risk Control
The addition of physical filters can filter out most of the noise and avoid being trapped in volatile market conditions.
## Strategy Risk
### Risks of long-short switching
The strategy conducts two-way trading, and frequent switching between long and short positions is a potential risk point. Appropriate optimization of position opening logic can reduce this risk.
### Risk of following the trend
When the indicator gives a signal, a large number of traders following the trend may gather in a short period of time, leading to the risk of market reversal. This risk can be reduced by optimizing indicator parameters.
### Market systemic risk
Under extreme market conditions, all models may fail. This requires controlling such risks by setting stop losses appropriately.
## Strategy optimization
### Parameter optimization
You can find the best parameters to improve strategy profitability by testing different parameter combinations, such as SMI cycle, RSI cycle, entity filter threshold, etc.
### Dynamic Stop Loss
Establishing a dynamic stop-loss mechanism based on ATR or volatility can better control individual stocks and overall risks.
### Machine Learning
Introduce machine learning algorithms to predict the future trend of indicator values through the model. This can determine the turning point of the indicator in advance and enhance the forward-lookingness of the strategy.
## Summarize
To sum up, this strategy integrates the stochastic momentum indicator, fast RSI indicator and entity filter to achieve a relatively complete overbought and oversold judgment system. Multi-indicator combinations improve signal accuracy, and two-way trading and risk control mechanisms also make the strategy more balanced. By continuously optimizing parameters and models, this strategy is expected to obtain better returns.
||

## Overview

The Stochastic Momentum Strategy is a quantitative trading strategy that combines the Stochastic Momentum Index (SMI) and the Relative Strength Index (RSI). It uses the SMI to identify overbought and oversold areas in the market, with the fast RSI acting as a signal filter. It also implements a body filter for more reliable signal selection.

## Strategy Principles  

### Stochastic Momentum Index

The Stochastic Momentum Index (SMI) is a common technical indicator used in quantitative trading that combines the strengths of momentum and oscillation indicators. 

Specifically, the SMI is calculated as:

SMI = (Close - (HH + LL)/2)/(0.5*(HH - LL)) * 100

where HH is the highest price over the past N days, and LL is the lowest price.  

So the SMI incorporates both the trend-following judgment of momentum and the reversal judgment of oscillation. Values above 80 are considered overbought, while values below 20 are oversold. The strategy generates trading signals when SMI reaches these overbought or oversold levels.

### Fast RSI 

The Relative Strength Index (RSI) is a standard overbought/oversold indicator. This strategy uses a fast RSI with a period of 7 to judge short-term overbought/oversold conditions. 

Readings below 20 are considered oversold, while those above 80 are deemed overbought per the fast RSI. Signals are generated when these thresholds are breached.

### Body Filter

The strategy also implements a body filter by checking the candlestick body size to filter certain signals. Only bodies exceeding a set threshold will trigger trades.  

This filters out some false signals and increases reliability. 

## Advantages

### Multi-Indicator Combo 

This approach combines the SMI, fast RSI, and body filter into a robust 3-part system. Using multiple integrated signals improves accuracy and enhances stability.

### Overbought/Oversold Detection

Both SMI and fast RSI are excellent for detecting exhausted trends. By trading mean-reversions from these overextended areas, the strategy adheres to buying low and selling high.  

### Two-Way Trading

The ability to both buy dips and short rallies maximizes opportunities across market conditions.  

### Risk Control

The body filter avoids whipsaws by rejecting low-conviction signals in choppy conditions.

## Risks

### Whipsaws

Frequent long/short switching brings whipsaw risk. Optimizing logic could minimize this.  

### Crowded Trades 

Signals may cluster market participants and spur quick reversals upon entry. Fine-tuning parameters could reduce herding risk.

### Black Swans

Extreme events can upend all models. Intelligent stop losses are necessary to control systematic risks.  

## Enhancements

### Parameter Optimization

Testing different SMI/RSI periods and body filter thresholds could uncover optimal values for higher returns.

### Dynamic Stops 

Incorporating volatility-based or ATR stops would better contain position and portfolio risk.

### Machine Learning

Models predicting future indicator levels could identify turning points earlier. This would enhance predictive power.  

## Conclusion

In summary, by integrating the SMI, fast RSI, and body filter, this strategy has created a fairly comprehensive overbought/oversold system. The multi-signal approach improves accuracy, while two-way trade capability and risk controls contribute to balance. With continual parameter and model optimization, it shows promise for capturing gains over the long run.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|false|Use Martingale|
|v_input_4|100|Capital, %|
|v_input_5|true|Use SMI Strategy|
|v_input_6|true|Use RSI Strategy|
|v_input_7|true|Use Body-Filter|
|v_input_8|5|SMI Percent K Length|
|v_input_9|3|SMI Percent D Length|
|v_input_10|50|SMI Limit|
|v_input_11|2017|From Year|
|v_input_12|2100|To Year|
|v_input_13|true|From Month|
|v_input_14|12|To Month|
|v_input_15|true|From day|
|v_input_16|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-22 00:00:00
end: 2024-01-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's Stochastic Strategy v1.1", shorttitle = "Stochastic str 1.1", overlay = false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings 
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
usemar = input(false, defval = false, title = "Use Martingale")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
usesmi = input(true, defval = true, title = "Use SMI Strategy")
usersi = input(true, defval = true, title = "Use RSI Strategy")
usebod = input(true, defval = true, title = "Use Body-Filter")
a = input(5, "SMI Percent K Length")
b = input(3, "SMI Percent D Length")
limit = input(50, defval = 50, minval = 1, maxval = 100, title = "SMI Limit")
fromyear = input(2017, defval = 2017, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Fast RSI
fastup = rma(max(change(close), 0), 7)
fastdown = rma(-min(change(close), 0), 7)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//Stochastic Momentum Index
ll = lowest (low, a)
hh = highest (high, a)
diff = hh - ll
rdiff = close - (hh+ll)/2
avgrel = ema(ema(rdiff,b),b)
avgdiff = ema(ema(diff,b),b)
SMI = avgdiff != 0 ? (avgrel/(avgdiff/2)*100) : 0
SMIsignal = ema(SMI,b)

//Lines
plot(SMI, color = blue, linewidth = 3, title = "Stochastic Momentum Index")
plot(SMIsignal, color = red, linewidth = 3, title = "SMI Signal Line")
plot(limit, color = black, title = "Over Bought")
plot(-1 * limit, color = black, title = "Over Sold")
plot(0, color = blue, title = "Zero Line")

//Body Filter
nbody = abs(close - open)
abody = sma(nbody, 10)
body = nbody > abody / 3 or usebod == false

//Signals
up1 = SMIsignal < -1 * limit and close < open and body and usesmi
dn1 = SMIsignal > limit and close > open and body and usesmi
up2 = fastrsi < 20 and close < open and body and usersi
dn2 = fastrsi > 80 and close > open and body and usersi
exit = ((strategy.position_size > 0 and close > open) or (strategy.position_size < 0 and close < open)) and body

//Trading
profit = exit ? ((strategy.position_size > 0 and close > strategy.position_avg_price) or (strategy.position_size < 0 and close < strategy.position_avg_price)) ? 1 : -1 : profit[1]
mult = usemar ? exit ? profit == -1 ? mult[1] * 2 : 1 : mult[1] : 1
lot = strategy.position_size == 0 ? strategy.equity / close * capital / 100 * mult : lot[1]

if up1 or up2
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("long", strategy.long, needlong == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if dn1 or dn2
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if time > timestamp(toyear, tomonth, today, 23, 59) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/439602

> Last Modified

2024-01-22 10:13:23
